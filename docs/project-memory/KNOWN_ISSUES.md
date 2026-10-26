# KNOWN ISSUES

**Actualización 2026-10-26:** los KI-03 a KI-16 describen la **versión original (v1, commit `b850794`)**, que ya no está en `main`: la v3 la reemplazó el 2026-09-30. En la v3 se verificó que ya no existen el ROI, `$297`, los avatares "María Elena"/"Carlos", "10 ventas" ni la línea de tiempo (KI-03, KI-04), y que respeta `prefers-reduced-motion`. El resto de los KI de v1 no se ha re-auditado contra la v3 línea por línea. Severidad: Alta / Media / Baja.

## Proyecto / documentación

- **KI-01 · RESUELTO por D-008.** Conflicto de alcance repo ↔ CLAUDE.md. Pendiente residual: mover `CLAUDE.md` al repo nuevo (Q8).
- **KI-02 · Alta · Documento rector ausente.** `docs/RIQUEZA_APP_MASTER_AGENT_PROJECT_v1.md` no existe. Ver Q2.

## Calculadora — riesgos de negocio/ética

- **KI-03 · Alta · Proyecciones de ingresos sin respaldo.** "ROI", "Potencial año 1" y la línea de tiempo salen de multiplicadores arbitrarios (`AREA_MULT`, `expFact`, `factHoras`, ×2.8 a 24 meses) — líneas 941–957, 1000–1006. El texto afirma "Estimado conservador" y "recuperar la inversión con un solo producto digital y 10 ventas" (línea 1019) sin evidencia. Riesgo reputacional y regulatorio (reglas de la FTC sobre declaraciones de ingresos en EE. UU.; aplicable si el público es estadounidense — a confirmar).
- **KI-04 · Media · Nombre de persona ficticio mostrado al usuario.** El título del resultado usa `g.avatar`: a toda usuaria "Ella" le dice "María Elena, cada mes que esperas…", a todo usuario "Él" le dice "Carlos" (líneas 746, 751, 961).

## Calculadora — bugs lógicos

- **KI-05 · Media · El paso 4 (Bloqueos) no afecta el resultado.** `D.bloqueo_costo` se calcula (línea 931) pero nunca se usa, aunque la UI dice "Esto determina el costo real de tu inacción".
- **KI-06 · Media · `modelo` (forma de cobro) e `ingreso` no se usan en el resultado.**
- **KI-07 · Media · El "costo mensual" ignora el valor por hora que ingresó el usuario (paso 3).** Se calcula con la tarifa pagada × multiplicadores × horas disponibles (línea 951); la brecha de valor del paso 3 solo aparece como dato secundario.
- **KI-08 · Media · Valores por defecto silenciosos.** Los botones "Siguiente" siempre están activos; si el usuario no elige, se usan género `f`, área `negocios`, identidad `emplead`, horas `5` sin que la UI los muestre seleccionados.
- **KI-09 · Baja · Días de break-even inconsistentes.** El breakdown usa `Math.ceil` (línea 984) y el insight `Math.round` (línea 1018) → pueden mostrar números distintos.
- **KI-10 · Baja · Texto con género fijo.** "Las líderes que deciden actuar…" (línea 1021) se muestra aunque se elija "Él" o "Neutro".
- **KI-11 · Baja · `reset()` no restablece etiquetas de género** ni el `--pct` visual de los sliders.
- **KI-12 · Baja · Fecha de Masterclass.** El día de la Masterclass salta al mes siguiente (`f > hoy`, línea 1068); usa "EST" aunque en horario de verano aplica EDT; la zona horaria del visitante no se considera.
- **KI-13 · Baja · `copiar()` no maneja error** si el portapapeles no está disponible.

## Calculadora — calidad técnica

- **KI-14 · Media · Accesibilidad.** Opciones y checks son `div` con `onclick` (sin teclado ni roles ARIA); slider estilizado solo para WebKit; animación sin `prefers-reduced-motion`.
- **KI-15 · Baja · Rendimiento.** La animación canvas corre indefinidamente aunque el hero no esté visible.
- **KI-16 · Baja · CSS huérfano** del paso de captura eliminado (`.capture-*`, `.rpb-*`, `.lock-badge`, líneas 281–444).
- **KI-17 · Media · Sin analítica.** No hay forma de medir completitud del embudo ni clics en el CTA; el resultado no se envía con el lead a systeme.io.
- **KI-18 · Baja · Sin tests, sin README, sin control de versiones local** (cambios subidos manualmente por la web de GitHub).

## Calculadora v2 — observaciones (históricas: la v2 se eliminó; revisar si aplican a la v3)

- **KI-19 · Baja.** Con tarifa alta y precio bajo, el punto de equilibrio puede ser poco realista (p. ej. 390 clientes al mes). Es aritmética correcta y la nota invita a probar otro precio, pero se podría agregar una sugerencia explícita.
- **KI-20 · Media.** El texto del CTA ya no promete "primer producto digital en 28 días", pero sigue pendiente confirmar qué cubre la Masterclass (Q10). "Cupos limitados" se mantuvo del original sin verificar.
- **KI-21 · Baja.** Horas por semana por botón: 2 / 5 / 9 / 12 (la versión original usaba 2 / 5 / 10 / 20). Se muestran como aproximadas.

## Calculadora v3 (en `main`) — abiertas

- **KI-22 · Media.** Sigue la animación "lluvia de dinero" en el hero (Q11).
- **KI-23 · Media.** Sigue "Cupos limitados" en el CTA sin verificar (Q10).
- **KI-17 sigue vigente:** sin analítica.
- **KI-24 · Baja.** La v3 no ha tenido una auditoría completa de fórmulas y copy como la que se hizo a la v1; solo una prueba de humo en el navegador.
