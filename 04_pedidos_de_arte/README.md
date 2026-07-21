# Pedidos de Arte para Automação

Esta pasta organiza os pedidos de geração ou edição de imagens que serão processados por uma automação externa, como n8n integrado à API da OpenAI.

## Fluxo de pastas

- `pendentes/`: todo novo pedido de arte deve ser salvo inicialmente nesta pasta.
- `processando/`: pedidos movidos pela automação enquanto estiverem em execução.
- `concluidos/`: pedidos finalizados com sucesso após geração ou edição da imagem.
- `erros/`: pedidos que falharam, precisam de correção ou retornaram erro no processamento.

## Regra principal

Cada pedido deve ser um arquivo JSON individual salvo primeiro em `04_pedidos_de_arte/pendentes/`.

A automação deve ler os arquivos pendentes, mover cada pedido para `processando/`, gerar ou editar a imagem conforme o JSON, salvar o resultado em `05_producao/design/artes_geradas/` e, ao final, mover o pedido para `concluidos/` ou `erros/`.

## Tipos de operação

- `editar_imagem`: usar quando existir uma fotografia real da Serviscon adequada ao serviço anunciado.
- `gerar_imagem`: usar somente quando não existir fotografia real adequada no banco oficial de imagens ou quando a imagem precisar ser criada integralmente por IA.

## Formato obrigatório do JSON

```json
{
  "id": "identificador-unico",
  "status": "pendente",
  "campanha": "nome da campanha",
  "servico": "serviço divulgado",
  "tipo_operacao": "editar_imagem",
  "formato": "1080x1350",
  "foto_origem": "caminho da fotografia real no repositório",
  "prompt": "instrução completa criada pelo Designer",
  "texto_principal": "texto da arte",
  "texto_apoio": "texto secundário",
  "cta": "chamada para ação",
  "pasta_saida": "05_producao/design/artes_geradas",
  "nome_arquivo_saida": "nome-da-arte.png"
}
```

## Exemplo fictício de pedido

> Este exemplo é apenas referência de estrutura. Não deve ser processado como pedido real enquanto estiver somente neste README.

```json
{
  "id": "exemplo-serviscon-limpeza-2026-08-001",
  "status": "pendente",
  "campanha": "Autoridade em limpeza profissional",
  "servico": "limpeza e conservação",
  "tipo_operacao": "editar_imagem",
  "formato": "1080x1350",
  "foto_origem": "03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.jpg",
  "prompt": "Editar a fotografia real mantendo o colaborador, uniforme, equipamento profissional e ambiente original. Aplicar tratamento publicitário premium com correção de luz, contraste limpo, valorização do azul institucional da Serviscon, aparência corporativa moderna, alta nitidez, fundo organizado e espaço negativo no topo para título. Não alterar o serviço executado, não trocar uniforme, não adicionar clientes, não inserir selos ou informações não confirmadas.",
  "texto_principal": "Limpeza profissional muda a rotina da empresa.",
  "texto_apoio": "Equipe treinada, equipamento adequado e acompanhamento da qualidade.",
  "cta": "Fale com a Serviscon.",
  "pasta_saida": "05_producao/design/artes_geradas",
  "nome_arquivo_saida": "exemplo-limpeza-profissional.png"
}
```

## Cuidados para automação

- Não sobrescrever pedidos existentes.
- Validar se o `id` é único antes de iniciar o processamento.
- Validar se `foto_origem` existe quando `tipo_operacao` for `editar_imagem`.
- Validar se `pasta_saida` aponta para `05_producao/design/artes_geradas`.
- Não publicar nem agendar imagens automaticamente; o resultado deve passar por aprovação antes do uso no Instagram.

## Pedido inteligente com fotografia real
Para integração com o catálogo inteligente, o pedido também deve conter o objeto `foto`, permitindo que o n8n localize automaticamente a fotografia por `foto.arquivo`.

```json
{
  "id": "pedido-unico",
  "status": "pendente",
  "campanha": "nome da campanha",
  "servico": "serviço divulgado",
  "tipo_operacao": "editar_imagem",
  "formato": "1080x1350",
  "foto": {
    "id": "LIMP-001",
    "arquivo": "03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.jpg",
    "metadados": "03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.json"
  },
  "prompt_imagem": "prompt completo criado pelo Designer",
  "texto_principal": "texto da arte",
  "texto_apoio": "texto secundário",
  "cta": "chamada para ação",
  "saida": "05_producao/design/artes_geradas/arte_limpeza_001.png"
}
```

O campo `foto.arquivo` é a referência operacional que o n8n deve usar para baixar a fotografia real e enviá-la à OpenAI junto com `prompt_imagem`.
