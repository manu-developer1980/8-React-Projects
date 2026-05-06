# Guía de seguimiento — 8 proyectos React (portfolio)

Este documento es tu **hoja de ruta** sin calendario: avanzas por **orden sugerido** o lo ajustas, pero cada proyecto tiene un **MVP cerrado** para poder cerrarlo con sensación de logro aunque los ratos de estudio sean irregulares.

**Antes de codificar** en cada uno: copia `PROJECT_BRIEF_TEMPLATE.md` a la carpeta del proyecto (`BRIEF.md`), rellénalo y revisión con preguntas de planificación (edge cases incluidos).

---

## Cómo usar esta guía sin fechas límite

- Trabaja en **un proyecto activo**; los demás quedan en cola.
- Define solo **“siguiente hito”** (por ejemplo: vertical slice en pantalla), no semanas.
- Si dejas varios días sin tocar el repo: al volver, lee **tu propio `BRIEF.md` + último commit** antes de añadir features.
- Marca las casillas de seguimiento cuando **de verdad** cumplan el criterio (no por optimismo).

---

## Orden sugerido (progresión técnica)

| Orden | # | Proyecto (nombre corto) |
|------|---|-------------------------|
| 1 | 1 | Panel de operaciones (dashboard) |
| 2 | 2 | Catálogo B2B + presupuesto |
| 3 | 4 | Explorador de API pública |
| 4 | 3 | Agenda de conferencia / festival |
| 5 | 6 | Tablero CRM (pipeline Kanban) |
| 6 | 5 | Visor Markdown + guías |
| 7 | 7 | Constructor de presupuestos / cotizaciones |
| 8 | 8 | Micro-SaaS: landing + app demo |

*Los números de proyecto (#) son los del listado detallado abajo; el orden “1→2→4…” sube estado y datos antes del DnD y del Markdown, y cierra con algo que parezca producto completo.*

Puedes seguir el orden 1–8 lineal si prefieres simplicidad mental; el orden de la tabla solo optimiza la curva de dificultad.

---

## Seguimiento global

Marca cuando el proyecto esté **cerrado a nivel MVP** según su checklist y tu `BRIEF.md`.

- [ ] Proyecto 1 — Dashboard
- [ ] Proyecto 2 — Catálogo B2B
- [ ] Proyecto 3 — Agenda conferencia
- [ ] Proyecto 4 — Explorador API
- [ ] Proyecto 5 — Markdown + guías
- [ ] Proyecto 6 — Kanban CRM
- [ ] Proyecto 7 — Presupuestos / cotizaciones
- [ ] Proyecto 8 — Micro-SaaS demo

**Opcional para portfolio:** README con decisiones, capturas o enlace a deploy en cada repo.

---

## Proyecto 1 — Panel de operaciones (dashboard)

**Idea:** panel interno ficticio (ventas, soporte, inventario…) con KPIs, tabla y filtros. Datos mock.

**Qué demuestra en portfolio:** layout de app real, densidad de información, estados de UI, filtros.

**React / frontend:** componentización, estado derivado, tablas, filtros, skeletons o loading claro.

**MVP:** 4–6 KPIs + tabla filtrable + rango de fechas (mock).

**Plus (cuando el MVP esté hecho):** export CSV del resultado filtrado solo en cliente.

**Carpeta sugerida:** `new-learning-path/p01-dashboard/`

**Checklist cierre MVP:**

- [ ] Brief aceptado (incl. edge cases de tabla vacía, filtros sin resultados, datos raros)
- [ ] Flujo principal usable
- [ ] README + (opcional) deploy

---

## Proyecto 2 — Catálogo B2B + solicitud de presupuesto

**Idea:** catálogo de productos o servicios con grid, comparador simple (p. ej. hasta 3 ítems) y formulario “solicitar presupuesto”.

**Qué demuestra:** flujo comercial creíble; no es un carrito tutorial genérico.

**React / frontend:** formularios, validación, estado de selección múltiple, rutas listado ↔ ficha.

**MVP:** listado + filtros + comparar hasta 3 + formulario con pantalla de confirmación o resumen.

**Plus:** persistir borrador del formulario en `localStorage`.

**Carpeta sugerida:** `new-learning-path/p02-catalogo-b2b/`

**Checklist cierre MVP:**

- [ ] Brief con estados de formulario y doble submit
- [ ] Comparador con límites claros (máx. ítems)
- [ ] README + (opcional) deploy

---

## Proyecto 3 — Agenda de conferencia / festival

**Idea:** programa por tracks, favoritos, detección de solapes de horario, vista “mi agenda”.

**Qué demuestra:** datos relacionados (sesiones, salas), reglas de negocio en UI, UX de eventos.

**React / frontend:** modelar datos en memoria, evitar renders innecesarios cuando toque, rutas o pestañas.

**MVP:** agenda + favoritos + aviso o resolución de solapes.

**Plus:** datos solo JSON estático; service worker solo si sobra tiempo y lo justificas en el brief.

**Carpeta sugerida:** `new-learning-path/p03-agenda-evento/`

**Checklist cierre MVP:**

- [ ] Brief: qué pasa si dos sesiones chocan (regla explícita)
- [ ] Favoritos y “mi agenda” coherentes
- [ ] README + (opcional) deploy

---

## Proyecto 4 — Explorador de API pública

**Idea:** buscador con listado, detalle, paginación o cursor, lista de “guardados” local. Ejemplos: GitHub, TMDB, Open Library (elige una en el brief).

**Qué demuestra:** fetch real, errores, vacíos, URLs compartibles; muy entrevistable.

**React / frontend:** efectos con propósito, cancelación o control de carreras, estado async limpio.

**MVP:** búsqueda + detalle + guardados (memoria o `localStorage`).

**Plus:** test de un hook de datos o de un reducer pequeño.

**Carpeta sugerida:** `new-learning-path/p04-api-explorer/`

**Checklist cierre MVP:**

- [ ] Brief: límites de la API (rate limit, sin resultados)
- [ ] Estados loading / error / empty en búsqueda y detalle
- [ ] README + (opcional) deploy

---

## Proyecto 5 — Visor Markdown + colección de guías

**Idea:** índice de documentos (MD en repo o JSON), tabla de contenidos, búsqueda simple, vista lectura.

**Qué demuestra:** contenido técnico en portfolio; encaja bien en perfiles frontend.

**React / frontend:** routing por slug, render MD seguro, rendimiento básico en listas largas.

**MVP:** índice + lectura + anclas + búsqueda simple.

**Plus:** estilos de impresión o vista “handout”.

**Carpeta sugerida:** `new-learning-path/p05-markdown-guias/`

**Checklist cierre MVP:**

- [ ] Brief: origen de los MD y qué pasa con MD roto o vacío
- [ ] Navegación slug clara
- [ ] README + (opcional) deploy

---

## Proyecto 6 — Tablero CRM (pipeline Kanban)

**Idea:** oportunidades o deals por etapas; arrastrar entre columnas; detalle lateral o modal; notas. Enfoque “pipeline”, no lista de tareas del día.

**Qué demuestra:** DnD con reglas, persistencia mock, sensación de producto interno.

**React / frontend:** librería DnD (p. ej. `@dnd-kit`), estado inmutable, restricciones por etapa si las defines en el brief.

**MVP:** columnas + mover tarjetas + detalle + notas.

**Plus:** timeline de actividad simulada al cambiar etapa.

**Carpeta sugerida:** `new-learning-path/p06-kanban-crm/`

**Checklist cierre MVP:**

- [ ] Brief: reglas de qué puede moverse a dónde
- [ ] Persistencia mínima (mock recargable o local)
- [ ] README + (opcional) deploy

---

## Proyecto 7 — Constructor de presupuestos / cotizaciones

**Idea:** líneas de ítem, impuestos o descuentos, totales, plantillas; salida PDF desde navegador o vista de impresión profesional.

**Qué demuestra:** lógica de negocio en UI, formato, impresión; muy distinto a CRUD genérico.

**React / frontend:** estado complejo ordenado, totales como derivados, formularios repetibles.

**MVP:** una plantilla + líneas editables + total correcto + PDF o print view.

**Plus:** versiones guardadas en `localStorage`.

**Carpeta sugerida:** `new-learning-path/p07-presupuestos/`

**Checklist cierre MVP:**

- [ ] Brief: redondeo de decimales y división por cero / líneas vacías
- [ ] Print/PDF usable
- [ ] README + (opcional) deploy

---

## Proyecto 8 — Micro-SaaS: landing + app demo

**Idea:** landing (pricing, FAQ) + “login” simulado + área cuenta con 2–3 pantallas coherentes y datos mock.

**Qué demuestra:** marketing + producto; madurez de presentación.

**React / frontend:** layouts distintos (marketing vs app), rutas “protegidas” falsas, empty states.

**MVP:** landing + flujo demo + dashboard mínimo.

**Plus:** tema claro/oscuro y tipografía consistente.

**Carpeta sugerida:** `new-learning-path/p08-micro-saas-demo/`

**Checklist cierre MVP:**

- [ ] Brief: qué significa “login simulado” (sin seguridad real) y límites
- [ ] Coherencia visual entre landing y app
- [ ] README + (opcional) deploy

---

## Resumen rápido (tabla de una página)

| # | Nombre | Idea en una línea | Enfoque React clave |
|---|--------|-------------------|---------------------|
| 1 | Dashboard | KPIs + tabla + filtros mock | Estado derivado, tabla densa |
| 2 | Catálogo B2B | Grid + comparador + formulario presupuesto | Forms, rutas, selección |
| 3 | Agenda evento | Tracks, favoritos, solapes | Modelo de datos, reglas UI |
| 4 | API explorer | Buscar + detalle + guardados | Fetch, errores, URL state |
| 5 | Markdown guías | Índice + lectura + búsqueda | Slugs, MD, rendimiento |
| 6 | Kanban CRM | Pipeline con DnD | DnD, estado inmutable |
| 7 | Presupuestos | Líneas + totales + print/PDF | Estado complejo, derivados |
| 8 | Micro-SaaS demo | Landing + app fake auth | Layouts, flujo producto |

---

## Documentos relacionados

- Plantilla de briefing: `new-learning-path/PROJECT_BRIEF_TEMPLATE.md`

Cuando quieras arrancar el siguiente proyecto, abre un `BRIEF.md` en su carpeta y seguimos con la ronda de preguntas de planificación antes del código.
