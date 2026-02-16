# Sileo

## Qué es

Sileo es una biblioteca de componentes de notificaciones (toasts) para React, lanzada en 2026. Está diseñada para ser hermosa por defecto sin necesidad de configuración adicional. Usa física-based animations con SVG para lograr transiciones fluidas y naturales.

## Para qué sirve

- Mostrar notificaciones tipo toast en aplicaciones React
- Comunicar estados al usuario: éxito, error, advertencia, info
- Posicionar notificaciones en cualquier esquina o zona de la pantalla
- Añadir animaciones elegantes sin configurar nada manualmente

## Características principales

- ✅ **Bonito por defecto** — cero configuración necesaria para lucir bien
- 🎯 **Múltiples estados** — éxito, error, advertencia, carga, info
- 📍 **Posiciones configurables** — top-left, top-right, bottom-left, bottom-right, center
- 🎬 **Animaciones con SVG** — physics-based, fluidas y naturales
- 📦 **TypeScript** — tipado completo incluido

## Instalación y uso básico

```bash
npm install sileo
```

```tsx
import { toast, Toaster } from 'sileo';

// Add the Toaster to your app root
function App() {
  return (
    <>
      <Toaster />
      <button onClick={() => toast.success('Saved successfully!')}>
        Save
      </button>
    </>
  );
}

// Available toast types
toast.success('Operation completed');
toast.error('Something went wrong');
toast.warning('Be careful');
toast.info('Here is some info');
toast.loading('Processing...');

// With custom options
toast.success('Done!', {
  position: 'bottom-right',
  duration: 3000,
});
```

## Tags

#react #ui #notifications #toast #frontend #animations #typescript #2026

## Relacionado

- [[pragmatic-drag-and-drop]]
- [[Unlighthouse]]
