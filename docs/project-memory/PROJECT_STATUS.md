# PROJECT STATUS

Última actualización: 2026-10-26 (sesión del Master Agent: sincronización con `main`)

## Fase actual

**Fase 1 — Calculadora RICA v3 en `main`.** La v3 reemplazó a la versión original en `calculadora-app.html` el 2026-09-30, desde otra sesión de Claude Code (commits `0e17648`, `575610b`, `3ff6234`).

Este repo es solo la calculadora (lead magnet), según D-008. Riqueza App irá en un repo nuevo, todavía sin crear.

## Estado verificado del repositorio (2026-10-26)

| Archivo | Estado |
|---|---|
| `calculadora-app.html` | **Calculadora RICA v3.** 1,348 líneas. Un solo HTML con CSS y JS vanilla, CSP estricta, sin backend ni cookies. |
| `README.md` | Descripción del repo (agregado el 2026-09-30). |
| `CLAUDE.md` | Entrypoint del Master Agent (en esta rama, pendiente de unirse a `main`). |
| `docs/project-memory/` | Memoria del proyecto (en esta rama, pendiente de unirse a `main`). |
| `docs/proposals/CALCULATOR_REDESIGN_v1.md` | Propuesta histórica que sirvió de base para v2 y v3. |

Ya no existe `calculadora-rica-v2.html`: se eliminó porque la v3 en `main` la reemplazó.

### Qué hace la v3 (verificado en el navegador el 2026-10-26)

- **4 pasos + resultado:**
  - Perfil: trato, años de experiencia y área.
  - Lo que ya tienes: activos, talentos y dones, formas de aportar.
  - Tu tiempo: tarifa actual, valor estimado y horas por semana, con la leyenda "Recomendado: 4–6 horas por semana".
  - Posibilidades.
- **Catálogo de 5 opciones:** coaching grupal, infoproducto, consultoría, taller y evento.
- **Resultado:**
  - "No empiezas desde cero" con los activos de la persona.
  - Cálculo con sus datos.
  - Hora convertida por opción, "del uno a uno al grupo" y guía de estructuras de precio.
  - Plan del piloto en 4 pasos.
  - Simulador editable.
  - Aviso fijo: no es una promesa de ingresos y las cifras son brutas.
- **CTA:** Masterclass gratuita en systeme.io.
- **Prueba (Chromium, 390 px):** el flujo completo llega al resultado, sin errores de JS y sin scroll horizontal.
- **Ya no aparecen:** ROI, `$297`, "María Elena", "10 ventas" ni "primer producto digital en 28 días".

## Hosting / despliegue

Desconocido (Q3). No hay configuración de hosting en el repo.

## Coordinación entre agentes

Leslie usa **Codex** como centro de comando y revisión, y **Claude Code** para ejecutar. Según Leslie, los roles ya se corrigieron, pero en este repo no existe `AGENTS.md` ni otra definición de roles visible (Q16). `CLAUDE.md` todavía describe a Claude Code como "Master Agent / Orchestrator".

## Bloqueadores y pendientes

1. Unir esta rama a `main` para que la memoria sea compartida (revisión de Codex/Leslie).
2. Calculadora: Q10 (mensaje de la Masterclass), Q11 (lluvia de dinero, sigue en la v3), Q3 (hosting), KI-17 (sin analítica).
3. Riqueza App: Q2 (documento rector) y Q7 (repo nuevo).
4. Roles entre agentes: Q16.
