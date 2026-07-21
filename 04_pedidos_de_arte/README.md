# Pedidos de Arte para Automação

Esta pasta organiza os pedidos JSON que conectam Codex, GitHub, n8n e OpenAI.

O Codex não realiza chamadas HTTP, não chama Webhooks e não utiliza diretamente a API da OpenAI. A comunicação com o n8n acontece exclusivamente pela criação de arquivos JSON no GitHub.

## Estrutura de pastas

```text
04_pedidos_de_arte/
├── pendentes/
├── processando/
├── concluidos/
└── erros/
```

## Regra de criação

Cada nova arte deve gerar um arquivo JSON dentro de:

`04_pedidos_de_arte/pendentes/`

Padrão de nome obrigatório:

`pedido_YYYYMMDD_HHMMSS_nome-da-campanha.json`

Exemplo:

`pedido_20260721_143000_limpeza-profissional.json`

## Tipos de operação

- `gerar_com_imagem_de_referencia`: usar quando uma ou mais fotografias reais da Serviscon serão enviadas à OpenAI como base visual da nova arte.
- `gerar_sem_imagem_de_referencia`: usar somente quando não houver fotografia compatível, quando a campanha for abstrata, quando for conceitual sem colaboradores ou quando houver autorização explícita no briefing.

O padrão para campanhas operacionais da Serviscon é `gerar_com_imagem_de_referencia`.

## Estrutura obrigatória do JSON

```json
{
  "id": "ARTE-20260721-001",
  "status": "pendente",
  "data_criacao": "2026-07-21T00:00:00-03:00",
  "campanha": {
    "nome": "Campanha de limpeza profissional",
    "objetivo": "Apresentar limpeza e conservação como serviço principal da Serviscon",
    "servico": "Limpeza e conservação",
    "publico": "Empresários, síndicos, administradores e gestores",
    "canal": "Instagram"
  },
  "copy": {
    "titulo": "Limpeza profissional muda a rotina da empresa.",
    "texto_apoio": "Equipe treinada, equipamento adequado e acompanhamento da qualidade.",
    "cta": "Fale com a Serviscon.",
    "legenda": "Limpeza e conservação profissional são o principal serviço da Serviscon, com equipe treinada, equipamentos adequados e supervisão.",
    "hashtags": ["#Serviscon", "#LimpezaProfissional", "#Facilities"]
  },
  "design": {
    "formato": "1080x1350",
    "tipo_peca": "feed_instagram",
    "conceito_visual": "Arte corporativa premium usando fotografia real de colaborador da Serviscon em operação de limpeza mecanizada.",
    "hierarquia_visual": ["foto real como base", "titulo no topo", "texto de apoio no meio", "cta no rodapé"],
    "cores": ["#061F49", "#10AEE0", "#FFFFFF"],
    "observacoes": "Manter identidade visual limpa, moderna e com alto contraste."
  },
  "imagem": {
    "tipo_operacao": "gerar_com_imagem_de_referencia",
    "fotos_referencia": [
      {
        "id": "LIMP-001",
        "arquivo": "03_base_de_conhecimento/banco_de_imagens/limpeza_e_conservacao/serviscon_limpeza_001.jpg",
        "categoria": "limpeza_e_conservacao",
        "descricao": "Colaborador da Serviscon conduz máquina de limpeza de piso em corredor interno com sinalização de segurança",
        "funcao_na_composicao": "imagem_principal"
      }
    ],
    "prompt_geracao": "Utilize a fotografia real anexada do colaborador da Serviscon como elemento principal. Preserve integralmente o rosto, a identidade, o uniforme, a logomarca no uniforme e os equipamentos. Crie ao redor da fotografia uma composição publicitária corporativa, moderna e realista sobre terceirização de limpeza profissional. Integre o colaborador naturalmente ao novo cenário, sem substituí-lo por uma pessoa gerada por IA. Utilize azul-marinho, azul-claro e branco da identidade visual da Serviscon. Reserve área limpa no topo para o título e espaço discreto na parte inferior para o CTA.",
    "restricoes": [
      "Preservar o rosto e a identidade do colaborador",
      "Preservar o uniforme da Serviscon",
      "Não substituir o colaborador por pessoa gerada por IA",
      "Não alterar a logomarca presente no uniforme",
      "Não deformar mãos, rosto ou corpo",
      "Manter aparência fotográfica realista"
    ],
    "arquivo_saida": "05_producao/design/artes_geradas/arte_limpeza_001.png"
  },
  "social_media": {
    "plataforma": "Instagram",
    "data_sugerida": "2026-08-05",
    "objetivo_publicacao": "Apresentar serviço principal e gerar interesse comercial"
  }
}
```

## Como o n8n usa o pedido

O n8n deve:

1. Detectar um novo JSON em `pendentes/`.
2. Ler o pedido.
3. Usar `imagem.fotos_referencia[].arquivo` para baixar as fotografias reais no GitHub.
4. Enviar as imagens reais, `imagem.prompt_geracao`, formato e restrições para a OpenAI.
5. Salvar o arquivo final em `imagem.arquivo_saida`.
6. Atualizar o status e mover o pedido para `concluidos/` ou `erros/`.

## Segurança

Não armazenar neste repositório chaves da OpenAI, tokens do GitHub, credenciais do n8n, senhas ou dados de autenticação.
