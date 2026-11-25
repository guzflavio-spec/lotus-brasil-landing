# Conversa completa: análise de 2 vídeos e instalação de ferramentas no Claude Code

> Documento feito para ser anexado como conhecimento em um Projeto no Claude.
> Repositório: https://github.com/guzflavio-spec/lotus-brasil-landing (branches `main` e `claude/video-analysis-installation-84vboh`)
> Período: 18/11/2026 a 25/11/2026

---

## 1. Resumo executivo

| Item | Situação |
|---|---|
| Pedido inicial | Analisar 2 vídeos (reels), explicar como funcionam, custos e passo a passo de instalação |
| Vídeo 1 | "5 plugins para o Claude Code parar de ser racionado" |
| Vídeo 2 | "5 configurações para o Claude montar sites mais bonitos" |
| Instalado e enviado ao GitHub | 4 skills, 2 plugins, 2 MCPs, README |
| Não instalado (de propósito) | OmniRoute e Headroom |
| Nome do repositório | Mantido como `lotus-brasil-landing` por decisão do Flavio |
| Pendências | Autenticar o Figma (`/mcp`), definir `main` como branch padrão, decidir sobre OmniRoute e Headroom |

**Limite da análise:** não foi possível transcrever o áudio dos vídeos, porque o container não tinha ferramenta de transcrição. A análise usou os quadros (texto na tela, legendas e telas mostradas) e a confirmação de cada ferramenta nas fontes oficiais.

Os dois vídeos são reels de isca: o criador pede um comentário ("XKGFR" no vídeo 1, "TASTE" no vídeo 2) para enviar os links por DM. Os links estão neste documento.

---

## 2. Vídeo 1: "5 plugins para o Claude Code parar de ser racionado"

**Ideia central:** o limite de uso do Claude Code costuma ser gasto à toa. Os 5 itens reduzem o gasto de tokens, evitam reexplicar o contexto toda hora ou permitem trocar de modelo.

### 2.1 Ferramentas

| # | Ferramenta | Para que serve | Custo |
|---|---|---|---|
| 1 | **OmniRoute** | Roteador de IA com um endpoint só. O vídeo mostra 237 provedores, 90+ com camada grátis e 500+ modelos. Permite trocar o modelo do Claude Code (ex.: Kimi, GLM) quando o limite acaba. | Software open source. Os modelos "grátis" têm limites dos próprios provedores. |
| 2 | **Claude Mem** | Memória persistente entre sessões. Exemplo do vídeo: perguntar "por que trocamos o KV por vetores?" e receber a resposta em menos de 1s. | Open source. Roda local e usa o Claude para resumir. |
| 3 | **Headroom** | Proxy que comprime saída de ferramentas, leitura de arquivos, buscas e logs. O painel do vídeo mostra de 64% a 93% de redução. | Open source, grátis. |
| 4 | **Claude Code Setup** (oficial) | Analisa o repositório e recomenda hooks, skills e MCPs sob medida. | Grátis, plugin verificado pela Anthropic. |
| 5 | **Task Observer** | Meta-skill que observa as tarefas e sugere melhorias para as skills. Quanto mais se usa, mais ele aprende. | Grátis. |

### 2.2 Cuidados

- **OmniRoute:** a promessa de "~1,6B de tokens grátis/mês" é do próprio projeto, não uma garantia. O vídeo mostra opções que usam cookie do navegador ou login de assinatura, o que pode violar os termos de uso dos provedores. Evitar colocar a assinatura do Claude por esse caminho.
- **Headroom:** redireciona o tráfego para um proxy local (`ANTHROPIC_BASE_URL`). Há uma issue aberta no GitHub dizendo que o contexto de 1M tokens pode se perder enquanto o Claude está "embrulhado" no proxy.
- Os números de economia vêm do painel de demonstração, não de um teste independente.

### 2.3 Instalação

```bash
# 1. OmniRoute (requer Node)
npm install -g omniroute
omniroute            # abre o painel; adicione provedores e depois aponte o Claude Code

# 2. Claude Mem (dentro do Claude Code)
/plugin marketplace add thedotmack/claude-mem
/plugin install claude-mem
# alternativa: npx claude-mem install   → reinicie o Claude Code

# 3. Headroom (requer Python/pip)
pip install "headroom-ai[proxy]"
headroom wrap claude       # inicia o Claude Code roteado pelo proxy
headroom unwrap claude     # desfaz

# 4. Claude Code Setup (dentro do Claude Code)
/plugin install claude-code-setup@claude-plugins-official
# depois peça: "recomende automações para este repositório"

# 5. Task Observer
npx skills add rebelytics/one-skill-to-rule-them-all --agent claude-code
# reinicie o Claude Code
```

**Ordem sugerida:** começar pelo 4 (oficial e sem risco), depois 2, depois 3. Deixar o 1 por último, porque é o que mais mexe na configuração.

---

## 3. Vídeo 2: "5 configurações para o Claude montar sites mais bonitos"

**Ideia central:** o Claude gera sites com cara genérica ("AI slop"). Três skills de design dão critério estético a ele. Dois MCPs dão contexto visual e deixam o Claude testar o próprio resultado.

### 3.1 Ferramentas

| # | Item | Tipo | O que faz |
|---|---|---|---|
| 1 | **Emil Kowalski skill** | Skill | Filosofia de "design engineer": animações, easing, sombras e detalhes que dão sensação de qualidade. |
| 2 | **Impeccable** | Skill | Comandos como shape, critique, audit, polish e animate para landing pages, dashboards e componentes. |
| 3 | **Taste Skill** | Skill | Framework "anti-slop" com regras de tipografia, layout e hierarquia. |
| 4 | **Figma MCP** | MCP | O Claude lê o design do Figma e implementa direto, em vez de "buscar inspirações" soltas. |
| 5 | **Playwright MCP** | MCP | O Claude abre o navegador, testa o site e corrige antes de entregar. |

**Custo:** as três skills e o Playwright MCP são gratuitos e open source. O Figma MCP é gratuito para instalar, mas precisa de conta Figma. Os limites de chamadas e o acesso a recursos como Dev Mode variam conforme o plano.

### 3.2 Instalação

```bash
# 1. Emil Kowalski
npx skills@latest add emilkowalski/skills

# 2. Impeccable
npx impeccable install
#  (ou, no Claude Code: /plugin marketplace add pbakaus/impeccable, depois instale em /plugin)

# 3. Taste Skill
npx skills add Leonxlnx/taste-skill
#  (ou: /plugin marketplace add Leonxlnx/taste-skill  e  /plugin install taste-skill@taste-skill)

# 4. Figma MCP
claude mcp add --transport http figma https://mcp.figma.com/mcp
#  depois rode /mcp no Claude Code e autentique com a conta Figma

# 5. Playwright MCP (Node 18+)
claude mcp add playwright npx @playwright/mcp@latest
npx playwright install
```

Na primeira vez, dizer "use o Playwright MCP para abrir o site". Sem isso, o Claude pode tentar rodar o Playwright pelo terminal.

**Como usar:** pedir "crie a landing page usando a taste skill e a impeccable". Depois pedir "abra no Playwright e me diga o que está feio". Se houver um design no Figma, colar o link dele.

### 3.3 O que não foi verificado

O comando do Figma MCP (`claude mcp add --transport http figma https://mcp.figma.com/mcp`) vem do conhecimento do produto e não da pesquisa feita na conversa. Confirmar em `help.figma.com`. Todos os outros comandos foram confirmados na documentação ou no GitHub de cada projeto.

---

## 4. O que foi feito no repositório

O Flavio estava fora do computador e pediu para fazer tudo automaticamente e instalar tudo que desse. A instalação foi feita **dentro do projeto**, para ficar versionada e valer também nas próximas sessões na nuvem.

### 4.1 Instalado

| O quê | Onde | Como |
|---|---|---|
| Skills do Emil Kowalski (pacote com 12) | `.claude/skills/` | `npx skills@latest add emilkowalski/skills` |
| Taste Skill (`design-taste-frontend`) | `.claude/skills/` | `npx skills add Leonxlnx/taste-skill` |
| Impeccable | `.claude/skills/` | `npx skills add pbakaus/impeccable` |
| Task Observer | `.claude/skills/` | `npx skills add rebelytics/one-skill-to-rule-them-all` |
| Plugin Claude Code Setup | `.claude/settings.json` | marketplace oficial da Anthropic |
| Plugin Claude Mem | `.claude/settings.json` | marketplace `thedotmack/claude-mem` |
| MCP Playwright | `.mcp.json` | `npx -y @playwright/mcp@latest` |
| MCP Figma | `.mcp.json` | `https://mcp.figma.com/mcp` |
| `README.md` | raiz | descreve tudo |

Skills instaladas na pasta: animate, animate-expo, animation-performance, animation-vocabulary, apple-design, ask-emil, ask-sonner, break-ui, choreograph, design-taste-frontend, emil-design-eng, find-animation-opportunities, gestures, impeccable, improve-animations, learn-taste, mobile-native, pick-ui-library, prototype, remove-animations, review-animations, task-observer, write-swift.

### 4.2 Não instalado, de propósito

- **OmniRoute:** roteia provedores por cookie ou assinatura, o que pode violar os termos de uso deles.
- **Headroom:** redireciona todo o tráfego do Claude por um proxy e pode perder o contexto de 1M.

Os comandos dos dois estão na seção 2.3 e no README, caso se queira instalar mesmo assim.

### 4.3 Resultado nesta sessão

- As skills carregaram, inclusive `claude-code-setup:claude-automation-recommender`.
- O Playwright MCP conectou.
- O **Figma MCP falhou** com "Proxy refused to open a tunnel: 403". É bloqueio de rede do container, não erro da configuração. No Claude Code normal, rodar `/mcp` e autenticar.

---

## 5. Linha do tempo das decisões

1. **Pedido:** analisar os 2 vídeos, explicar funcionamento, custo e instalação.
2. **Análise:** extração de quadros com `ffmpeg` (1 a cada 2s), leitura por contact sheets, e confirmação de cada ferramenta com buscas na web.
3. **Pedido de renomear o repositório** para algo como "Flaviotoolsclaude", sem nada de Lotus. O repositório estava vazio, então só o nome tinha "Lotus". Não havia ferramenta para renomear, e a orientação foi fazer em Settings → General → Repository name.
4. **"Fazer tudo automaticamente":** instalação das skills, plugins e MCPs no projeto, com commit local.
5. **Push falhou** (403). O GitHub não reconhecia o acesso do Claude ao repositório. O Flavio reconectou o GitHub.
6. **Push funcionou** na branch `claude/video-analysis-installation-84vboh`.
7. **Decisão do Flavio:** manter o nome `lotus-brasil-landing`. O título do README continua "Flavio Tools Claude".
8. **Pull Request:** não foi possível abrir, porque só existia uma branch e não havia `main` como destino.
9. **Autorização explícita** do Flavio para criar a `main`. A `main` foi criada com o mesmo conteúdo da branch de trabalho.
10. **Links** do repositório enviados.
11. **Este documento:** pedido para juntar tudo num projeto só no Claude.

---

## 6. Pendências para quando voltar ao computador

1. **Autenticar o Figma:** abrir o Claude Code no projeto, rodar `/mcp` e fazer login.
2. **Definir `main` como branch padrão:** Settings → Branches → Default branch.
3. **Aprovar os plugins** quando o Claude Code pedir (Claude Code Setup e Claude Mem).
4. **Decidir sobre OmniRoute e Headroom**, depois de ler os cuidados da seção 2.2.
5. **Opcional:** rodar o Claude Code Setup para receber recomendações específicas do projeto.
6. **Opcional:** usar as skills de design para refazer a landing page.

---

## 7. Links

- Repositório: https://github.com/guzflavio-spec/lotus-brasil-landing
- Branch `main`: https://github.com/guzflavio-spec/lotus-brasil-landing/tree/main
- Pasta das skills: https://github.com/guzflavio-spec/lotus-brasil-landing/tree/main/.claude/skills

Fontes das ferramentas:

- OmniRoute: https://github.com/diegosouzapw/OmniRoute
- Claude Mem: https://github.com/thedotmack/claude-mem
- Headroom: https://github.com/headroomlabs-ai/headroom
- Claude Code Setup: https://claude.com/marketplace/plugins/claude-code-setup
- Task Observer: https://github.com/rebelytics/one-skill-to-rule-them-all
- Taste Skill: https://github.com/leonxlnx/taste-skill
- Impeccable: https://github.com/pbakaus/impeccable
- Emil Kowalski: https://github.com/emilkowalski/skills
- Playwright MCP: https://github.com/microsoft/playwright-mcp

---

## 8. Como usar este arquivo no Claude

1. Em claude.ai, abrir **Projetos** e criar um projeto novo (ex.: "Ferramentas Claude Code").
2. Em **Conhecimento do projeto**, adicionar este arquivo (`CONVERSA-COMPLETA.md`).
3. Opcional: adicionar também o `README.md` do repositório.
4. Nas instruções do projeto, escrever algo como: "Use o documento CONVERSA-COMPLETA como referência das ferramentas instaladas e das pendências".
