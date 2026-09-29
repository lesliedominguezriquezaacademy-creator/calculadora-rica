# PROJECT STATUS

Última actualización: 2026-09-29 (sesión de inicialización del Master Agent)

## Fase actual

**Fase 1 — Calculadora RICA v2 en revisión.** `calculadora-rica-v2.html` está construida en la rama como copia aparte. La versión publicada (`calculadora-app.html`) no cambió.

**Decisión D-008 (Leslie, 2026-09-29):** este repo = calculadora (lead magnet). Riqueza App = repo nuevo, pendiente de crear.

Dos líneas de trabajo:
1. **Calculadora (este repo):** rediseño conceptual propuesto (`docs/proposals/CALCULATOR_REDESIGN_v1.md`), concepto aprobado con cambios (Q9); la versión breve v1.2 está pendiente de visto bueno para implementar (Q14). El rediseño resolvería KI-03 a KI-08, KI-10 y KI-16.
2. **Riqueza App (repo nuevo):** bloqueada por Q2 (documento rector) y Q7 (creación del repo).

## Estado verificado del repositorio

Repositorio: `lesliedominguezriquezaacademy-creator/calculadora-rica`
Ramas: `main` (única rama remota antes de esta sesión) y `claude/riqueza-master-agent-setup-atbcvj` (esta sesión).

Contenido de `main` (commit `b850794`, 2026-09-17):

| Archivo | Descripción |
|---|---|
| `calculadora-app.html` | Único archivo del proyecto. 1,245 líneas, ~63 KB. HTML + CSS + JS vanilla en un solo archivo. |

No existe en `main`:

- `CLAUDE.md` (Leslie lo suministró por chat en esta sesión; se agregó en esta rama)
- `docs/RIQUEZA_APP_MASTER_AGENT_PROJECT_v1.md` (**no existe en ninguna rama ni en el historial de git**)
- README (existió en el commit inicial y fue borrado en `20a8ac5`)
- `package.json`, dependencias, build, tests, CI, configuración de despliegue, backend, base de datos, variables de entorno

## Qué es `calculadora-app.html` (verificado leyendo el código)

Lead magnet estático: **"¿Cuánto te cuesta NO actuar? — Diagnóstico de Valor, Riqueza Academy™"**, en español.

- Flujo de 5 pasos: Perfil → Situación → Mentalidad → Bloqueos → Resultado.
- Entradas: género de trato, años de experiencia, área, tarifa por hora, horas vendidas/semana, horas disponibles, valor percibido por hora, modelo de cobro, identidad, bloqueos.
- Salidas: "costo mensual de inacción", ROI del Método Rica IA™ (precio fijo en código: `$297`), línea de tiempo 0–24 meses, texto de diagnóstico personalizado.
- CTA único: abre `https://lesliedominguezriquezaacademy.systeme.io/calculadora-optin` (Masterclass gratuita, fecha calculada como "tercer miércoles del mes", 7 PM EST).
- Animación canvas de "lluvia de dinero" en el hero.
- Sin backend, sin almacenamiento, sin analítica, sin captura de email propia (un paso de captura "4.5" existió y fue eliminado en `40db451`; su CSS quedó huérfano).
- Dependencia externa única: Google Fonts (Cormorant Garamond, Jost).

## Relación con el proyecto "Riqueza App" descrito en CLAUDE.md

**CONFLICT DETECTED** — ver `OPEN_QUESTIONS.md` Q1 y `KNOWN_ISSUES.md` KI-01.

CLAUDE.md describe una aplicación completa (backend, Riqueza AI Service, MockAIProvider, onboarding, perfil, diagnóstico, dashboard, progreso). Este repositorio contiene solo una calculadora estática de captación. Ninguno de los componentes de arquitectura de CLAUDE.md existe aquí.

## Hosting / despliegue

Desconocido. No hay evidencia en el repositorio de dónde se publica la calculadora (ver `OPEN_QUESTIONS.md`).

## Bloqueadores

1. Calculadora: revisión de la v2 por Leslie; Q10 (mensaje de la Masterclass) y Q11 (lluvia de dinero) antes de publicar; Q3 (hosting) antes del merge.
2. Riqueza App: falta `docs/RIQUEZA_APP_MASTER_AGENT_PROJECT_v1.md` (Q2) y el repo nuevo (Q7).
