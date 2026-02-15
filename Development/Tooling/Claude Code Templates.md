# Claude Code Templates

## Qué es
Claude Code Templates es una **colección de configuraciones y plantillas listas para usar** con Claude Code (el agente CLI de Anthropic). Incluye agentes especializados, comandos personalizados, hooks, integraciones MCP y herramientas de monitoreo — todo instalable con un solo comando via `npx`.

## Para qué sirve
- Configurar agentes de IA especializados por dominio (seguridad, frontend, bases de datos, etc.)
- Agregar comandos slash personalizados a Claude Code (`/generate-tests`, `/optimize-bundle`, `/check-security`)
- Integrar servicios externos via MCP (GitHub, PostgreSQL, Stripe, AWS, OpenAI)
- Monitorear sesiones de desarrollo con IA en tiempo real
- Automatizar con hooks (validación pre-commit, acciones post-completado)

## Componentes disponibles

| Componente | Descripción | Ejemplos |
|---|---|---|
| 🤖 **Agents** | Especialistas IA por dominio | Security auditor, React optimizer, DB architect |
| ⚡ **Commands** | Comandos slash personalizados | `/generate-tests`, `/optimize-bundle`, `/check-security` |
| 🔌 **MCPs** | Integraciones con servicios externos | GitHub, PostgreSQL, Stripe, AWS, OpenAI |
| ⚙️ **Settings** | Configuraciones de Claude Code | Timeouts, memoria, estilos de output |
| 🪝 **Hooks** | Triggers de automatización | Pre-commit validation, post-completion actions |
| 🎨 **Skills** | Capacidades reutilizables | Procesamiento PDF, automatización Excel |

## Instalación y uso

```bash
# Instalación interactiva (navegar y elegir)
npx claude-code-templates@latest

# Instalar un stack completo de desarrollo
npx claude-code-templates@latest --agent development-team/frontend-developer --command testing/generate-tests --mcp development/github-integration --yes

# Instalar componentes específicos
npx claude-code-templates@latest --agent development-tools/code-reviewer --yes
npx claude-code-templates@latest --command performance/optimize-bundle --yes
npx claude-code-templates@latest --hook git/pre-commit-validation --yes
npx claude-code-templates@latest --mcp database/postgresql-integration --yes
```

## Herramientas adicionales incluidas

### 📊 Analytics
Monitoreo en tiempo real de sesiones de desarrollo con IA:
```bash
npx claude-code-templates@latest --analytics
```

### 💬 Conversation Monitor
Interfaz mobile-optimized para ver respuestas de Claude en tiempo real:
```bash
# Local
npx claude-code-templates@latest --chats

# Acceso remoto seguro via Cloudflare Tunnel
npx claude-code-templates@latest --chats --tunnel
```

### 🔍 Health Check
Diagnóstico completo de tu instalación de Claude Code:
```bash
npx claude-code-templates@latest --health-check
```

## Enlaces
- 🔗 **Sitio:** https://aitmpl.com
- 📚 **Docs:** https://docs.aitmpl.com
- 🐙 **GitHub:** https://github.com/davila7/claude-code-templates
- 📦 **npm:** https://www.npmjs.com/package/claude-code-templates

## Tags
#claude #ai #tooling #templates #agents #mcp #cli #prompts #automation

## Relacionado
- [[SpaceCake]]
- [[Tooling]]
