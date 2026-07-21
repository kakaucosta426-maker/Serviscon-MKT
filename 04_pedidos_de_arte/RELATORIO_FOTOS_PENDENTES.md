# Relatório de Fotos Pendentes
## Resumo
- Total de pedidos auditados: 9
- Fotografias encontradas localmente: 0
- Fotografias versionadas no Git: 0
- Pedidos prontos para processar: 0
- Pedidos aguardando fotografia: 9

## Auditoria dos pedidos
| Pedido | Campanha | Fotografia esperada | Caminho esperado | Extensão | Categoria | Arquivo existe | Está versionado | Saída esperada | Status |
|---|---|---|---|---|---|---|---|---|---|
| `ARTE-20260721-STORY-001` | Story Dia 1 - Limpeza profissional | `serviscon_limpeza_001.jpg` | `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.jpg` | `jpg` | `limpeza_e_conservacao` | Não | Não | `05_producao/design/artes_geradas/story-dia-1-limpeza-profissional.png` | aguardando_foto |
| `ARTE-20260721-STORY-002` | Story Dia 1 - Segurança na limpeza | `serviscon_limpeza_006.jpg` | `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_006.jpg` | `jpg` | `limpeza_e_conservacao` | Não | Não | `05_producao/design/artes_geradas/story-dia-1-seguranca-limpeza.png` | aguardando_foto |
| `ARTE-20260721-STORY-003` | Story Dia 1 - Supervisão operacional | `serviscon_supervisao_001.jpg` | `03_base_de_conhecimento/banco_de_imagens/supervisao_operacional/serviscon_supervisao_001.jpg` | `jpg` | `supervisao_operacional` | Não | Não | `05_producao/design/artes_geradas/story-dia-1-supervisao-operacional.png` | aguardando_foto |
| `ARTE-20260721-STORY-004` | Story Dia 2 - Portaria profissional | `serviscon_portaria_003.jpg` | `03_base_de_conhecimento/banco_de_imagens/portaria/serviscon_portaria_003.jpg` | `jpg` | `portaria` | Não | Não | `05_producao/design/artes_geradas/story-dia-2-portaria-profissional.png` | aguardando_foto |
| `ARTE-20260721-STORY-005` | Story Dia 2 - Controle de acesso | `serviscon_portaria_001.jpg` | `03_base_de_conhecimento/banco_de_imagens/portaria/serviscon_portaria_001.jpg` | `jpg` | `portaria` | Não | Não | `05_producao/design/artes_geradas/story-dia-2-controle-de-acesso.png` | aguardando_foto |
| `ARTE-20260721-STORY-006` | Story Dia 2 - Comunicação operacional | `serviscon_supervisao_002.jpg` | `03_base_de_conhecimento/banco_de_imagens/supervisao_operacional/serviscon_supervisao_002.jpg` | `jpg` | `supervisao_operacional` | Não | Não | `05_producao/design/artes_geradas/story-dia-2-comunicacao-operacional.png` | aguardando_foto |
| `ARTE-20260721-STORY-007` | Story Dia 3 - Equipe em operação | `serviscon_limpeza_005.jpg` | `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_005.jpg` | `jpg` | `limpeza_e_conservacao` | Não | Não | `05_producao/design/artes_geradas/story-dia-3-equipe-em-operacao.png` | aguardando_foto |
| `ARTE-20260721-STORY-008` | Story Dia 3 - Jardinagem | `serviscon_jardinagem_002.jpg` | `03_base_de_conhecimento/banco_de_imagens/jardinagem/serviscon_jardinagem_002.jpg` | `jpg` | `jardinagem` | Não | Não | `05_producao/design/artes_geradas/story-dia-3-jardinagem.png` | aguardando_foto |
| `ARTE-20260721-STORY-009` | Story Dia 3 - Terceirização com gestão | `serviscon_limpeza_008.jpg` | `03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_008.jpg` | `jpg` | `limpeza_e_conservacao` | Não | Não | `05_producao/design/artes_geradas/story-dia-3-terceirizacao-com-gestao.png` | aguardando_foto |

## Verificação do banco de imagens
- Pasta verificada: `03_base_de_conhecimento/banco_de_imagens/`.
- Arquivos de imagem encontrados localmente no banco oficial: 0.
- Arquivos de imagem encontrados em outras pastas do projeto: 0.
- Arquivo `.gitignore` encontrado no projeto: não.
- Conclusão: as fotografias estão descritas no `catalogo.json` e nos metadados individuais, mas os binários `.jpg` não foram adicionados ao projeto.

## Ação aplicada
- Pedidos sem fotografia binária disponível foram movidos para `04_pedidos_de_arte/aguardando_fotos/`.
- O status desses pedidos foi alterado para `aguardando_foto`.
- Cada pedido recebeu o bloco `pendencia` com o caminho da fotografia real esperada.
- Nenhuma fotografia fictícia, vazia, gerada por IA, SVG, HTML ou código foi criada.
