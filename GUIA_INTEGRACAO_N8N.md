# Guia de Integração n8n + OpenAI para Artes da Serviscon

## Objetivo
Finalizar a arquitetura de produção automática da agência de marketing da Serviscon usando Codex, GitHub, n8n e OpenAI.

O Codex prepara pedidos JSON no GitHub. O Codex não realiza chamadas HTTP, não chama Webhooks, não utiliza diretamente a API da OpenAI e não gera imagens durante a preparação da arquitetura.

## Fluxo oficial

1. Usuário solicita a campanha.
2. Analista cria o diagnóstico.
3. Estrategista define a campanha.
4. Copywriter cria os textos.
5. Designer define a composição visual.
6. Designer consulta `03_base_de_conhecimento/banco_de_imagens/catalogo.json`.
7. Designer escolhe a fotografia real mais adequada.
8. Codex cria o pedido JSON em `04_pedidos_de_arte/pendentes/`.
9. n8n detecta o novo pedido.
10. n8n baixa a fotografia real.
11. n8n envia fotografia + prompt para a OpenAI.
12. OpenAI gera uma nova arte utilizando a fotografia como base.
13. n8n salva a arte final no GitHub.
14. Social Media prepara a publicação.

## Estrutura dos pedidos

Garantir a existência de:

```text
04_pedidos_de_arte/
├── pendentes/
├── processando/
├── concluidos/
└── erros/
```

Cada nova arte deve gerar um arquivo JSON dentro de `04_pedidos_de_arte/pendentes/`.

Padrão de nome:

`pedido_YYYYMMDD_HHMMSS_nome-da-campanha.json`

## Banco de imagens oficial

Considerar como banco oficial:

`03_base_de_conhecimento/banco_de_imagens/`

O Designer deve consultar:

`03_base_de_conhecimento/banco_de_imagens/catalogo.json`

antes de criar qualquer pedido de imagem.

O banco contém fotografias reais de colaboradores, equipes, uniformes, equipamentos, atividades operacionais, ambientes e serviços executados pela Serviscon.

## Responsabilidade do Designer

Para cada arte, o Designer deve:

1. Ler o briefing da campanha.
2. Identificar serviço, público, objetivo e formato da peça.
3. Consultar `catalogo.json`.
4. Localizar fotografias compatíveis com o tema.
5. Selecionar a fotografia real mais adequada.
6. Definir como a fotografia será usada na composição.
7. Criar um prompt detalhado para a OpenAI.
8. Criar o pedido JSON em `04_pedidos_de_arte/pendentes/`.

O Designer não gera a imagem diretamente.

## Regra visual obrigatória

Quando a campanha representar uma atividade real da Serviscon, a OpenAI deve gerar a arte usando uma ou mais fotografias reais do banco de imagens.

A fotografia não é apenas inspiração textual. O arquivo real deve ser baixado pelo n8n e enviado à OpenAI como imagem de entrada.

A nova arte pode incluir novo enquadramento, expansão de cenário, fundo publicitário, recorte do colaborador, elementos gráficos, iluminação profissional, profundidade, tratamento de imagem, composição com identidade visual, áreas livres para título e CTA, integração de mais de uma fotografia quando tecnicamente possível e adaptação para formatos de redes sociais.

## Preservação da imagem real

Ao usar fotografia do banco, preservar:

- identidade do colaborador;
- rosto;
- características físicas;
- uniforme;
- logomarca presente no uniforme;
- equipamentos reais;
- atividade representada;
- identidade institucional da Serviscon.

A IA não pode trocar colaborador, criar outro rosto, modificar características faciais, alterar cor ou modelo do uniforme sem autorização, deformar mãos ou corpo, inserir logomarcas incorretas, inventar equipamentos incompatíveis, descaracterizar a atividade ou gerar colaboradores fictícios quando houver fotos reais adequadas.

## Tipos de geração

### `gerar_com_imagem_de_referencia`
Usar quando uma fotografia real será enviada à OpenAI como base para a criação da nova arte.

Este é o padrão para campanhas operacionais da Serviscon.

### `gerar_sem_imagem_de_referencia`
Usar somente quando:

- não houver fotografia compatível;
- a campanha for totalmente abstrata;
- a campanha for conceitual e não representar colaboradores;
- houver autorização explícita no briefing.

## Estrutura do JSON

Cada pedido deve seguir esta estrutura:

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

## Prompt de geração

O campo `prompt_geracao` deve descrever qual fotografia será utilizada, quem ou o que aparece na fotografia, o que deve ser preservado, objetivo da campanha, cenário desejado, composição, enquadramento, iluminação, elementos gráficos, identidade visual da Serviscon, localização do título, localização do CTA, proporção, tamanho, aparência final e elementos que não podem ser alterados.

## Papel do n8n

O n8n deve identificar novos arquivos em `04_pedidos_de_arte/pendentes/`.

Ao encontrar um novo pedido, deve:

1. Ler o JSON.
2. Alterar `status` para `processando`.
3. Obter cada caminho em `imagem.fotos_referencia[].arquivo`.
4. Baixar os arquivos reais do banco de imagens no GitHub.
5. Converter os arquivos para o formato aceito pela integração da OpenAI, quando necessário.
6. Enviar para a OpenAI as fotografias reais, `prompt_geracao`, formato da arte e restrições visuais.
7. Solicitar a geração de uma nova arte usando as fotografias como base visual.
8. Receber a arte final gerada.
9. Salvar a arte em `imagem.arquivo_saida`.
10. Atualizar o JSON com `status`, `arquivo_final`, `data_processamento` e `fotos_utilizadas`.
11. Mover o pedido para `04_pedidos_de_arte/concluidos/`.

## Tratamento de erros

Caso a geração não seja concluída:

1. Não apagar o pedido.
2. Alterar `status` para `erro`.
3. Registrar `mensagem_erro`, `etapa_erro`, `data_erro` e `tentativas`.
4. Mover o arquivo para `04_pedidos_de_arte/erros/`.
5. Permitir que o pedido seja corrigido e reenviado.

## Responsabilidade do Social Media

O Social Media deve utilizar apenas pedidos com `status = concluido`.

Ele deve receber arquivo final da arte, título, texto de apoio, CTA, legenda, hashtags, plataforma e objetivo da publicação.

O Social Media não deve publicar ou considerar concluída uma campanha enquanto a arte final não estiver disponível no GitHub.

## Segurança

Nunca armazenar no repositório chave da OpenAI, token do GitHub, credenciais do n8n, senhas ou dados de autenticação.

Toda autenticação deve permanecer exclusivamente nas credenciais protegidas do n8n.

## Configuração manual necessária no n8n

Ainda será necessário configurar manualmente no n8n:

- credenciais do GitHub;
- credenciais da OpenAI;
- gatilho para detectar novos JSONs em `04_pedidos_de_arte/pendentes/`;
- leitura e validação do JSON;
- download de `imagem.fotos_referencia[].arquivo`;
- chamada ao recurso de geração/edição de imagem da OpenAI;
- upload do arquivo final para `05_producao/design/artes_geradas/`;
- atualização de status do pedido;
- movimentação para `concluidos/` ou `erros/`;
- notificações internas, se desejado.
