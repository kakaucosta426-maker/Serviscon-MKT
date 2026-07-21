# Diagnóstico de produção — Stories 3 dias

## Status da produção
Os 9 pedidos reais de geração foram criados e permanecem na pasta monitorada pelo n8n:

`04_pedidos_de_arte/pendentes/`

## Verificações realizadas
- Pasta monitorada pelo n8n identificada: `04_pedidos_de_arte/pendentes/`.
- Formato aceito pelo workflow atual identificado nos documentos `04_pedidos_de_arte/README.md` e `GUIA_INTEGRACAO_N8N.md`.
- Catálogo consultado: `03_base_de_conhecimento/banco_de_imagens/catalogo.json`.
- Pedidos reais encontrados e atualizados com aprovação do cliente: 9.
- Tipo de operação mantido: `gerar_com_imagem_de_referencia`.
- Pasta esperada para saída final: `05_producao/design/artes_geradas/`.

## Campanhas em produção
| ID | Campanha | Foto real selecionada | Pedido |
|---|---|---|---|
| ARTE-20260721-STORY-001 | Story Dia 1 - Limpeza profissional | LIMP-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120001_story-dia-1-limpeza-profissional.json` |
| ARTE-20260721-STORY-002 | Story Dia 1 - Segurança na limpeza | LIMP-006 | `04_pedidos_de_arte/pendentes/pedido_20260721_120002_story-dia-1-seguranca-limpeza.json` |
| ARTE-20260721-STORY-003 | Story Dia 1 - Supervisão operacional | SUP-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120003_story-dia-1-supervisao-operacional.json` |
| ARTE-20260721-STORY-004 | Story Dia 2 - Portaria profissional | PORT-003 | `04_pedidos_de_arte/pendentes/pedido_20260721_120004_story-dia-2-portaria-profissional.json` |
| ARTE-20260721-STORY-005 | Story Dia 2 - Controle de acesso | PORT-001 | `04_pedidos_de_arte/pendentes/pedido_20260721_120005_story-dia-2-controle-de-acesso.json` |
| ARTE-20260721-STORY-006 | Story Dia 2 - Comunicação operacional | SUP-002 | `04_pedidos_de_arte/pendentes/pedido_20260721_120006_story-dia-2-comunicacao-operacional.json` |
| ARTE-20260721-STORY-007 | Story Dia 3 - Equipe em operação | LIMP-005 | `04_pedidos_de_arte/pendentes/pedido_20260721_120007_story-dia-3-equipe-em-operacao.json` |
| ARTE-20260721-STORY-008 | Story Dia 3 - Jardinagem | JARD-002 | `04_pedidos_de_arte/pendentes/pedido_20260721_120008_story-dia-3-jardinagem.json` |
| ARTE-20260721-STORY-009 | Story Dia 3 - Terceirização com gestão | LIMP-008 | `04_pedidos_de_arte/pendentes/pedido_20260721_120009_story-dia-3-terceirizacao-com-gestao.json` |

## Diagnóstico de bloqueio encontrado
Os metadados das fotografias estão no repositório, mas os arquivos binários `.jpg` referenciados nos pedidos não foram encontrados no caminho informado pelo catálogo.

Nó provável do n8n que falhará caso execute agora: `Baixar fotografia real do GitHub`.

Motivo provável: o campo `imagem.fotos_referencia[].arquivo` aponta para arquivos `.jpg` catalogados, mas os binários correspondentes ainda não estão versionados no repositório.

## Etapa que precisa ser corrigida
Antes do processamento completo pelo n8n, salvar no repositório os arquivos reais correspondentes às fotos usadas nos pedidos:

- `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.jpg`
- `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_006.jpg`
- `03_base_de_conhecimento/banco_de_imagens/supervisao_operacional/serviscon_supervisao_001.jpg`
- `03_base_de_conhecimento/banco_de_imagens/portaria/serviscon_portaria_003.jpg`
- `03_base_de_conhecimento/banco_de_imagens/portaria/serviscon_portaria_001.jpg`
- `03_base_de_conhecimento/banco_de_imagens/supervisao_operacional/serviscon_supervisao_002.jpg`
- `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_005.jpg`
- `03_base_de_conhecimento/banco_de_imagens/jardinagem/serviscon_jardinagem_002.jpg`
- `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_008.jpg`

## Imagens geradas
Nenhum PNG foi gerado localmente pelo Codex, conforme a regra do projeto. As artes finais devem ser produzidas pelo n8n/OpenAI e salvas em `05_producao/design/artes_geradas/`.
