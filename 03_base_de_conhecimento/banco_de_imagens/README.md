# Banco de Imagens Oficial da Serviscon

Este diretório organiza as fotografias oficiais da Serviscon por serviço ou atividade principal.

## Regra de classificação
Cada imagem deve ser classificada pela atividade principal que aparece na cena. Se uma foto puder pertencer a mais de uma categoria, usar a categoria que representa melhor o serviço executado.

## Categorias criadas
- `jardinagem/`
- `portaria/`
- `limpeza_e_conservacao/`
- `supervisao_operacional/`

## Catálogo inteligente
O arquivo `catalogo.json` consolida todas as fotografias oficiais do banco de imagens e deve ser usado pelo Designer e pelo n8n para localizar a foto mais adequada de cada campanha.

Cada fotografia possui um arquivo `.json` de metadados na mesma pasta da categoria. Esses metadados registram serviço, ambiente, atividade, equipamentos, uniforme, orientação, qualidade, palavras-chave, possíveis usos e restrições.

## Uso obrigatório pelo Designer
Antes de criar qualquer arte, o Designer deve consultar `catalogo.json`, localizar fotografias compatíveis com a campanha e priorizar fotografias reais da Serviscon.

## Regra de uso
Sempre que existir fotografia real compatível com o serviço divulgado, a campanha deve usar `tipo_operacao = gerar_com_imagem_de_referencia`.

Usar `gerar_sem_imagem_de_referencia` apenas quando não houver foto compatível, quando a campanha for abstrata, quando for conceitual sem colaboradores ou quando houver autorização explícita no briefing.

## Como o n8n usa as fotos
O n8n deve obter os caminhos em `imagem.fotos_referencia[].arquivo`, baixar os arquivos reais no GitHub e enviá-los à OpenAI junto com `imagem.prompt_geracao` e as restrições visuais.
