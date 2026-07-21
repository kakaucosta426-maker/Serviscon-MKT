# Aprovação — Stories 3 dias

## Status
Todas as 9 artes de stories foram aprovadas pelo cliente em 2026-07-21 para seguir no fluxo automático de geração pelo n8n/OpenAI.

## Escopo aprovado
- Quantidade aprovada: 3 stories por dia durante 3 dias.
- Total aprovado: 9 stories.
- Canal: Instagram Stories.
- Formato visual aprovado: 1080x1920.
- Operação de imagem aprovada: `gerar_com_imagem_de_referencia`.
- Banco de imagens aprovado para uso: `03_base_de_conhecimento/banco_de_imagens/`.
- Pasta de pedidos aprovados para processamento: `04_pedidos_de_arte/pendentes/`.
- Pasta de saída das artes finais: `05_producao/design/artes_geradas/`.

## Stories aprovados
| ID | Story | Serviço/tema | Foto base | Pedido JSON | Status de aprovação |
|---|---|---|---|---|---|
| STORY-001 | Story Dia 1 - Limpeza profissional | Limpeza e conservação | LIMP-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120001_story-dia-1-limpeza-profissional.json` | Aprovado para geração |
| STORY-002 | Story Dia 1 - Segurança na limpeza | Segurança na operação de limpeza | LIMP-006 | `04_pedidos_de_arte/pendentes/pedido_20260721_120002_story-dia-1-seguranca-limpeza.json` | Aprovado para geração |
| STORY-003 | Story Dia 1 - Supervisão operacional | Supervisão operacional | SUP-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120003_story-dia-1-supervisao-operacional.json` | Aprovado para geração |
| STORY-004 | Story Dia 2 - Portaria profissional | Portaria | PORT-003 | `04_pedidos_de_arte/pendentes/pedido_20260721_120004_story-dia-2-portaria-profissional.json` | Aprovado para geração |
| STORY-005 | Story Dia 2 - Controle de acesso | Controle de acesso | PORT-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120005_story-dia-2-controle-de-acesso.json` | Aprovado para geração |
| STORY-006 | Story Dia 2 - Comunicação operacional | Comunicação e supervisão | SUP-002 | `04_pedidos_de_arte/pendentes/pedido_20260721_120006_story-dia-2-comunicacao-operacional.json` | Aprovado para geração |
| STORY-007 | Story Dia 3 - Equipe em operação | Equipe e padronização | LIMP-005 | `04_pedidos_de_arte/pendentes/pedido_20260721_120007_story-dia-3-equipe-em-operacao.json` | Aprovado para geração |
| STORY-008 | Story Dia 3 - Jardinagem | Jardinagem e paisagismo | JARD-002 | `04_pedidos_de_arte/pendentes/pedido_20260721_120008_story-dia-3-jardinagem.json` | Aprovado para geração |
| STORY-009 | Story Dia 3 - Terceirização com gestão | Terceirização com gestão operacional | LIMP-008 | `04_pedidos_de_arte/pendentes/pedido_20260721_120009_story-dia-3-terceirizacao-com-gestao.json` | Aprovado para geração |

## Próxima etapa
O n8n deverá processar os pedidos JSON que permanecem em `04_pedidos_de_arte/pendentes/`, baixar as fotos reais indicadas em cada arquivo, enviar fotografia e prompt para a OpenAI e salvar as artes finais em `05_producao/design/artes_geradas/`.

## Observação operacional
A aprovação registrada aqui não significa que as imagens finais já foram geradas. O status `pendente` dos JSONs deve ser mantido até o n8n processar cada pedido e mover os arquivos para `04_pedidos_de_arte/concluidos/` ou `04_pedidos_de_arte/erros/`.
