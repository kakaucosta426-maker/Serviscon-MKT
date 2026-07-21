# Serviscon MKT — Arquitetura de Produção Automática

Este repositório organiza a operação de marketing para o Instagram da Serviscon e prepara a produção automática de artes usando Codex, GitHub, n8n e OpenAI.

## Princípio central

A produção deve usar informações reais da Serviscon. Não inventar clientes, resultados, datas, preços, credenciais, pessoas, uniformes, equipamentos ou serviços.

## Fluxo oficial

1. Usuário solicita a campanha.
2. Analista cria o diagnóstico.
3. Estrategista define a campanha.
4. Copywriter cria os textos.
5. Designer define a composição visual.
6. Designer consulta `03_base_de_conhecimento/banco_de_imagens/catalogo.json`.
7. Designer escolhe a fotografia real mais adequada.
8. Codex cria o pedido JSON em `04_pedidos_de_arte/pendentes/`.
9. n8n detecta o novo pedido no GitHub.
10. n8n baixa as fotografias reais indicadas em `imagem.fotos_referencia[].arquivo`.
11. n8n envia fotografia + prompt para a OpenAI.
12. OpenAI gera uma nova arte usando a fotografia como base visual.
13. n8n salva a arte final em `05_producao/design/artes_geradas/`.
14. Social Media prepara a publicação após o pedido estar concluído.

## Estrutura principal

```text
01_contexto_do_cliente/
02_planejamento/
03_base_de_conhecimento/
  banco_de_imagens/
    catalogo.json
04_agentes/
04_pedidos_de_arte/
  pendentes/
  processando/
  concluidos/
  erros/
05_producao/
  design/
    artes_geradas/
05_resultados/
```

## Banco de imagens oficial

O banco oficial fica em `03_base_de_conhecimento/banco_de_imagens/`.

Ele contém fotografias reais catalogadas de colaboradores, equipes, uniformes, equipamentos, atividades operacionais, ambientes e serviços executados pela Serviscon.

O Designer deve consultar `catalogo.json` antes de criar qualquer pedido de arte.

## Tipos de geração

- `gerar_com_imagem_de_referencia`: padrão para campanhas operacionais da Serviscon quando houver foto real compatível.
- `gerar_sem_imagem_de_referencia`: permitido apenas quando não houver fotografia compatível, a campanha for abstrata, conceitual sem colaboradores ou houver autorização explícita no briefing.

## Comunicação com n8n

O Codex não chama Webhooks, não faz chamadas HTTP e não usa diretamente a API da OpenAI.

A comunicação com o n8n acontece exclusivamente por arquivos JSON criados em:

`04_pedidos_de_arte/pendentes/`

O n8n deve monitorar essa pasta, processar os pedidos e salvar a arte final no caminho indicado em `imagem.arquivo_saida`.

## Segurança

Nunca armazenar neste repositório chaves da OpenAI, tokens do GitHub, credenciais do n8n, senhas ou dados de autenticação. Toda autenticação deve ficar nas credenciais protegidas do n8n.
