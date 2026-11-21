# Flavio Tools Claude

Configuração do Claude Code (skills, plugins e MCPs) instalada a partir de dois vídeos.

## Instalado neste repositório
**Skills (`.claude/skills/`)**: Emil Kowalski, Impeccable, Taste Skill, Task Observer.
**Plugins (`.claude/settings.json`)**: Claude Code Setup (oficial), Claude Mem.
**MCPs (`.mcp.json`)**: Playwright, Figma (autenticar com `/mcp` no primeiro uso).

**Agentes (`.claude/agents/`)**: `consultor-360` — consultor estratégico padrão McKinsey que faz diagnóstico 360° de uma empresa (12 dimensões, scorecard, recomendações priorizadas, roadmap 30-60-90 e KPIs). Uso: peça "use o agente consultor-360 para analisar a empresa X" ou invoque com `@consultor-360`.

## Não instalado de propósito
- **OmniRoute**: roteia provedores por cookie/assinatura, o que pode violar termos de uso. Instalar manualmente: `npm install -g omniroute`.
- **Headroom**: proxy que redireciona todo o tráfego do Claude (`ANTHROPIC_BASE_URL`) e pode perder o contexto de 1M. Instalar manualmente: `pip install "headroom-ai[proxy]"` e `headroom wrap claude`.
