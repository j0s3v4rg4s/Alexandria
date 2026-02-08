# Google Search – Client-side JS (Submit/Click Handling)

## Qué es
Fragmento de **JavaScript del frontend de Google Search**. Maneja eventos globales de **submit** y **click**, previniendo acciones por atributos `data-*`, y configura métricas/telemetría (performance, lazy loading de imágenes, etc.).

## Qué hace (alto nivel)
- **Intercepta `submit`** para evitar envíos según flags (`data-submitfalse`, validaciones de `q`).
- **Intercepta `click` en enlaces** para prevenir navegación cuando `data-nohref=1`.
- **Inicializa flags de estado** (`google.hs`, `google.c`) para comportamiento del cliente.
- **Instrumenta performance** (timing, métricas) y **lazy-loading** de imágenes.

## Por qué es interesante
- Ejemplo real de **event delegation** a nivel `documentElement`.
- Uso intensivo de **atributos `data-*`** como feature flags.
- Patrón de **telemetría y performance** en producción a gran escala.

## Snippet (referencia)
```js
// (fragmento compartido)
// Intercepta submit/click y setea flags/telemetría
```

## Tags
#frontend #javascript #performance #event-delegation #google

## Relacionado
- [[Performance]]
- [[Web Performance]]
- [[Frontend]]
