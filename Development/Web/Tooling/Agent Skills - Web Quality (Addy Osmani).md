# Agent Skills - Web Quality (Addy Osmani)

## Qué es

**Web Quality Skills** es una colección completa de Agent Skills (instrucciones especializadas para agentes de IA) creada por **Addy Osmani** (Google Chrome team) para optimizar proyectos web siguiendo las guías de **Google Lighthouse** y **Core Web Vitals**.

Son instrucciones que se instalan en tu agente de código (Claude Code, Cursor, Codex, OpenClaw) para que automáticamente aplique mejores prácticas de:
- ✅ **Performance** (velocidad de carga, optimización de recursos)
- ✅ **Accesibilidad** (WCAG 2.1, screen readers, navegación por teclado)
- ✅ **SEO** (optimización para buscadores, crawlability, structured data)
- ✅ **Best Practices** (seguridad, APIs modernas, calidad de código)

**Stack-agnostic:** Funciona con cualquier framework (React, Vue, Angular, Svelte, Next.js, Nuxt, Astro, HTML plano, etc.)

## Para qué sirve

Mientras las guías de UI te dicen **qué construir**, Web Quality Skills te dicen **cómo construirlo** de forma performante, accesible y optimizada para buscadores.

### Casos de uso prácticos

1. **Auditorías automáticas:** "Audita mi sitio" → El agente revisa 150+ checks de Lighthouse
2. **Optimización de performance:** "Optimiza el performance" → Critical rendering path, code splitting, lazy loading, etc.
3. **Core Web Vitals:** "Mejora mi LCP" → Optimizaciones específicas para LCP, INP, CLS
4. **Accesibilidad:** "Revisa la accesibilidad" → WCAG compliance, contraste, navegación
5. **SEO técnico:** "Optimiza para SEO" → Meta tags, structured data, sitemaps

## Instalación

### Opción 1: Con npx (recomendado)
```bash
npx add-skill addyosmani/web-quality-skills
```

O también:
```bash
npx skills add addyosmani/web-quality-skills
```

### Opción 2: Manual
```bash
git clone https://github.com/addyosmani/web-quality-skills
cd web-quality-skills
cp -r skills/* ~/.claude/skills/
```

### Opción 3: OpenClaw
Para OpenClaw, copiar los skills a:
```bash
~/.openclaw/skills/
```

## Skills Disponibles

| Skill | Descripción | Trigger |
|-------|-------------|---------|
| **web-quality-audit** | Revisión completa (todas las categorías) | "Audit my site", "Check web quality" |
| **performance** | Velocidad de carga, optimización de recursos | "Optimize performance", "Speed up" |
| **core-web-vitals** | LCP, INP, CLS específicos | "Improve Core Web Vitals", "Fix LCP" |
| **accessibility** | WCAG compliance, screen readers | "Improve accessibility", "a11y review" |
| **seo** | Optimización para buscadores | "Optimize for SEO", "Fix meta tags" |
| **best-practices** | Seguridad, APIs modernas, calidad | "Best practices", "Security audit" |

## Cómo Usar

Una vez instalados, los skills se activan automáticamente cuando tu request coincide con su descripción:

```
"Audita esta página por problemas de calidad web"
→ Activa web-quality-audit

"Optimiza el performance y arregla Core Web Vitals"
→ Activa performance + core-web-vitals

"Revisa la accesibilidad y sugiere mejoras"
→ Activa accessibility

"Haz esto SEO-ready"
→ Activa seo
```

## Métricas y Benchmarks

### Core Web Vitals

| Métrica | Bueno | Mejorable | Pobre |
|---------|-------|-----------|-------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5s – 4.0s | > 4.0s |
| INP (Interaction to Next Paint) | ≤ 200ms | 200ms – 500ms | > 500ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1 – 0.25 | > 0.25 |

### Performance Budget

| Tipo de recurso | Budget |
|-----------------|--------|
| Peso total | < 1.5 MB |
| JavaScript | < 300 KB (comprimido) |
| CSS | < 100 KB (comprimido) |
| Imágenes | < 500 KB above-fold |
| Fuentes | < 100 KB |
| Third-party | < 200 KB |

### Lighthouse Scores

| Categoría | Target |
|-----------|--------|
| Performance | ≥ 90 |
| Accessibility | 100 |
| Best Practices | ≥ 95 |
| SEO | ≥ 95 |

## Patrones por Framework

### React/Next.js
```jsx
import Image from 'next/image'
const LazyComponent = React.lazy(() => import('./Heavy'))

// Para INP
const handleClick = useCallback(() => {}, [])
const expensiveValue = useMemo(() => compute(), [deps])
```

### Vue/Nuxt
```vue
<NuxtImg src="/image.jpg" />
<component :is="AsyncComponent" />

<!-- v-once para contenido estático -->
<div v-once>{{ staticContent }}</div>
```

### Svelte/SvelteKit
```svelte
<script>
  import { Image } from 'svelte:image'
  // Reactive statements para performance
  $: computed = expensive(value)
</script>

{#await promise}...{/await}
```

### Astro
```astro
---
import { Image } from 'astro:assets'
---
<Image src={hero} alt="Hero" />

<!-- Partial hydration -->
<Component client:idle />
```

### HTML plano
```html
<!-- Native lazy loading -->
<img src="image.jpg" loading="lazy" alt="Description">

<!-- Picture para responsive -->
<picture>
  <source media="(min-width: 800px)" srcset="large.webp">
  <img src="small.jpg" alt="Description">
</picture>

<!-- Preconnect -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

## Qué Revisa

### Performance (50+ patterns)
- Critical rendering path
- JavaScript bundling y code splitting
- Optimización de imágenes (formatos, sizing, lazy loading)
- Estrategias de carga de fuentes
- Caching y preloading
- Optimización de respuesta del servidor

### Accesibilidad (40+ rules)
- **Perceivable:** Alternativas de texto, captions, contraste
- **Operable:** Navegación por teclado, timing, navegación
- **Understandable:** Legibilidad, predictibilidad, asistencia de input
- **Robust:** Compatibilidad con tecnologías asistivas

### SEO (30+ requirements)
- SEO técnico (crawlability, indexability)
- SEO on-page (meta tags, headings, estructura)
- Structured data (JSON-LD, schema.org)
- Mobile-friendliness
- Señales de performance

### Best Practices (20+ patterns)
- HTTPS y security headers
- APIs modernas de JavaScript
- Compatibilidad de navegadores
- Manejo de errores
- Console limpio

## Links

- **Repo:** https://github.com/addyosmani/web-quality-skills
- **Lighthouse Docs:** https://developer.chrome.com/docs/lighthouse/
- **Core Web Vitals:** https://web.dev/articles/vitals
- **WCAG 2.1:** https://www.w3.org/WAI/WCAG21/quickref/
- **Agent Skills Spec:** https://agentskills.io/specification

## Tags

#desarrollo #web #performance #accesibilidad #seo #lighthouse #core-web-vitals #agent-skills #ia #optimizacion #google #addy-osmani #wcag #best-practices

## Relacionado

- [[Lighthouse]] (por crear)
- [[Core Web Vitals]] (por crear)
- [[WCAG]] (por crear)
- [[Agent Skills]] (por crear)
