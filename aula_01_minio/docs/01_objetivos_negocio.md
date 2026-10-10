# 01. Objetivos de negócio

## Objetivos

| ID | Objetivo | Métrica de sucesso | Origem |
|----|----------|-------------------|---------|
| OBJ-01 | Custo dentro do crédito único de US$ 5 do trial do Railway, que vale por até 30 dias | O custo total de armazenamento e processamento permanece dentro do crédito único de US$ 5 disponível para o trial de até 30 dias | docs/00_persona.md |
| OBJ-02 | Dados persistem entre deploys e reinícios do serviço | Objetos gravados continuam disponíveis após novos deploys ou reinícios do serviço (zero objetos perdidos) | docs/00_persona.md |
| OBJ-03 | Acesso somente autenticado, sem segredo versionado no repositório público | Todos os recursos de armazenamento acessíveis apenas por usuários autenticados; nenhum segredo (senhas, chaves) versionado no repositório público do grupo | docs/00_persona.md |
| OBJ-04 | Storage recriável do zero por comandos documentados, por qualquer integrante | Um integrante recria o storage do zero usando apenas os comandos documentados, sem dependência de configuração manual | docs/00_persona.md |

## Drivers de negócio

| ID | Driver | Atributo de qualidade afetado |
|----|--------|-------------------------------|
| DRV-01 | Limitação de orçamento do trial do Railway (crédito único de US$ 5, válido por até 30 dias) | Custo operacional mantido dentro do limite de US$ 5 |
| DRV-02 | Necessidade de persistência de dados | Integridade e disponibilidade dos dados coletados entre execuções |
| DRV-03 | Colaboração da equipe | Reprodutibilidade dos pipelines e compartilhamento de dados entre membros |
| DRV-04 | O repositório do grupo é público no GitHub | Segurança e confidencialidade dos segredos |

## Restrições

| ID | Restrição | Tipo | Origem |
|----|-----------|------|--------|
| RES-01 | Orçamento limitado ao trial do Railway: crédito único de US$ 5, válido por até 30 dias; depois, plano Free com US$ 1 por mês; 1 GB de RAM, vCPU compartilhada e até 5 serviços por projeto; volumes de contas trial são apagados 30 dias após o fim dos créditos | Financeira | enunciado da Aula 01 |
| RES-02 | Imagem do MinIO: ghcr.io/coollabsio/minio com tag fixada | técnica | enunciado da Aula 01 |
| RES-03 | Repositório do grupo é público no GitHub | legal | enunciado da Aula 01 |
| RES-04 | Agente na OpenRouter com modelo gratuito e limite de 50 requisições por dia | técnica | enunciado da Aula 01 |

## Fora do escopo

- Alta disponibilidade com múltiplos nós
- Console web público
- Backup automatizado agendado

## Perguntas abertas

- Haverá necessidade de versionamento de objetos?
- O grupo precisa de políticas de retenção ou lifecycle para os dados?