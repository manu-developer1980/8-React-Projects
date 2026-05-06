# Briefing de proyecto (plantilla)

Copia este archivo por proyecto: `new-learning-path/<nombre-proyecto>/BRIEF.md` y rellénalo **antes** de escribir código de producto.  
Objetivo: cerrar alcance, decisiones y **casos límite**; no buscar perfección el día 1.

---

## 1. Resumen en una frase

**Qué existe al final (resultado verificable):**  
_(Una oración. Si no cabe en una línea, el alcance es demasiado grande.)_

---

## 2. Contexto y motivación

- **Problema / oportunidad:**
- **Para quién** (usuario o “yo como aprendizaje”):
- **Por qué ahora** (deadline, portfolio, bloque del curso):

---

## 3. Historias de usuario (máximo 4 para el MVP)

Formato: *Como … quiero … para …*

| # | Historia | Criterio de aceptación (medible) |
|---|----------|----------------------------------|
| 1 |          |                                  |
| 2 |          |                                  |
| 3 |          |                                  |
| 4 |          |                                  |

**Fuera de alcance (explícito):**  
_(Lista corta: qué NO harás en esta iteración.)_

---

## 4. Flujos críticos (boceto mental)

Describe **2–3** caminos: inicio → decisión → fin.

1. Flujo principal (feliz):
2. Flujo secundario:
3. (Opcional) Flujo “vuelvo atrás” / cancelar:

Si un flujo no “cierra” (el usuario no llega a un estado final claro), recorta alcance.

---

## 5. Datos y contratos

- **Origen de datos:** mock estático / JSON local / API pública / backend propio.
- **Entidades principales** (nombres + relación en una línea cada una):

| Entidad | Campos mínimos | Notas |
|---------|----------------|--------|
|         |                |        |

- **Validación:** qué campos son obligatorios, formatos, límites (longitud, rangos).

---

## 6. Estados de UI (obligatorio revisar)

Para **cada** pantalla o bloque importante, marca qué aplica:

| Pantalla / bloque | Vacío (sin datos) | Cargando | Error | Éxito |
|-------------------|-------------------|----------|-------|-------|
|                   |                   |          |       |       |

---

## 7. Edge cases y límites (no saltar esta sección)

Rellena con honestidad. “No aplica” solo si es verdad.

### 7.1 Datos y red

| Situación | Comportamiento esperado | ¿En MVP? |
|-----------|-------------------------|----------|
| Lista vacía | | sí / no |
| Respuesta vacía pero 200 | | |
| Error de red / timeout | | |
| Respuesta no esperada (forma distinta) | | |
| Reintento manual vs automático | | |

### 7.2 Entrada del usuario

| Situación | Comportamiento esperado | ¿En MVP? |
|-----------|-------------------------|----------|
| Campos vacíos / submit sin datos | | |
| Input demasiado largo | | |
| Caracteres raros / espacios | | |
| Doble click / doble submit | | |
| Pegar texto enorme | | |

### 7.3 Concurrencia y navegación

| Situación | Comportamiento esperado | ¿En MVP? |
|-----------|-------------------------|----------|
| Usuario navega fuera mientras carga | | |
| Vuelve atrás con datos “a medias” | | |
| Refresco en mitad de un flujo | | |
| URL directa a una vista que necesita contexto | | |

### 7.4 Rendimiento y límites de producto

| Situación | Comportamiento esperado | ¿En MVP? |
|-----------|-------------------------|----------|
| Muchos ítems en lista (100, 1000) | | |
| Búsqueda / filtro lento | | |

### 7.5 Accesibilidad mínima (ajusta a tu MVP)

| Situación | Comportamiento esperado | ¿En MVP? |
|-----------|-------------------------|----------|
| Teclado solo (Tab, Enter, Escape) | | |
| Focus visible en controles | | |
| Errores de formulario anunciados / legibles | | |

---

## 8. Decisiones técnicas (tradeoffs)

Por cada decisión importante: **opción elegida**, **alternativa descartada**, **por qué**, **coste**.

| Decisión | Elegido | Alternativa | Por qué | Coste asumido |
|----------|---------|-------------|---------|-----------------|
|          |         |             |         |                 |

---

## 9. Riesgos e incógnitas

| Riesgo / duda | Impacto si ocurre | Mitigación (MVP) |
|---------------|-------------------|------------------|
|               |                   |                  |

**Spikes permitidos** (máx. tiempo, p. ej. 90 min):  
_(Solo para incógnitas que bloquean: librería, API, DnD, etc.)_

---

## 10. Hitos (entrega incremental)

1. **Vertical slice mínimo** (un flujo feo pero completo: UI + datos + navegación si aplica):
2. Pulido de estados (vacío / error / carga):
3. Edge cases priorizados de la sección 7:
4. README + deploy (si aplica):

---

## 11. Definition of Done (checklist)

Marca al cerrar el MVP:

- [ ] Flujo principal de la tabla de historias cumple criterios de aceptación
- [ ] Estados vacío / carga / error cubiertos donde definiste “sí” en MVP
- [ ] Al menos los edge cases marcados “sí en MVP” tienen comportamiento definido (aunque sea mensaje + acción)
- [ ] `README`: problema, alcance, cómo arrancar, decisiones clave
- [ ] Build (y lint/typecheck si existen en el proyecto) sin errores nuevos
- [ ] (Opcional) URL de demo desplegada

---

## 12. Preguntas abiertas

_(Lo que falta decidir; no empezar bloques grandes hasta resolver o acotar “deferido”.)_

---

# Anexo: preguntas de apertura (antes de codificar)

Quien te acompañe en el proyecto puede usar esta lista para **revisar** tu briefing y señalar lagunas.

### Alcance y valor

1. ¿Qué puede hacer el usuario el día del entregable que **no** podía antes?
2. ¿Qué tres cosas quedan **fuera** a propósito?
3. ¿Cuál es el **único** flujo que si falla el proyecto “no cuenta”?

### Datos y errores

4. ¿De dónde salen los datos el primer día: mock, archivo, API?
5. Si la red falla, ¿qué ve el usuario y qué puede hacer después?
6. Si la lista está vacía, ¿es un bug o un estado válido? ¿Cómo se comunica?

### Comportamiento y límites

7. ¿Qué pasa con doble submit, doble click en “guardar”, o enviar dos veces seguidas?
8. ¿Hay límites de tamaño (texto, número de ítems) que debamos definir ya?
9. ¿Qué debe pasar si el usuario recarga o entra por URL en mitad de un flujo?

### Técnica y mantenimiento

10. ¿Qué decisión técnica te costaría más **defender en una entrevista** si no la escribes aquí?
11. ¿Qué parte es “spike” y cuánto tiempo máximo le das?

Cuando rellenes el briefing, **vuelve a la sección 7** al menos una vez después de definir flujos: suele aparecer ahí lo que antes se te pasaba.
