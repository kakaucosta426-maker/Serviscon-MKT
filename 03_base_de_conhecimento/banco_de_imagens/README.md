# Banco de Imagens Oficial da Serviscon

Este diretório organiza as fotografias oficiais da Serviscon por serviço ou atividade principal.

## Regra de classificação
Cada imagem deve ser classificada pela atividade principal que aparece na cena. Se uma foto puder pertencer a mais de uma categoria, usar a categoria que representa melhor o serviço executado.

## Categorias criadas
- `jardinagem/`
- `portaria/`
- `limpeza_e_conservacao/`
- `supervisao_operacional/`

## Uso obrigatório pelo Designer
Antes de criar qualquer arte, o Designer deve consultar `indice_imagens.md` e priorizar fotografias reais da Serviscon. IA só deve ser usada quando não houver foto adequada ou para complementar elementos visuais, fundos e composições.

## Catálogo inteligente
O arquivo `catalogo.json` consolida todas as fotografias oficiais do banco de imagens e deve ser usado pelo Designer e pelo n8n para localizar a foto mais adequada de cada campanha.

Cada fotografia possui um arquivo `.json` de metadados na mesma pasta da categoria. Esses metadados registram serviço, ambiente, atividade, equipamentos, uniforme, orientação, qualidade, palavras-chave, possíveis usos e restrições.

### Regra de uso
Sempre que existir fotografia real compatível com o serviço divulgado, a campanha deve usar `tipo_operacao = editar_imagem`. Não gerar pessoas por IA quando houver fotografia real adequada da Serviscon.
