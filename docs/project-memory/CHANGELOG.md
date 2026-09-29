# CHANGELOG

Cambios materiales del repositorio. Más reciente arriba.

## 2026-09-29 — Calculadora RICA v2 (copia aparte, rama `claude/riqueza-master-agent-setup-atbcvj`)

- Nuevo archivo `calculadora-rica-v2.html`, que implementa la propuesta v1.2. `calculadora-app.html` **no se modificó**.
- Mismo CSS, botones y animación del hero de la versión actual (D-015). Son 4 pasos y 9 respuestas (D-016).
- Horas por semana con leyenda "Recomendado: 4–6 horas por semana" (D-014).
- Se eliminan los multiplicadores, el ROI, el precio de $297, la línea de tiempo, "10 ventas" y los nombres ficticios.
- Resultado: activos, cálculo con los datos de la persona, posibilidad con plan de 4 pasos, escenario editable con fórmulas visibles y aviso fijo.
- Correcciones incluidas: la fecha de la Masterclass incluye el mismo día (KI-12) y usa "ET"; copiar tiene alternativa si falla (KI-13); navegación con teclado (KI-14, parcial); respeta `prefers-reduced-motion`.

## 2026-09-29 — Inicialización del Master Agent (rama `claude/riqueza-master-agent-setup-atbcvj`)

- Agregado `CLAUDE.md` (suministrado por Leslie en chat).
- Creada `docs/project-memory/` con PROJECT_STATUS, DECISIONS, OPEN_QUESTIONS, CHANGELOG, KNOWN_ISSUES, SESSION_LOG.
- Registrada decisión D-008 (calculadora y Riqueza App en repos separados).
- Registrada decisión D-009 (nueva dirección de la calculadora).
- Agregada propuesta `docs/proposals/CALCULATOR_REDESIGN_v1.md` (no aprobada).
- Propuesta actualizada a v1.1: horas del piloto elegidas por la persona (D-010) y rango sugerido por tipo (D-011).
- Propuesta v1.2: versión breve (4 pasos, 9 respuestas, horas por semana con leyenda de recomendado). Registradas D-013 a D-016.
- Sin cambios en `calculadora-app.html`.

## Historial previo reconstruido desde git (2026-09-17, todo vía "upload" en GitHub web)

- `f69f5bc` Commit inicial con README.
- `d6e7c8f` Primera versión de `calculadora-app.html` (1,391 líneas).
- `20a8ac5` README eliminado.
- `31f928f` Nueva versión (1,314 líneas).
- `40db451` Nueva versión (1,245 líneas): se elimina el paso 4.5 de captura de email (bonus "Riqueza Interna™") y se rediseña el CTA.
- `b850794` CTA cambia de registro Zoom a `lesliedominguezriquezaacademy.systeme.io/calculadora-optin`.
