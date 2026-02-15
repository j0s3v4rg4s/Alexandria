# Pragmatic Drag & Drop

## Qué es
Pragmatic Drag & Drop es un **toolchain de bajo nivel para drag and drop** desarrollado por Atlassian. Utiliza la funcionalidad nativa de drag and drop del navegador (no la reimplementa), lo que lo hace extremadamente liviano y performante. Es la misma librería que usa **Trello, Jira y Confluence** en producción.

## Para qué sirve
- Implementar drag and drop en cualquier aplicación web
- Crear experiencias como: kanban boards, listas reordenables, file uploads con drag, layouts editables
- Drag and drop accesible con soporte completo para tecnologías asistivas
- Experiencias con virtualización (listas enormes con scroll virtual)

## Características clave
- ✅ **Tiny:** ~4.7KB core (solo lo esencial)
- ✅ **Incremental:** Solo importas lo que necesitas (paquetes opcionales)
- ✅ **Headless:** Control total del rendering y estilos — sin opiniones visuales
- ✅ **Framework agnostic:** React, Vue, Angular, Svelte, vanilla JS
- ✅ **Cross-browser:** Soporte completo en Firefox, Safari, Chrome
- ✅ **Mobile:** Funciona en iOS y Android
- ✅ **Virtualización:** Compatible con listas virtualizadas
- ✅ **Deferred loading:** Puedes cargar los paquetes de forma lazy para mejorar tiempos de carga
- ✅ **Accesibilidad:** Toolchain opcional para experiencias con screen readers y tecnologías asistivas

## Arquitectura

La librería se divide en:

### Core (obligatorio)
El paquete base que maneja la mecánica del drag and drop. Sin opiniones sobre UI.

```bash
npm install @atlaskit/pragmatic-drag-and-drop
```

### Paquetes opcionales
- **Drop indicators** — indicadores visuales de dónde soltar
- **Hitbox** — detección de zonas de drop más precisa
- **Auto-scroll** — scroll automático al arrastrar hacia los bordes
- **Live region** — anuncios para screen readers
- **React adapter** — bindings específicos para React
- **Flourish** — animaciones de feedback visual

### Visual outputs (opcional)
Atlassian ofrece componentes visuales listos (drop indicators, etc.) basados en su Design System. Puedes usarlos, copiar el estilo, o ir por tu cuenta — no son obligatorios.

## Instalación

```bash
# Core
npm install @atlaskit/pragmatic-drag-and-drop

# Paquetes opcionales según necesidad
npm install @atlaskit/pragmatic-drag-and-drop-hitbox
npm install @atlaskit/pragmatic-drag-and-drop-auto-scroll
npm install @atlaskit/pragmatic-drag-and-drop-react-drop-indicator
npm install @atlaskit/pragmatic-drag-and-drop-live-region
npm install @atlaskit/pragmatic-drag-and-drop-flourish
```

## Ejemplo básico (React)

```tsx
import { draggable, dropTargetForElements } from '@atlaskit/pragmatic-drag-and-drop/element/adapter';
import { useEffect, useRef } from 'react';

function DraggableCard({ id, label }) {
  const ref = useRef(null);

  useEffect(() => {
    const el = ref.current;
    return draggable({
      element: el,
      getInitialData: () => ({ id }),
    });
  }, [id]);

  return <div ref={ref}>{label}</div>;
}

function DropZone({ onDrop }) {
  const ref = useRef(null);

  useEffect(() => {
    const el = ref.current;
    return dropTargetForElements({
      element: el,
      onDrop: ({ source }) => onDrop(source.data),
    });
  }, [onDrop]);

  return <div ref={ref}>Suelta aquí</div>;
}
```

## Cuándo usarlo
- Necesitas drag and drop **liviano y sin vendor lock-in** visual
- Quieres control total del aspecto (headless)
- Tu app tiene listas reordenables, kanban boards, o file drops
- Necesitas soporte mobile real
- La accesibilidad es importante para tu producto
- Usas cualquier framework (no solo React)

## Cuándo NO usarlo
- Si buscas una solución plug-and-play con UI incluida → considera `dnd-kit` o `react-beautiful-dnd`
- Si tu caso es muy simple y no justifica una librería

## Comparación rápida

| Librería | Tamaño | Framework | Headless | Accesibilidad | Estado |
|---|---|---|---|---|---|
| **Pragmatic DnD** | ~4.7KB | Cualquiera | ✅ | ✅ (opcional) | Activo (Atlassian) |
| dnd-kit | ~10KB | React | ✅ | ✅ | Activo |
| react-beautiful-dnd | ~30KB | React | ❌ | ✅ | Deprecado |
| SortableJS | ~10KB | Cualquiera | Parcial | ❌ | Mantenimiento |

## Enlaces
- 🐙 **GitHub:** https://github.com/atlassian/pragmatic-drag-and-drop
- 📚 **Docs:** https://atlassian.design/components/pragmatic-drag-and-drop
- 📦 **npm:** https://www.npmjs.com/package/@atlaskit/pragmatic-drag-and-drop

## Tags
#frontend #drag-and-drop #javascript #react #vue #angular #svelte #atlassian #ui #accesibilidad

## Relacionado
- [[Frontend]]
- [[Tooling]]
