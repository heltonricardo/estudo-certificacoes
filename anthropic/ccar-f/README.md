# CCAR-F: Anthropic Claude Certified Architect – Foundations

[Voltar para a página principal](../../README.md)

<img src="assets/badge.png" alt="CCAR-F: Anthropic Claude Certified Architect – Foundations" width="200"/>

## 1. Modos de execução (Claude Code)

Claude Code tem modos que controlam quanto ele pode fazer sem pedir aprovação. A escolha certa depende de quão ambígua/arriscada é a tarefa.

- **Plan mode**: Claude só planeja primeiro, sem tocar em arquivos. Você aprova o plano inteiro de uma vez; depois disso ele **executa todas as edições em sequência, sem pedir aprovação por edição**. Usar quando há múltiplas abordagens válidas e mudança ampla.
- **Default (Manual)**: cada edição individual pede aprovação separada, mesmo sem plan mode antes.
- **Accept edits**: edita direto, sem aprovação por edição — pra iteração rápida em mudanças pequenas e já entendidas.
- Regra geral: pra impedir edição de fato, use a ferramenta de permissão (plan mode / hook), não confie só numa instrução em prompt.

## 2. Subagents — delegação

Um subagent é um "sub-Claude" especializado que o agente principal (coordinator) pode chamar pra executar uma subtarefa isoladamente. O coordinator decide **se** delega olhando o campo `description` da definição do subagent.

- **Description** vaga ("Helper agent") = coordinator não sabe quando usar, então resolve sozinho. Description boa nomeia situações específicas de uso + diz pra usar proativamente.
- **Contexto da tarefa** (arquivos já lidos, achados anteriores) vai no **prompt de delegação** no momento da chamada, não no description — description só afeta _se_ é chamado, não _o que_ ele recebe.
- Restringir tools de um subagent: usar o **tools field/allowlist** na definição, não confiar em instrução de prompt.
- Subtarefas independentes → disparar todos os Task/Agent calls **no mesmo turno** (paralelo). Sequencial só quando uma depende do resultado da outra.

## 3. Ferramentas MCP / erro handling

MCP (Model Context Protocol) é o protocolo que conecta Claude a ferramentas externas (bancos de dados, APIs, sistemas internos). Quando uma tool MCP falha, como ela comunica o erro afeta se o agente consegue se recuperar direito.

- Erro de **protocolo** (schema inválido, tool inexistente, permissão negada) → JSON-RPC error.
- Erro de **execução da tool** (documento indisponível, timeout) → `CallToolResult` com `isError:true`.
- Mensagem genérica ("Operation failed") pra todo tipo de falha = agente não sabe se deve tentar de novo ou desistir. Corrigir com mensagem específica + metadata (categoria, flag "pode tentar de novo").
- Nunca disfarçar erro como sucesso (ex: array vazio em vez de erro) — causa decisão errada silenciosa.
- Busca sem resultado (zero matches legítimo) não é erro — não usar `isError:true` pra isso.

## 4. Contexto e degradação em sessões longas

Toda conversa tem um limite de contexto. Em sessões longas, informação antiga vai sendo resumida/perdida, e o agente começa a "alucinar padrões genéricos" em vez de citar o que realmente encontrou.

- Sintoma: respostas viram "padrões típicos" em vez de fatos específicos, contradizem o que foi dito antes.
- Soluções: extrair fatos críticos (valores, IDs, decisões) num bloco sempre incluído no prompt e excluído da sumarização; delegar exploração pra um subagent que devolve só a conclusão; `/compact` pra condensar histórico; salvar achados confirmados num arquivo e reler antes de continuar.
- Errado: só sumarizar mais agressivamente sem proteger os fatos-chave.

## 5. Hooks

Hook é um script/callback que roda automaticamente em pontos específicos do ciclo de vida de uma tool call (antes, depois, etc.), permitindo interceptar, bloquear ou modificar comportamento de forma determinística — diferente de uma instrução em prompt, que o modelo pode ignorar.

- **PreToolUse**: roda antes da tool executar — único ponto que realmente **bloqueia** a execução.
- **PostToolUse**: roda depois — só reage ao que já aconteceu, não impede.
- Bloquear de fato: `permissionDecision: deny` (SDK) ou **exit code 2** no script (exit code 1 só loga, não bloqueia).
- Hook casa pelo **nome da tool** (matcher, ex: "Write|Edit"), não por path — pra restringir por path, checar `tool_input.file_path` dentro do próprio callback.
- Regra não-negociável (ex: aprovação humana antes de ação irreversível) → hook, nunca só instrução de prompt.

## 6. CLAUDE.md / hierarquia de memória

CLAUDE.md é o arquivo de instruções persistentes que Claude Code carrega automaticamente no início da sessão. Existe em vários níveis, e o nível certo depende de quem deve receber a instrução.

- **Root CLAUDE.md** (versionado): convenções que todo o time precisa, sempre.
- **~/.claude/CLAUDE.md** (nível usuário): preferências pessoais, não compartilhadas.
- **CLAUDE.local.md** (gitignored): específico do dev, não versionado.
- Conflito entre CLAUDE.md pai/filho: resolver reescrevendo a regra raiz pra excluir a exceção explicitamente — não confiar que o arquivo filho "vence" sozinho.
- `@import`: usado pra apontar de um arquivo pessoal pra um arquivo compartilhado do repo.
- Arquivo gigante sempre carregado, mas só parte é relevante por sessão → mover conteúdo pra `.claude/rules/*.md` com frontmatter `paths:` (carrega só quando arquivo relevante está em jogo).

## 7. Skills

Skill é um arquivo `SKILL.md` que empacota um procedimento reutilizável — instruções, e opcionalmente templates/scripts — que vira um comando (`/nome`) ou que o próprio Claude pode acionar automaticamente quando pertinente.

- `.claude/skills/nome/SKILL.md` = skill de projeto (versionada).
- **Shadowing**: skill de mesmo nome em `~/.claude/skills/` (usuário) sobrepõe a do projeto — remover/renomear a pessoal resolve.
- `user-invocable: true` + `name:` no frontmatter → necessário pra aparecer como slash command.
- `disable-model-invocation: true` → fica no menu, mas só humano aciona, nunca o próprio Claude sozinho.
- `context: fork` → roda em subagent isolado e devolve só a conclusão pra sessão principal (evita poluir contexto com logs de execução).

## 8. Frontmatter

Frontmatter é o bloco de metadados em YAML no topo de um arquivo Markdown (entre `---`), separado do conteúdo. É onde ficam as configurações que o Claude Code lê programaticamente (nome do comando, paths de aplicação, etc.), sem misturar com o texto da instrução em si.

```
---
name: docgen
paths: ["**/*.test.ts"]
---
```

## 9. Registro de MCP servers

Antes de usar uma tool MCP, o servidor precisa ser registrado em algum escopo. O escopo certo depende de se a configuração deve ser compartilhada com o time ou não.

- **Project scope** (`.mcp.json`, commitado): todo dev recebe ao clonar; usar pra servers sem segredo.
- **User scope** (`~/.claude.json`): usar quando precisa de token/credencial — nunca commitar segredo em `.mcp.json`.
- Se o time atualizou `.mcp.json` mas um dev já tinha registrado o mesmo nome em local scope antes → `claude mcp reset-project-choices` força reprompt.
- Entrada remota só com `url` e sem tipo de transporte definido = mal configurada; stdio precisa de `command`.

## 10. Structured Outputs / Tool Use

Structured output é quando você força o modelo a responder num formato específico (JSON validado por schema) em vez de texto livre, geralmente via tool use.

- `strict: true` garante schema/sintaxe válida, **não impede fabricação semântica** (inventar data/nome plausível pra campo vazio). Corrigir com instrução explícita: "nunca adivinhe, só reporte o que está na fonte".
- `tool_choice: {"type": "any"}` força usar alguma tool (evita resposta em prosa), mas não resolve escolher a tool errada — isso é papel de description + exemplos.
- `tool_choice` forçando uma tool específica só faz sentido quando só existe uma tool possível pra aquele call.
- JSON cortado por `stop_reason: max_tokens` → tratar como truncamento (aumentar limite/continuar geração), não só instruir "sempre gere JSON válido".
- `stop_reason: refusal` → tratar como caminho separado, não reenviar como erro de parse.
- Enum muito restrito (só 4 categorias, aparece uma 5ª) → adicionar valor "other" + campo de detalhe livre.
- Campo ambíguo (`invoice_date` sem formato) → **renomear o campo** pra especificar formato (`invoice_date_iso8601`) costuma ser mais eficaz que só description.

## 11. Validação / Retry loops

Quando a resposta do modelo falha na validação (schema ou regra de negócio), o loop de retry reenvia a requisição — mas o que você reenvia importa.

- Retry deve incluir **doc original + output rejeitado + erro específico do validador**, não só repetir o pedido igual.
- Verificação semântica (ex: trecho citado não existe de fato na fonte) exige checagem programática separada — schema validation sozinho não pega isso.

## 12. Revisão / Confiabilidade (self-review vs independente)

Adicionar uma etapa de revisão automática só funciona se o revisor for de fato independente — senão vira teatro.

- Self-review na **mesma sessão/conversa** tende a aprovar a própria decisão (viés) — não pega erro real.
- Corrigir com subagent/instância independente de contexto fresco, ou extended thinking no passo de revisão.
- Reviewer com contexto amplo (histórico de raciocínio) não ajuda se o erro é simples de checar direto contra o documento-fonte.
- Cobertura inconsistente entre passadas de revisão → reviewer reportar confidence score por categoria e re-rodar categorias abaixo do threshold.

## 13. Sampling / redução de revisão humana

Quando o time quer reduzir quanto um humano revisa manualmente, a métrica usada pra decidir isso importa muito.

- Nunca usar accuracy **agregada** (ex: "96% geral") pra reduzir revisão uniformemente — accuracy varia por segmento (tópico raro vs comum).
- Certo: confidence score **calibrado contra validation set rotulado** + amostragem estratificada.

## 14. Escalonamento / Critérios ambíguos

Escalonamento é quando o agente decide passar o caso pra um humano em vez de resolver sozinho. A qualidade dessa decisão depende de quão específico é o critério.

- Linguagem vaga ("escalone quando parecer complexo") = comportamento inconsistente.
- Certo: condições explícitas e mensuráveis (cliente pediu humano / fora da política documentada / sem progresso após N tool calls) + few-shot pra calibrar casos ambíguos.

## 15. Handoff / Sumários de escalonamento

Quando um caso é escalado, o humano que recebe precisa saber o que é fato verificado (veio de tool result) e o que é só o que o cliente disse (não verificado).

- Corrigir exigindo que o agente **atribua a fonte de cada afirmação** no resumo — não basta pedir "resumo mais limpo" sem essa distinção.

## 16. Decomposição de tarefas

Decidir como quebrar uma tarefa grande em partes (sequencial, paralela, ou "descobrir durante o caminho") depende do que já se sabe antes de começar.

- Conhecimento desconhecido a priori (só se descobre investigando) → decomposição **dinâmica/adaptativa**, não fixa de antemão.
- Passos sequenciais dependentes → ordem fixa, sem etapa de "entrevista" desnecessária.
- Subtarefas paralelas independentes → subagents disparados no mesmo turno.

## 17. Few-shot examples

Few-shot é dar exemplos concretos dentro do prompt pra guiar o formato/estilo da resposta. Ajuda muito, mas tem armadilhas.

- Poucos exemplos do **mesmo tipo** → overfitting (aplica o padrão errado a casos diferentes). Corrigir com exemplos diversos, não só "mais exemplos iguais".
- Exemplos com dados reais (nomes, IDs) colados no prompt podem **vazar pra produção** — o modelo reusa esses dados em respostas reais. Corrigir removendo dados sensíveis dos exemplos, não removendo os exemplos inteiros.
- Instrução nova conflita com exemplos antigos que não a seguem → exemplos pesam mais que prosa; atualizar os exemplos.

## 18. Batches API

A Message Batches API processa muitas requisições de forma assíncrona e mais barata, mas sem garantia de resposta rápida — não serve pra tudo.

- Usar só pra trabalho não urgente/não bloqueante (auditoria noturna, reprocessamento em lote). Nunca pra chamada síncrona de cliente.
- Correlacionar resultado por **custom_id**, nunca por posição/ordem de linha.
- `expired` no resultado não é bug de app, é limite de tempo do batch.
- MCP tool calls dentro de batch precisam das definições de tool no request (geralmente `tool_choice: any`); quem executa o client-side tool ainda é a aplicação, depois do batch devolver o tool_use.

## 19. CI/CD (GitHub Actions / claude -p)

Rodar Claude Code de forma automatizada (sem humano no terminal) em pipeline exige configuração específica de permissões e trigger.

- `claude-code-action@v1` sem prompt input = modo "tag" (só dispara com comentário `@claude`). Com prompt input = modo automation (roda em todo evento).
- `pull_request` trigger só dispara pra quem tem write access por padrão — usar `allowed_non_write_users` ou `schedule` pra bots/PRs externos.
- Erro "could not obtain GitHub App token" com API key válida → falta `actions: read` no permissions block.
- Commits do Claude não disparam CI checks → falta `id-token: write` no permissions block.
- Múltiplos passos headless no mesmo runner → `--continue` retoma a sessão mais recente.

## 20. Gestão de sessão / continuidade

Uma sessão do Claude Code/Agent SDK pode ser retomada depois. A forma certa de retomar depende do que mudou desde então e se você quer preservar ou ramificar o histórico.

- Trabalho anterior + arquivos que mudaram desde então → **não** dar resume cego; iniciar sessão nova com resumo estruturado do que foi achado + nota do que mudou, pra reverificação.
- Comparar duas estratégias a partir do mesmo ponto sem uma influenciar a outra → **fork** (baseline intacto, cada branch com histórico próprio).
- Sistema distribuído (containers autoscaled) → **SessionStore** compartilhado, não depender de arquivo local.
- Múltiplos usuários concorrentes no mesmo processo → capturar session ID e usar `fork` em cada follow-up, não sessão compartilhada.

## 21. Bash / execução de comando

Cada chamada da tool Bash roda num shell novo e isolado.

- Variável de ambiente definida numa call **não persiste** pra próxima call — rodar no mesmo comando ou usar arquivo pra estado.
- Tools nativas (Read/Grep) rodam concorrentes num turno; tools MCP customizadas podem não ter esse paralelismo nativamente.

## 22. Edit tool — old_string não único

A tool Edit exige que o texto a ser substituído (`old_string`) seja único no arquivo, senão falha.

- Erro "matches multiple locations" → expandir `old_string` com linhas de contexto até ficar único.
- Se não dá pra tornar único de forma prática → usar **Write** pra sobrescrever o arquivo inteiro com o conteúdo final desejado (só se Claude já leu o arquivo antes).

## 23. Grep vs Bash grep

Grep (tool nativa) e grep via Bash (shell) têm outputs diferentes.

- Grep nativo às vezes retorna só os paths dos arquivos, não a linha do match.
- Se precisa ver a linha real → usar Bash com grep de shell.
- Pra achar arquivos por conteúdo sem carregar tudo: Grep primeiro (paths), Read seletivo depois — nunca Read tudo de uma vez.

## 24. Payloads grandes de tool result

Tool MCP que retorna dezenas de campos, mas só alguns são usados, enche o contexto à toa.

- Corrigir filtrando/reduzindo o payload **antes** de entrar no contexto (ex: hook PostToolUse), não aumentando limite de contexto.

## 25. Timestamps inconsistentes entre tools

Fontes diferentes de dados retornam datas em formatos diferentes (epoch, string livre, ISO), causando erro de ordenação cronológica.

- Corrigir normalizando via **hook (PostToolUse)** pra ISO 8601 antes de entrar no contexto — não confiar que o modelo normaliza sozinho.

## 26. Padrões "errados" recorrentes (pegadinhas comuns nas opções)

Lista de respostas que aparecem como distratores frequentes nas questões — geralmente parecem razoáveis mas não resolvem a causa raiz:

- Aumentar `max_turns` quando o problema real é falta de contexto/paralelismo.
- "Mais exemplos do mesmo padrão" quando falta é diversidade de exemplos.
- Resolver tool routing só com nome mais longo, sem mudar description/boundary.
- Jogar tudo numa única call/contexto grande quando o certo é decompor.
- Self-review na mesma sessão como alternativa a revisor independente — quase sempre errado.
- Accuracy agregada como justificativa pra reduzir revisão — quase sempre errado.

[Voltar para a página principal](../../README.md)
