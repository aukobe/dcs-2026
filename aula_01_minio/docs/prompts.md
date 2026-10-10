# Histórico de prompts

> Registro contínuo dos prompts CREATE efetivamente enviados ao agente, na ordem.
> Cole o texto exatamente como foi enviado, inclusive as correções. Não reescreva
> prompts antigos para parecerem melhores: o histórico real mostra como o projeto
> foi conduzido. Nunca cole chave, senha ou token aqui.

## P01: Persona

- Data e hora: 10/10/2026 16:00
- Quem enviou: Augusto
- Modelo usado: openrouter/openrouter/free
- Arquivos alterados: 00_persona.md
- Resultado da revisão ("Revise antes de seguir"): refeito. A primeira versão citava Railway e "bucket" nas linhas de sucesso e do que não aceita, e trazia uma suposição inventada sobre buckets. Pedi a correção ao agente e a versão corrigida foi aceita. Também registrei que o grupo tem 3 integrantes.

```text
[C] Personagem
Você é um analista de requisitos de engenharia de dados que trabalha com um grupo de alunos de MBA. Nesta etapa você só descreve pessoas e problemas. Você não propõe tecnologia, não escreve código e não executa comandos.

[R] Pedido
Preencha docs/00_persona.md para o projeto aula_01_minio: um object storage próprio do grupo, compatível com a API S3, que será usado nas Aulas 02, 03 e 04 da disciplina (coleta de JSON, APIs e scraping, lakehouse) e no projeto final. Descreva uma persona principal: o engenheiro de dados do grupo, que precisa de um object storage próprio, barato e reprodutível para o semestre. Use a tabela que já existe no arquivo.

[E] Exemplos
Linha bem escrita:
| Dor atual | Cada integrante guarda arquivos no próprio Codespace; quando o Codespace é apagado, os dados coletados somem e ninguém consegue reproduzir a coleta do colega. |
Linha mal escrita (não faça assim):
| Dor atual | Precisa de uma solução escalável e robusta na nuvem. |

[A] Ajustes
- Use somente as informações deste prompt, de AGENTS.md e dos fatos listados em Extras.
- Não invente números (volume de dados, quantidade de arquivos, custo, tempo). Onde faltar um valor, escreva "hipótese: validação pendente".
- Não cite produtos ou ferramentas nas linhas de dor e de sucesso; a persona fala do problema dela.
- Preencha "Fatos, lacunas e suposições" com pelo menos três linhas, cada fato com a origem.
- Não crie nem altere outros arquivos.

[T] Tipo de saída
Somente docs/00_persona.md, em Markdown, com no máximo uma página. Antes de editar, mostre em tópicos o que vai escrever e espere minha confirmação.

[E] Extras
Leia antes: AGENTS.md e docs/00_persona.md.
Fatos do contexto (origem: enunciado da Aula 01):
- o grupo tem um único repositório público no GitHub e cada integrante trabalha no próprio Codespace;
- a plataforma de publicação é o Railway, com crédito único de US$ 5 no trial de até 30 dias;
- volumes de contas trial são apagados 30 dias após o fim dos créditos;
- a coleta da Aula 02 será horária e gravará JSON bruto.
Se faltar informação para uma linha, pergunte antes de supor. Ao terminar, liste as perguntas abertas e pare.
```

## P02: Objetivos de negócio
