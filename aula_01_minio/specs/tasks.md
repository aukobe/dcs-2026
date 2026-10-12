# Tarefas

> Etapa 5 do SDD. Preenchido pelo prompt 5 a partir de `specs/plan.md`.
> Tarefa pequena: cabe em um prompt de implementação e termina com uma verificação
> executável. Marque [x] só depois de ver a saída da verificação.

| ID | Tarefa | Requisito | Verificação (teste ou comando) | Evidência esperada | Status |
|---|---|---|---|---|---|
| T-01 | Criar docker-compose.yml com imagem fixada por tag e volumes persistentes | RF-03, RF-07 | `docker compose up -d --wait`, `docker compose ps` mostrando healthy, `curl -s -o /dev/null -w '%{http_code}' http://localhost:9000/minio/health/live` devolvendo 200 | Container rodando nas portas 9000 e 9001, imagem com tag RELEASE.2025-10-15T17-29-55Z, healthcheck 200 | [x] |
| T-02 | Criar minio_railway/Dockerfile com imagem fixada por tag | RF-03, RF-07 | `docker build -t minio-teste minio_railway/` seguido de conferir com grep que o Dockerfile contém a tag RELEASE.2025-10-15T17-29-55Z e `CMD server /data --console-address ":9001"` | Build succeed; Dockerfile contém `FROM ghcr.io/coollabsio/minio:RELEASE.2025-10-15T17-29-55Z` e `CMD server /data --console-address ":9001"` | [x] |
| T-03 | Criar scripts/criar_buckets.sh que cria raw, bronze, silver e gold com mc mb --ignore-existing | RF-02, RNF-03 | `bash scripts/criar_buckets.sh local` executado duas vezes seguidas | Segunda execução termina com código 0; mc ls local lista 4 buckets; idempotência com nova tentativa e espera crescente (máx. 3 tentativas) | [ ] |
| T-04 | Criar scripts/verificar.sh que testa saúde, 403 anônimo, buckets, ida e volta de objeto (chave fixa raw/_verificacao/teste.json, até 3 tentativas com espera crescente), salva saída em docs/evidencias/ | RF-04, RF-06, RNF-03, RNF-04 | `bash scripts/verificar.sh local` | Saída salva em docs/evidencias/ com data e comando; saúde ok, 403 anônimo, 4 buckets, objeto gravado e lido com conteúdo idêntico | [ ] |
| T-05 | Criar README.md com instruções de recriação do zero | RF-05 | Seguir os comandos do README para recriar o ambiente local do zero e terminar com `bash scripts/verificar.sh local` com código 0 | Ambiente recriado com sucesso e verificação RF-04 passa | [ ] |
| T-06 | Deploy no Railway (executado pelo prompt 8): inclui `bash scripts/criar_buckets.sh railway` e `bash scripts/verificar.sh railway` | RF-01, RF-02, RF-04, RF-06 | Executado pelo grupo via prompt 8 | Serviço ativo no Railway com domínio HTTPS, 4 buckets listáveis, verificação railway passa | [ ] |
| T-07 | Teste de persistência com redeploy no Railway | RNF-01 | Gravar raw/_verificacao/teste.json, executar `railway redeploy --service minio --yes` e listar raw/_verificacao/ com `mc ls railway/raw/_verificacao/` | Objeto continua presente após redeploy | [ ] |

## Ordem de execução e dependências

1. T-01 (docker-compose.yml local) → T-02 (Dockerfile Railway) → T-03 (scripts/criar_buckets.sh) → T-04 (scripts/verificar.sh) → T-05 (README.md)
2. T-06 (deploy Railway) depende de T-01, T-02, T-03 e T-04 estar concluídos
3. T-07 (teste persistência) depende de T-06 estar concluído

## Tarefas que criam recursos no Railway ou consome crédito

- T-06: deploy no Railway — cria o serviço MinIO no Railway e consome crédito
- T-07: `railway redeploy --service minio --yes` — opera sobre o serviço do Railway

## Sem tarefa de código

- **RNF-02** (custo acompanhado dentro do crédito): o consumo do crédito é consultado manualmente no painel do Railway e registrado em `docs/evidencias/` com a data. Não há script de automação, pois depende de uma interface web externa.

## Tarefas manuais (feitas pelo grupo, não pelo agente)

- Instalar o cliente `mc` no Codespace
- Gerar a senha local em `MINIO_ROOT_PASSWORD` no `.env`
- Login no Railway
- Gerar e cadastrar usuário e senha do MinIO no Railway e em `MINIO_RAILWAY_USER` e `MINIO_RAILWAY_PASSWORD`
- Copiar o domínio do Railway, com `https://`, somente para `MINIO_RAILWAY_ENDPOINT`