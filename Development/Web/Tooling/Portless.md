# Portless

## Qué es

**Portless** es una herramienta CLI desarrollada por **Vercel Labs** que reemplaza los números de puerto en desarrollo local por URLs estables y con nombre usando el dominio `.localhost`. En lugar de recordar que tu app corre en `http://localhost:3000`, simplemente accedes a `https://myapp.localhost`.

Está pensado tanto para **desarrolladores humanos** como para **agentes de IA** que necesitan interactuar con servicios locales de forma predecible.

**Datos del proyecto:**
- **Repositorio:** [vercel-labs/portless](https://github.com/vercel-labs/portless)
- **npm:** `portless` (v0.6.0)
- **Lenguaje:** TypeScript
- **Licencia:** Apache-2.0
- **Estrellas GitHub:** ~4,459 ⭐
- **Creado:** Febrero 2026
- **Requisitos:** Node.js 20+, macOS o Linux

## Para qué sirve

### Problema que resuelve

En desarrollo local típico, cada servicio corre en un puerto diferente:
- Frontend: `localhost:3000`
- API: `localhost:8080`
- Docs: `localhost:4321`
- Admin: `localhost:3001`

Esto genera varios problemas:
1. **Colisiones de puertos** — Dos proyectos quieren usar el mismo puerto
2. **Difícil de recordar** — ¿Era el 3000 o el 3001?
3. **URLs inestables** — El puerto puede cambiar entre sesiones
4. **Problemas con cookies/CORS** — Todo es `localhost`, difícil aislar dominios
5. **Agentes de IA confundidos** — Los agentes no saben qué puerto corresponde a qué servicio

### Solución

Portless actúa como un **proxy reverso local** que:
- Asigna automáticamente puertos efímeros (rango 4000-4999) a tus apps
- Ruteea el tráfico basándose en el **nombre** en lugar del **puerto**
- Todo pasa por un único punto de entrada: `*.localhost:1355` (o puerto 443 con HTTPS)

```
Browser → myapp.localhost:1355 → Proxy Portless → :4123 (tu app)
Browser → api.localhost:1355   → Proxy Portless → :4567 (tu API)
```

## Instalación

```bash
# Instalación global (NO como dependencia de proyecto)
npm install -g portless
```

> ⚠️ **Importante:** Debe instalarse globalmente. No usar como dependencia de proyecto ni ejecutar via `npx`.

## Uso

### Uso básico

```bash
# Ejecutar tu app a través de portless
portless myapp next dev
# -> http://myapp.localhost:1355

# Con HTTPS/HTTP2 (primera vez requiere sudo para certificados)
portless proxy start --https
portless myapp next dev
# -> https://myapp.localhost
```

### En package.json

```json
{
  "scripts": {
    "dev": "portless run next dev"
  }
}
```

Cuando usas `portless run` (sin nombre explícito), el nombre se infiere automáticamente del directorio del proyecto.

### Subdominios

```bash
# Organizar microservicios con subdominios
portless api.myapp pnpm start
# -> http://api.myapp.localhost:1355

portless docs.myapp next dev
# -> http://docs.myapp.localhost:1355
```

Los subdominios wildcard funcionan automáticamente: `tenant1.myapp.localhost:1355` ruteará a la app `myapp` sin configuración extra.

### Alias estáticos (para Docker u otros servicios)

```bash
# Registrar un servicio que ya está corriendo en un puerto fijo
portless alias postgres 5432
portless alias redis 6379
```

### Git Worktrees

Portless detecta automáticamente git worktrees y asigna subdominios por branch:

```bash
# Main worktree
portless run next dev   # -> http://myapp.localhost:1355

# Worktree del branch "fix-ui"
portless run next dev   # -> http://fix-ui.myapp.localhost:1355
```

## Características avanzadas

### HTTPS / HTTP2

```bash
# Habilitar HTTPS con certificados auto-generados
portless proxy start --https

# La primera vez solicita sudo para confiar en la CA local
# Después no necesita permisos elevados

# Usar certificados propios (e.g., de mkcert)
portless proxy start --cert ./cert.pem --key ./key.pem

# Confiar en la CA manualmente
sudo portless trust
```

**¿Por qué HTTP/2?** Los navegadores limitan HTTP/1.1 a 6 conexiones por host. Dev servers como Vite sirven muchos archivos sin bundle, y HTTP/2 multiplexa todo en una sola conexión → **carga más rápida**.

### TLD personalizado

```bash
# Usar .test en lugar de .localhost
sudo portless proxy start --https --tld test
portless myapp next dev
# -> https://myapp.test
```

**Recomendaciones de TLD:**
- ✅ `.test` — Reservado por IANA, sin riesgo de colisión
- ⚠️ `.local` — Conflictos con mDNS/Bonjour
- ❌ `.dev` — Propiedad de Google, fuerza HTTPS via HSTS

### Variables de entorno

Portless inyecta estas variables en los procesos hijos:

| Variable | Descripción |
|----------|-------------|
| `PORT` | Puerto efímero asignado |
| `HOST` | Siempre `127.0.0.1` |
| `PORTLESS_URL` | URL pública (e.g. `https://myapp.localhost`) |

Variables de configuración:

| Variable | Descripción |
|----------|-------------|
| `PORTLESS_HTTPS=1` | Habilitar HTTPS por defecto |
| `PORTLESS_PORT=<n>` | Cambiar puerto del proxy |
| `PORTLESS_TLD=<tld>` | Cambiar TLD |
| `PORTLESS_SYNC_HOSTS=1` | Sincronizar `/etc/hosts` |
| `PORTLESS=0` | Desactivar portless temporalmente |

### Proxying entre apps Portless

Si tu frontend proxy (Vite, webpack) redirige requests a otra app portless, necesitas `changeOrigin: true`:

```ts
// vite.config.ts
server: {
  proxy: {
    "/api": {
      target: "http://api.myapp.localhost:1355",
      changeOrigin: true,  // IMPORTANTE
      ws: true,
    },
  },
}
```

Sin esto, portless detecta el loop y responde con `508 Loop Detected`.

## Comandos

| Comando | Descripción |
|---------|-------------|
| `portless run [--name <name>] <cmd>` | Ejecutar app (nombre inferido o explícito) |
| `portless <name> <cmd> [args...]` | Ejecutar app con nombre explícito |
| `portless alias <name> <port>` | Registrar ruta estática |
| `portless alias --remove <name>` | Eliminar ruta estática |
| `portless list` | Mostrar rutas activas |
| `portless trust` | Agregar CA al trust store del sistema |
| `portless hosts sync` | Agregar rutas a `/etc/hosts` |
| `portless hosts clean` | Limpiar entradas de `/etc/hosts` |
| `portless proxy start` | Iniciar proxy (daemon) |
| `portless proxy start --https` | Iniciar con HTTPS/HTTP2 |
| `portless proxy stop` | Detener proxy |

## Frameworks compatibles

Portless funciona con cualquier framework que respete la variable `PORT`:
- **Next.js** ✅ (nativo)
- **Express** ✅ (nativo)
- **Nuxt** ✅ (nativo)
- **Fastify** ✅ (nativo)

Para frameworks que ignoran `PORT`, portless auto-inyecta los flags `--port` y `--host`:
- **Vite** ✅ (auto-inyección)
- **Astro** ✅ (auto-inyección)
- **React Router** ✅ (auto-inyección)
- **Angular** ✅ (auto-inyección)

## Comparación con alternativas

| Herramienta | Tipo | HTTPS | Subdominios | Local-only |
|------------|------|-------|-------------|------------|
| **Portless** | Proxy local | ✅ Auto-cert | ✅ Wildcard | ✅ |
| **ngrok** | Túnel remoto | ✅ | ✅ | ❌ (tráfico sale) |
| **localtunnel** | Túnel remoto | ✅ | ❌ | ❌ |
| **caddy** | Proxy reverso | ✅ | ✅ Manual | ✅ |
| **traefik** | Proxy reverso | ✅ | ✅ Manual | ✅ |
| **mkcert** | Solo certs | ✅ | ❌ | ✅ |

**Ventaja principal de Portless:** Zero-config. No necesitas configurar Caddyfile, docker-compose, ni nada. Solo `portless <name> <cmd>` y funciona.

## Arquitectura

```
┌─────────────────────────────────────────┐
│              Browser                     │
│  myapp.localhost:1355                    │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│         Portless Proxy (daemon)          │
│         Puerto 1355 (o 443 HTTPS)        │
│                                          │
│  Routing table:                          │
│  myapp     → 127.0.0.1:4123             │
│  api.myapp → 127.0.0.1:4567             │
│  docs      → 127.0.0.1:4890             │
└──────┬───────────────┬──────────────────┘
       │               │
┌──────▼─────┐  ┌──────▼─────┐
│  Next.js   │  │  Express   │
│  :4123     │  │  :4567     │
└────────────┘  └────────────┘
```

## Limitaciones

- **Solo macOS y Linux** — No soporta Windows (aún)
- **Node.js 20+** — Requiere versión moderna
- **Safari con .localhost** — Puede requerir `portless hosts sync` para resolver subdominios
- **No es un túnel** — Solo funciona localmente, no expone tu app a internet (para eso usar ngrok)

## Tags

#development #tooling #proxy #localhost #vercel #devserver #https #http2 #dx #npm

## Relacionado

- [[Unlighthouse]]
