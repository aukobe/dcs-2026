# Especificação

> Etapa 3 do SDD. Preenchido pelo prompt 3 a partir da persona e dos objetivos.
> A spec diz O QUE o sistema faz e com qual qualidade. Não escolha tecnologia aqui,
> exceto quando uma restrição de `docs/01_objetivos_negocio.md` já a impuser.

## Contexto e escopo

O storage do projeto implementa um MinIO compatível com a API S3 para persistir os JSONs brutos coletados nas Aulas 02, 03, 04 e no projeto final, permitindo que qualquer integrante do grupo recrie o ambiente do zero e acesse os dados.

## Requisitos funcionais

### RF-01: API compatível com S3 publicada por HTTPS num domínio do Railway
- **Origem:** OBJ-03, OBJ-02
- **Critério de aceite:**
  - Dado o endpoint da API S3 no Railway
  - Quando o comando `mc ls railway` for executado
  - Então o endpoint começa com `https://` e a lista de buckets é retornada

### RF-02: buckets raw, bronze, silver e gold
- **Origem:** OBJ-04
- **Critério de aceite:**
  - Dado o MinIO no ar com credenciais válidas no .env
  - Quando scripts/criar_buckets.sh railway for executado duas vezes seguidas
  - Então ambas as execuções terminam com código 0 e mc ls lista exatamente os quatro buckets

### RF-03: ambiente local equivalente por docker compose, com a mesma imagem e tag
- **Origem:** OBJ-04
- **Critério de aceite:**
  - Dado o docker-compose.yml com a mesma imagem e tag que o Railway
  - Quando docker compose up -d é executado
  - Então o container do MinIO roda em 0.0.0.0:9000:9000 (API S3) e 0.0.0.0:9001:9001 (console)

### RF-04: verificação automatizada, local e no Railway
- **Origem:** OBJ-02, OBJ-03
- **Critério de aceite (local):**
  - Dado o MinIO local está ativo
  - Quando os comandos `mc ready minio`, `mc ls minio` listando os quatro buckets, e `mc cp raw/_verificacao/teste.json minio/` seguido de `mc get minio/raw/_verificacao/teste.json` são executados
  - Então o objeto é gravado e lido com conteúdo idêntico
- **Critério de aceite (railway):**
  - Dado o MinIO no Railway está ativo
  - Quando os mesmos comandos são executados usando o alias railway
  - Então os quatro buckets aparecem e o objeto de teste está disponível

### RF-05: recriação documentada do zero
- **Origem:** OBJ-04
- **Critério de aceite:**
  - Dado um ambiente limpo sem armazenamento MinIO
  - Quando o procedimento de recriação descrito no README é executado por qualquer integrante
  - Então a recriação termina sem erro e a verificação automatizada do RF-04 passa

### RF-06: acesso autenticado e segredos fora do Git
- **Origem:** OBJ-03
- **Critério de aceite:**
  - Dado o .env com as credenciais do MinIO está no .env
  - Quando (a) um cliente tenta acessar a API S3 sem fornecer credenciais e recebe 403, e (b) `git ls-files | grep '\.env$'` não retorna nada
  - Então o acesso é negado e os segredos não estão versionados no repositório

### RF-07: imagem fixada por tag, nunca latest
- **Origem:** RES-02
- **Critério de aceite:**
  - Dado os arquivos docker-compose.yml e minio_railway/Dockerfile
  - Quando os comandos `git grep -n "RELEASE.2025-10-15T17-29-55Z"` e `git grep -n latest` são executados
  - Então a tag `RELEASE.2025-10-15T17-29-55Z` aparece nos dois arquivos e `latest` não aparece como tag de imagem

## Requisitos não funcionais (atributos de qualidade)

### RNF-01: persistência entre deploys
- **Atributo:** disponibilidade
- **Origem:** OBJ-02
- **Critério de aceitável:**
  - Dado um objeto é gravado no MinIO antes do redeploy
  - Quando o serviço é redesployado
  - Então o objeto continua presente e acessível via mc ls

### RNF-02: custo acompanhado dentro do crédito
- **Atributo:** custo
- **Origem:** OBJ-01, RES-01
- **Critério de aceitável:**
  - Dado o consumo do crédito é consultado no painel do Railway
  - Quando o consumo é registrado em docs/evidencias/ com frequência definida
  - Então o custo permanece dentro do limite do crédito; hipótese: validação pendente

### RNF-03: tolerância a 502 do proxy com nova tentativa e operações idempotentes
- **Atributo:** disponibilidade, idempotência
- **Origem:** experiência do professor com serviços no Railway (Fato adicional)
- **Critério de aceitável:**
  - Dado um objeto é gravado via mc cp minio/ test.json enquanto o proxy do Railway devolve 502 esporádico
  - Quando o cliente repete a operação com espera crescente
  - Então o objeto existe uma única vez na chave esperada; tentativas máximas: hipótese: validação pendente

### RNF-04: evidências de verificação registradas em docs/evidencias/
- **Atributo:** rastreabilidade
- **Origem:** enunciado da Aula 01
- **Critério de aceitável:**
  - Dado qualquer verificação é executada (local ou no Railway)
  - Quando a verificação é concluída com sucesso
  - Então a saída da verificação completa é registrada em docs/evidencias/ com a data e o comando

## Fora do escopo

- Alta disponibilidade com múltiplos nós
- Console web público
- Backup automatizado agendado

## Perguntas abertas

- Haverá necessidade de versionamento de objetos?
- O grupo precisa de políticas de retenção ou lifecycle para os dados?