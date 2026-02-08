# Google Search – Performance Timers & AFT Logic

## Qué es
Fragmento de **JavaScript cliente de Google Search** enfocado en **medición de performance**, especialmente **AFT (Above The Fold Time)**, visibilidad de elementos, lazy‑loading y reporte de métricas.

## Qué hace
- Gestiona **timers** (`google.startTick`, `google.tick`) para medir hitos de carga.
- Calcula **visibilidad real** de elementos en viewport y contenedores con overflow.
- Determina **AFT / IMAGES / IMAGES IN VIEW** con lógica avanzada.
- Reporta métricas vía **CSI / gen_204**.
- Maneja estados como **reload, back/forward, prerender**.

## Por qué es interesante
- Ejemplo real de **performance instrumentation a escala Google**.
- Lógica no trivial para decidir cuándo algo cuenta como visible.
- Separación clara entre **recolección**, **agregación** y **reporte**.

## Conceptos clave
- AFT (Above The Fold Time)
- Event delegation + viewport math
- Performance API (`performance.now`, `navigation`)
- Lazy loading controlado por métricas

## Tags
#frontend #javascript #performance #aft #metrics #google

## Relacionado
- [[Performance]]
- [[Web Performance]]
- [[Google-Search-Client-JS]]
