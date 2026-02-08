# Hosting gratuitos de bases de datos (2026)

> Curado y actualizado para proyectos personales, side‑projects y MVPs.  
> **Nota:** los free tiers sirven para empezar, no para cargas críticas sostenidas.

---

## Resumen rápido
- Ideal para **desarrollo, demos y MVPs**.
- Espera **límites de storage, conexiones y tiempo de cómputo**.
- Muchos servicios aplican **cold starts** o suspensión por inactividad.
- Evita lock‑in: revisa compatibilidad y planes de salida.

---

## Comparativa rápida

| Servicio | Motor | Límite gratis | Extras | Ideal para |
|---|---|---|---|---|
| **Neon** | PostgreSQL | 500 MB · 100h compute | Branching, serverless | SaaS early, staging |
| **MongoDB Atlas** | MongoDB | 512 MB | Backups auto | Apps NoSQL pequeñas |
| **Turso** | SQLite | 5 GB · 500M reads | Distribuido, edge | Apps ligeras, edge |
| **Supabase** | PostgreSQL | 500 MB · 5 GB transfer | Auth, Storage, Realtime | MVP full‑stack |
| **CockroachDB** | SQL distribuido | 10 GB · 50M req | Alta disponibilidad | Experimentos distribuidos |
| **Filess** | MariaDB | 10 MB | Simple | Demos rápidas |
| **FreeDB.tech** | MySQL | 25 MB · 200 conns | — | Pruebas básicas |
| **Koyeb** | PostgreSQL | 1 GB · 5h ejecución | App + DB | Prototipos |

---

## Análisis por proveedor

### Neon — https://neon.tech
- **Qué es:** PostgreSQL serverless con branching tipo Git.
- **Free:** 500 MB, ~100h de cómputo/mes.
- **Pros:** DX excelente, ideal para dev/staging.
- **Contras:** Cold starts; no para workloads constantes.

### MongoDB Atlas — https://www.mongodb.com
- **Qué es:** MongoDB gestionado.
- **Free:** 512 MB, backups automáticos.
- **Pros:** Estable y conocido.
- **Contras:** Cluster compartido → latencia; límites de conexiones.

### Turso — https://turso.tech
- **Qué es:** SQLite distribuido.
- **Free:** 5 GB, 500M lecturas.
- **Pros:** Latencia muy baja, ideal edge.
- **Contras:** No es Postgres/MySQL (ojo migraciones).

### Supabase — https://supabase.com
- **Qué es:** Postgres + Auth + Storage + Realtime.
- **Free:** 500 MB DB, 5 GB transferencia.
- **Pros:** Plataforma completa para MVP.
- **Contras:** Límites ajustados para prod.

### CockroachDB — https://www.cockroachlabs.com
- **Qué es:** SQL distribuido.
- **Free:** 10 GB, 50M requests.
- **Pros:** Alta disponibilidad.
- **Contras:** Complejidad; overkill para proyectos chicos.

### Filess — https://filess.io
- **Qué es:** MariaDB sencillo.
- **Free:** 10 MB.
- **Pros:** Rápido para demos.
- **Contras:** Muy limitado.

### FreeDB.tech — https://freedb.tech
- **Qué es:** MySQL gratuito.
- **Free:** 25 MB, 200 conexiones.
- **Pros:** Fácil acceso.
- **Contras:** Confiabilidad variable; no recomendado para serio.

### Koyeb — https://www.koyeb.com
- **Qué es:** Plataforma app + DB.
- **Free:** 1 GB Postgres, 5h ejecución.
- **Pros:** Útil para prototipos integrados.
- **Contras:** Modelo de límites poco claro.

---

## Recomendaciones prácticas
- **Side‑project:** Turso, Neon.
- **MVP full‑stack:** Supabase.
- **NoSQL pequeño:** MongoDB Atlas.
- **Distribuido/experimento:** CockroachDB.

## Advertencias
- Revisa **políticas de suspensión** y **exportación**.
- Configura **backups** incluso en free tier.
- Monitorea **conexiones y latencia**.

---

## Pendiente por revisar
- PlanetScale (estado free tier).
- Railway / Render DBs (cambios 2025‑2026).

---

*Nota creada y curada para el vault **Alexandria**.*