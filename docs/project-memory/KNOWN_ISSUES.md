# KNOWN ISSUES

Problemas verificados leyendo el código (`calculadora-app.html`, commit `b850794`). Ninguno ha sido corregido. Severidad: Alta / Media / Baja.

## Proyecto / documentación

- **KI-01 · Alta · Conflicto de alcance.** CLAUDE.md describe Riqueza App; el repo contiene solo la calculadora. Ver Q1.
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
