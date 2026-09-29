# DECISIONS

Registro de decisiones materiales. Formato: ID · fecha · decisión · quién decidió · fuente.

Solo se registran decisiones **explícitas** de Leslie o documentadas. Las propuestas del agente van en `OPEN_QUESTIONS.md` hasta ser aprobadas.

## Decisiones vigentes (tomadas de CLAUDE.md, suministrado por Leslie el 2026-09-29)

| ID | Fecha | Decisión | Decidió | Fuente |
|---|---|---|---|---|
| D-001 | 2026-09-29 | GitHub es la fuente de verdad técnica canónica. | Leslie | CLAUDE.md §1, §4 |
| D-002 | 2026-09-29 | La memoria del proyecto vive en `docs/project-memory/`. | Leslie | CLAUDE.md §5 |
| D-003 | 2026-09-29 | La IA se consume vía capa de abstracción; prototipo con `MockAIProvider`. OpenRouter solo después, nunca desde el frontend; llaves solo en servidor. | Leslie | CLAUDE.md §6 |
| D-004 | 2026-09-29 | No conectar OpenRouter todavía. | Leslie | Instrucción de sesión 2026-09-29 |
| D-005 | 2026-09-29 | Prioridades del MVP: onboarding → perfil → diagnóstico → análisis → activos → cuellos de botella → ruta → dashboard → siguiente acción → progreso. Excluidos: marketplace, CRM, red social, ecosistema de agentes, automatización compleja, entrenamiento de modelos. | Leslie | CLAUDE.md §7 |
| D-006 | 2026-09-29 | No implementar hasta alinear el plan con Leslie. | Leslie | CLAUDE.md §8 |

## Decisiones de la sesión de inicialización (agente, de bajo impacto y reversibles)

| ID | Fecha | Decisión | Motivo |
|---|---|---|---|
| D-007 | 2026-09-29 | `CLAUDE.md` suministrado por chat se versiona en la raíz del repo, en la rama de trabajo (no en `main`). | Cumplir D-001 (GitHub como fuente de verdad). Reversible: no se fusiona a `main` hasta resolver Q1. |
