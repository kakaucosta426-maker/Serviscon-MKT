# Guia de Integração n8n + OpenAI para Artes da Serviscon

## Objetivo
Este guia documenta o fluxo oficial para transformar pedidos de arte criados pelo Designer em imagens editadas por automação externa, usando n8n e API da OpenAI.

Nenhuma imagem deve ser gerada diretamente dentro deste repositório. O repositório prepara dados, metadados, prompts e pedidos JSON para que o n8n execute o processamento.

## Fluxo oficial

1. Analista
2. Estrategista
3. Copywriter
4. Designer
5. Consulta `03_base_de_conhecimento/banco_de_imagens/catalogo.json`
6. Escolha da fotografia real mais compatível
7. Criação do pedido JSON em `04_pedidos_de_arte/pendentes/`
8. GitHub
9. n8n
10. Download da fotografia indicada em `foto.arquivo`
11. Envio da fotografia e do prompt para a OpenAI
12. Edição da fotografia
13. GitHub
14. Salvamento do resultado em `05_producao/design/artes_geradas/`

## Banco de imagens inteligente

O banco oficial de imagens fica em:

`03_base_de_conhecimento/banco_de_imagens/`

Todas as fotografias catalogadas representam colaboradores reais da Serviscon e devem ser priorizadas em campanhas compatíveis com o serviço divulgado.

Cada fotografia possui um arquivo JSON de metadados na mesma categoria da imagem. O catálogo geral fica em:

`03_base_de_conhecimento/banco_de_imagens/catalogo.json`

## Como o Designer escolhe a foto

Antes de criar qualquer pedido de arte, o Designer deve:

1. Ler o briefing e a copy da campanha.
2. Identificar o serviço divulgado.
3. Pesquisar `catalogo.json` por `servico`, `categoria`, `atividade`, `ambiente`, `palavras_chave`, `orientacao` e `possiveis_utilizacoes`.
4. Listar as fotografias compatíveis.
5. Escolher a melhor foto considerando serviço, ambiente, atividade, enquadramento, iluminação, qualidade, composição e formato da peça.
6. Usar a fotografia real sempre que existir compatibilidade.

## Regra obrigatória

Sempre que existir fotografia real compatível, o pedido deve usar:

```json
{
  "tipo_operacao": "editar_imagem"
}
```

Quando houver fotografia compatível, é proibido gerar pessoas por IA.

## Quando usar gerar_imagem

Usar:

```json
{
  "tipo_operacao": "gerar_imagem"
}
```

somente quando:

- não existir fotografia adequada;
- a campanha for institucional abstrata;
- a campanha for conceitual;
- houver autorização explícita no briefing.

## Pedido JSON para o n8n

O Designer deve criar um arquivo JSON em `04_pedidos_de_arte/pendentes/` com a fotografia escolhida e o prompt de edição.

Estrutura mínima esperada para o n8n:

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

## Como o n8n encontra a foto

A automação deve ler o arquivo JSON pendente e usar:

`foto.arquivo`

para localizar a fotografia real no repositório.

Em seguida, o n8n deve:

1. Mover o pedido de `pendentes/` para `processando/`.
2. Baixar a fotografia indicada em `foto.arquivo`.
3. Enviar a fotografia real para a OpenAI.
4. Enviar também `prompt_imagem`.
5. Receber a imagem editada.
6. Salvar o arquivo final no caminho indicado em `saida`.
7. Mover o pedido para `concluidos/` em caso de sucesso ou para `erros/` se houver falha.

## O que a OpenAI pode fazer

A fotografia real deve permanecer como imagem principal.

A OpenAI pode:

- melhorar iluminação;
- melhorar resolução;
- trocar ou melhorar o fundo;
- ampliar cenário;
- criar composição publicitária;
- inserir elementos gráficos;
- harmonizar cores;
- criar espaço para títulos;
- criar espaço para CTA;
- melhorar qualidade geral.

## Proibições

A OpenAI não deve:

- trocar o colaborador;
- alterar rosto;
- alterar identidade;
- trocar uniforme;
- substituir equipamentos reais;
- inventar pessoas;
- inventar clientes;
- inventar resultados;
- inserir selos, certificações ou prêmios não confirmados.

## Saída final

Todas as artes geradas ou editadas pela automação devem ser salvas em:

`05_producao/design/artes_geradas/`

As imagens finais ainda devem passar por revisão e aprovação antes de publicação no Instagram.
