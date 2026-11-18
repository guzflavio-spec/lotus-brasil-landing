# Flavio Tools Claude

Configuração do Claude Code (skills, plugins e MCPs) instalada a partir de dois vídeos.

## Instalado neste repositório
**Skills (`.claude/skills/`)**: Emil Kowalski, Impeccable, Taste Skill, Task Observer.
**Plugins (`.claude/settings.json`)**: Claude Code Setup (oficial), Claude Mem.
**MCPs (`.mcp.json`)**: Playwright, Figma (autenticar com `/mcp` no primeiro uso).

## Não instalado de propósito
- **OmniRoute**: roteia provedores por cookie/assinatura, o que pode violar termos de uso. Instalar manualmente: `npm install -g omniroute`.
- **Headroom**: proxy que redireciona todo o tráfego do Claude (`ANTHROPIC_BASE_URL`) e pode perder o contexto de 1M. Instalar manualmente: `pip install "headroom-ai[proxy]"` e `headroom wrap claude`.
