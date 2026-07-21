# AGENTS.md — Agência de Marketing para Instagram

## Escopo
Este repositório organiza o trabalho de uma agência de marketing focada exclusivamente no Instagram de um único cliente.

## Regra principal
Não invente informações sobre o cliente. Sempre use campos claramente identificados como `[PREENCHER]`, `[A DEFINIR]` ou checklists em branco quando um dado ainda não tiver sido fornecido.

## Funções da equipe
A operação deve considerar cinco funções:

1. Analista de Marketing
2. Estrategista de Conteúdo
3. Copywriter
4. Designer
5. Social Media

## Fluxo de trabalho
1. Contexto do cliente
2. Planejamento
3. Produção
4. Aprovação
5. Resultados

## Convenções
- Use Markdown para documentos operacionais.
- Mantenha linguagem clara, objetiva e orientada a preenchimento.
- Não inclua dados fictícios de mercado, persona, métricas, marca, produto ou cliente.
- Todo conteúdo publicado ou planejado deve estar relacionado ao Instagram do cliente.

## Rotina de início de mês
Ao iniciar um novo mês de planejamento, leia `01_contexto_do_cliente/briefing_do_cliente.md` antes de criar ou atualizar `02_planejamento/calendario_editorial.md`.

O calendário editorial mensal deve conter todas as publicações previstas para o mês, incluindo datas sugeridas, formato, tema, objetivo, responsável e status. Não deixe campos em branco; quando uma informação depender de confirmação do cliente, registre a dependência nas observações ou use uma descrição operacional clara, sem inventar dados.

## Fluxo inteligente de imagens
- O banco oficial de imagens fica em `03_base_de_conhecimento/banco_de_imagens/`.
- Todas as fotografias catalogadas representam colaboradores reais da Serviscon e devem ser priorizadas em campanhas compatíveis.
- O catálogo geral para consulta automática é `03_base_de_conhecimento/banco_de_imagens/catalogo.json`.
- Cada fotografia deve ter um JSON de metadados na mesma pasta da imagem.
- O Designer deve consultar `catalogo.json` antes de criar qualquer pedido de arte.
- Sempre que a campanha representar colaboradores, equipes, uniformes, serviços ou ambientes operacionais da Serviscon e existir fotografia compatível, usar `tipo_operacao = gerar_com_imagem_de_referencia`.
- Usar `tipo_operacao = gerar_sem_imagem_de_referencia` somente quando não existir fotografia adequada, quando a campanha for totalmente abstrata, quando for conceitual e não representar colaboradores, ou quando houver autorização explícita no briefing.
- O Designer deve criar pedidos JSON em `04_pedidos_de_arte/pendentes/` e nunca executar geração de imagem diretamente.
- O Codex não deve realizar chamadas HTTP, chamar Webhooks ou usar diretamente a API da OpenAI; a comunicação com o n8n ocorre apenas por arquivos JSON no GitHub.
- O n8n deve usar `imagem.fotos_referencia[].arquivo` para localizar as fotografias reais no repositório e salvar o resultado final em `05_producao/design/artes_geradas/`.

### Fluxo oficial de automação de arte
Usuário solicita a campanha → Analista cria o diagnóstico → Estrategista define a campanha → Copywriter cria os textos → Designer define a composição visual → Designer consulta `catalogo.json` → Designer escolhe a fotografia real mais adequada → Codex cria o pedido JSON no GitHub → n8n detecta o novo pedido → n8n baixa a fotografia real → n8n envia fotografia + prompt para a OpenAI → OpenAI gera nova arte usando a fotografia como base → n8n salva a arte final no GitHub → Social Media prepara a publicação.

## Segurança
Nunca armazenar no repositório:

- chave da OpenAI;
- token do GitHub;
- credenciais do n8n;
- senhas;
- dados de autenticação.

Toda autenticação deve permanecer exclusivamente nas credenciais protegidas do n8n.
