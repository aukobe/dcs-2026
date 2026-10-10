# 00. Persona

> Etapa 1 do SDD. Preenchido pelo prompt 1 (Persona) e revisado pelo grupo.
> Descreva pessoas reais do problema, não o agente. Uma persona principal basta;
> acrescente secundárias só se elas tomarem decisões diferentes.

## Persona principal

| Campo | Descrição |
|---|---|
| Nome e papel | Engenheiro de dados do grupo (MBA Engenharia de Dados, Mackenzie, 2026) |
| Contexto | Trabalha no Codespace próprio, no único repositório público do grupo no GitHub; publica no Railway com crédito único de US$ 5 (trial de até 30 dias) |
| Decisão que toma com o dado | Escolhe onde persistir os JSONs brutos gerados na coleta horária (Aula 02) e nas aulas seguintes (03, 04) e no projeto final, de modo que qualquer integrante possa reproduzir os pipelines |
| Dor atual | Cada integrante guarda arquivos no próprio Codespace; quando o Codespace é apagado, os dados coletados somem e ninguém consegue reproduzir a coleta do colega |
| Frequência de uso | Coleta horária na Aula 02; uso contínuo nas Aulas 03, 04 e no projeto final |
| O que considera sucesso | Dados persistem entre sessões, qualquer integrante acessa o mesmo objeto, custo cabe no crédito único de teste disponível para o semestre |
| O que não aceita | Perder dados ao recriar Codespace; depender de serviço externo pago; configuração manual a cada nova execução |

## Personas secundárias (opcional)

## Fatos, lacunas e suposições

| Tipo | Afirmação | Origem |
|---|---|---|
| Fato | O grupo tem um único repositório público no GitHub e cada integrante trabalha no próprio Codespace | Enunciado da Aula 01 |
| Fato | A plataforma de publicação é o Railway, com crédito único de US$ 5 no trial de até 30 dias | Enunciado da Aula 01 |
| Fato | Volumes de contas trial são apagados 30 dias após o fim dos créditos | Enunciado da Aula 01 |
| Fato | A coleta da Aula 02 será horária e gravará JSON bruto | Enunciado da Aula 01 |
| Lacuna | Volume estimado de dados por coleta horária | Não informado |
| Fato | O grupo tem três integrantes | informado pelo grupo |

## Perguntas abertas

- Haverá necessidade de versionamento de objetos?
- O grupo precisa de políticas de retenção ou lifecycle para os dados?