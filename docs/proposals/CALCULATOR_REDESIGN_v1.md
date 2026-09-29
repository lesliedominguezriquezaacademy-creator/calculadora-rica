# CALCULATOR REDESIGN — v1 (PROPUESTA, NO APROBADA)

Estado: **Borrador para aprobación de Leslie.** No implementado.
Fecha: 2026-09-29
Base analizada: `calculadora-app.html` @ `b850794`
Origen: instrucción de Leslie del 2026-09-29 (ver `docs/project-memory/DECISIONS.md` D-009).

Nombre de trabajo: **Mapa de Valor · 10 Horas** (a confirmar).

---

## 1. Current experience (verificado en el código)

### Flujo actual

| Paso | Pantalla | Qué pregunta |
|---|---|---|
| Hero | "¿Cuánto te cuesta *no actuar hoy*?" + animación de lluvia de dinero | — |
| 1 · Perfil | Género del trato (f/m/n), años de experiencia (5–30), área (6 opciones) | |
| 2 · Situación | Tarifa por hora ($5–150), horas/semana para otros (5–50), horas propias disponibles (4 rangos) | |
| 3 · Mentalidad | Valor estimado de su hora de conocimiento ($20–500), forma de cobro (4), identidad (4) | |
| 4 · Bloqueos | 7 casillas (multi-selección) | |
| 5 · Resultado | "{María Elena/Carlos/Profesional}, cada mes que esperas, este es tu costo real" | |
| CTA | Masterclass gratuita → systeme.io, fecha = tercer miércoles | |

### Variables: introducidas por el usuario vs. supuestos internos

**Introducidas por el usuario**

| Variable | Rango | ¿Se usa en el resultado? |
|---|---|---|
| `genero` | f / m / n | Solo en el copy (y en el nombre ficticio del avatar) |
| `anos` | 5–30 | Sí, dentro de `expFact` |
| `area` | 6 opciones | Sí, dentro de `AREA_MULT` |
| `tarifa` | $5–150/h | Sí |
| `hotro` | 5–50 h/sem | Sí |
| `horas` (propias) | 2 / 5 / 10 / 20 (puntos medios de rangos) | Sí |
| `valor` | $20–500/h | Solo en la brecha secundaria |
| `modelo` | hora / proyecto / salario / mixto | **No** (solo un mensaje en pantalla) |
| `identidad` | 4 opciones | Solo en el copy |
| `bloqueos` | 7 casillas con un "costo" oculto cada una | **No** (`bloqueo_costo` nunca se usa) |

**Supuestos internos (sin fuente documentada)**

| Supuesto | Valor | Línea |
|---|---|---|
| `AREA_MULT` | salud 1.3, negocios 1.5, educación 1.2, creatividad 1.1, tech 1.4, otro 1.1 | 763 |
| `expFact` | 1 + (años/30) × 0.8 | 942 |
| Semanas/mes | 4.3 | 854, 951 |
| `factHoras` (tasa de "conversión") | 15 % / 30 % / 45 % / 60 % según horas | 954 |
| `PRECIO` del Método Rica IA™ | $297 | 948 |
| Crecimiento con RICA | 30 % a 6 meses, 100 % a 12 meses, ×2.8 a 24 meses | 1003–1005 |
| Costos por bloqueo | $900–2,500 cada uno (no se usan) | 661–667 |
| "10 ventas" | texto fijo | 1019 |

### Fórmulas actuales

```
salario_mensual   = tarifa × hotro × 4.3                          ← cálculo limpio
brecha_anual      = max(0, valor − tarifa) × hotro × 52           ← cálculo limpio (sobre una estimación del usuario)
costo_mes         = tarifa × AREA_MULT × expFact × horas × 4.3    ← mezcla de dato y supuesto arbitrario
costo_año         = costo_mes × 12
ganancia_año1     = costo_año × factHoras                          ← supuesto arbitrario
ROI               = ganancia_año1 / 297                            ← supuesto arbitrario
break-even (días) = 297 / costo_mes × 30   (ceil en una tarjeta, round en otra)
línea de tiempo   = costo_mes × {3,6,12,24}  vs  ganancia_año1 × {0, .3, 1, 2.8}
% tiempo vendido  = hotro / (hotro + horas)
```

### Copy actual que expresa el problema de Q4

- "Dinero que dejas sobre la mesa cada mes" (sobre `costo_mes`)
- "ROI del Método Rica IA™ en tu caso" / "retorno sobre la inversión en 12 meses"
- "Potencial año 1 · Estimado conservador con el Método RICA™"
- "Con RICA™ · potencial año 1" (tarjeta de decisión)
- Línea de tiempo "Sin actuar / Con RICA™"
- "Break-even del curso · Días de inacción que cuestan lo mismo que el Método Rica IA™"
- "El Método Rica IA™ no cuesta $297. Te cuesta N días de inacción… con un solo producto digital y 10 ventas"
- "Eso no es un juicio. Es matemática."
- "Lo que pierdes al año · alguien más captura esto"
- "{hotro}h/semana trabajan para el sueño de alguien más"
- "Las líderes que deciden actuar…" (sin importar el género)
- Título con nombre ficticio: "María Elena, …" / "Carlos, …"

---

## 2. Problem with current approach

1. **Presenta supuestos como si fueran matemática.** El número principal (`costo_mes`) depende de multiplicadores inventados. El texto dice "Es matemática".
2. **Promete resultados.** ROI, "potencial año 1", "estimado conservador" y "10 ventas" son afirmaciones de ingreso sin evidencia.
3. **Una sola ruta.** Todo lleva a "producto digital / Método RICA", en contra de la filosofía KNOWLEDGE + EXPERIENCE + ASSETS → VALUE → OFFER…
4. **Culpa en lugar de posibilidad.** El marco "cuánto te cuesta no actuar" y "el sueño de alguien más" trabajan con miedo a la pérdida. Funciona para convertir a corto plazo, pero desgasta una marca que se presenta como de riqueza con propósito.
5. **Preguntas que no hacen nada.** Bloqueos y forma de cobro no afectan el resultado, aunque la pantalla diga que sí.
6. **No descubre nada.** No le muestra a la persona qué activos ya tiene ni qué podría construir con ellos.

---

## 3. New concept

**Pregunta central:**
> ¿Qué podrías crear con lo que ya sabes si decidieras invertir 10 horas en convertirlo en una oportunidad?

**Promesa de la experiencia (no de ingresos):** en 5 minutos la persona sale con:

1. Un **inventario de sus activos**: "No empiezo desde cero".
2. Su **hora de referencia** actual: un cálculo con sus propios datos.
3. **3 posibilidades** de proyecto que encajan con sus activos y preferencias, sin imponer una sola ruta.
4. Un **plan de 10 horas** para una versión piloto de la posibilidad que elija.
5. Un **escenario económico editable**, con sus propios supuestos a la vista, separado del cálculo.

**Principios de diseño**

- *Cálculo* = solo datos de la persona. *Escenario* = supuestos que la persona ve y puede mover. Se distinguen visualmente.
- Ninguna cifra sin su fórmula visible.
- Ningún número fijo que no venga de una variable ("10 ventas" pasa a ser "unidades necesarias para recuperar tus 10 horas", calculado).
- El objetivo de las 10 horas es **validar**, no "lanzar un negocio".

**Encaje con la filosofía de Riqueza App**

| Etapa | Dónde aparece en la calculadora |
|---|---|
| KNOWLEDGE + EXPERIENCE + ASSETS | Paso 1: inventario |
| VALUE | Paso 2: tu hora hoy + valor estimado |
| OFFER | Pasos 3–4: posibilidades y elección |
| BUSINESS | Paso 5: escenario + plan de 10 h |
| EXPANSION → IMPACT → LEGACY | Se mencionan como horizonte en el cierre; no se calculan |

---

## 4. User inputs

Objetivo: no más de 12 respuestas en total, 5 pasos, unos 5 minutos.

| # | Paso | Input | Tipo | Uso |
|---|---|---|---|---|
| U1 | 1 | Cómo prefieres que te hablemos (ella / él / neutro) | selección | Copy |
| U2 | 1 | Años de experiencia | slider 1–40 | Copy + afinidad (licencia/metodología pide más experiencia) |
| U3 | 1 | Área | chips (6, las actuales) | Copy |
| U4 | 1 | Tema en una frase (opcional). Ej.: "nutrición para personas con diabetes" | texto, máx. 80 caracteres | Copy del resultado (se inserta con `textContent`, nunca con `innerHTML`) |
| U5 | 1 | **Activos que ya tienes** | multi-selección (8) | Inventario + afinidad |
| U6 | 2 | Cuánto recibes hoy por hora | slider $5–200 | Cálculo |
| U7 | 2 | Horas por semana que trabajas para otros | slider 0–60 | Cálculo |
| U8 | 2 | Cuánto crees que vale una hora de tu conocimiento para quien lo recibe | slider $10–500 | Cálculo (brecha) + precio de referencia |
| U9 | 2 | Horas por semana que podrías dedicar a esto | 4 rangos (mantener) | Cálculo (semanas para completar 10 h) |
| U10 | 3 | Cómo te gusta aportar valor | multi-selección (5) | Afinidad |
| U11 | 3 | Cuánto de tu presencia quieres que requiera | alta / media / baja | Afinidad |
| U12 | 3 | Qué te ha frenado (mantener, opcional) | multi-selección (7 actuales) | Se refleja en el plan de 10 h, **sin costo en dinero** |

**Activos (U5)**
1. Experiencia práctica resolviendo un problema concreto
2. Me piden consejo sobre esto con frecuencia
3. Tengo un proceso o método propio (aunque no esté escrito)
4. Tengo casos o resultados que puedo mostrar
5. Tengo materiales ya creados (plantillas, presentaciones, guías, notas)
6. Tengo una red de contactos que confía en mí
7. Tengo audiencia (redes, lista de correo, comunidad)
8. Tengo credenciales o certificaciones en el tema

**Formas de aportar valor (U10):** uno a uno · en grupo · escribiendo o creando contenido · en vivo / eventos · para organizaciones o empresas.

**Inputs del escenario (en la pantalla de resultado, editables):**
- S1 Posibilidad elegida
- S2 Precio por unidad
- S3 Unidades (clientes / participantes / copias / miembros / licencias)
- S4 Horas de entrega (por unidad, edición o mes, según el tipo)

---

## 5. Calculation logic

### A. Cálculos (solo con datos de la persona)

```
C1  ingreso_mensual_actual   = U6 × U7 × 4.33             (52 semanas / 12 meses)
C2  brecha_por_hora          = max(0, U8 − U6)
C3  brecha_anual_estimada    = C2 × U7 × 52               ("según tu propia estimación")
C4  valor_de_tus_10_horas    = 10 × U6                    (costo de oportunidad a tu tarifa actual)
C5  semanas_para_10_horas    = ceil(10 / U9)
```

### B. Escenario (supuestos visibles y editables)

Cuatro familias de fórmula según cómo se entrega cada proyecto:

| Familia | Tipos | Horas de entrega | Ingreso del escenario |
|---|---|---|---|
| **T · Tiempo por cliente** | Servicio, Consultoría, Coaching | S4 × S3 | S2 × S3 |
| **G · Tiempo por edición** | Taller, Programa grupal, Experiencia/evento | S4 (una edición) | S2 × S3 participantes |
| **P · Sin tiempo por unidad** | Producto digital, Ebook/guía, Licenciamiento | S4 soporte total (por defecto bajo) | S2 × S3 |
| **R · Recurrente** | Membresía | S4 por mes | S2 × S3 por mes |

```
E1  ingreso_bruto_escenario   = S2 × S3                               ("antes de costos, comisiones e impuestos")
E2  horas_totales             = 10 (creación) + horas_de_entrega
E3  valor_efectivo_por_hora   = E1 / E2
E4  comparación               = E3 frente a U6                        ("hoy recibes $U6/h")
E5  unidades_de_equilibrio    = ceil(C4 / S2)                         ("unidades para recuperar el valor de tus 10 horas")
E6  sensibilidad              = E3 con S3 × 0.5 · S3 · S3 × 2          ("si fuera la mitad / tu escenario / el doble")
```

**Valores iniciales del escenario (todos anclados a datos de la persona o marcados como supuestos):**

- **Unidades (S3):** empiezan en **E5, el punto de equilibrio**. La primera vista responde "¿qué haría falta para que esas 10 horas valieran lo mismo que a tu tarifa actual?". No es un número inventado de ventas.
- **Precio (S2):**
  - Familia T: U8 × S4. Es tu propio valor estimado por hora multiplicado por las horas de entrega.
  - Familias G, P y R: U6. Es una hora de tu tarifa actual, y se etiqueta "punto de partida, no es una recomendación de precio".
- **Horas de entrega (S4):** valor inicial por tipo, **marcado como supuesto editable** (tabla de la sección 6). *Leslie debe revisar estos valores.*

**Qué se elimina del cálculo:** `AREA_MULT`, `expFact`, `factHoras`, `PRECIO = 297`, ROI, crecimiento ×0.3/×2.8, costos por bloqueo, "10 ventas", "% tiempo vendido".

### C. Afinidad (qué posibilidades mostrar primero)

Es una heurística transparente. **No es un diagnóstico.**

```
puntos(tipo) = 2 × (formas de aportar U10 que coinciden con el tipo)
             + 2 × (si U11 coincide con el nivel de presencia del tipo)
             + 1 × (activos U5 que fortalecen el tipo)
             − 2 × (si falta un requisito clave del tipo, p. ej. Licencia sin método ni casos)
```

- Se muestran las **3 con más puntos**, cada una con su motivo en lenguaje humano ("Encaja porque prefieres enseñar en grupo y ya tienes materiales creados"). Nunca se muestran porcentajes.
- Un enlace "Ver todas las posibilidades" deja elegir cualquiera.

---

## 6. Project possibilities

Catálogo en un único objeto de configuración dentro del HTML, fácil de editar y reutilizable más adelante en Riqueza App.

| Tipo | Familia | Unidad | Presencia | Formas que encajan | Activos que lo fortalecen | Requisito honesto | Horas entrega (supuesto) |
|---|---|---|---|---|---|---|---|
| Servicio especializado | T | cliente | alta | 1:1, organizaciones | experiencia, red, casos | Alguien con el problema, dispuesto a pagar | 5 h/cliente |
| Consultoría | T | cliente | alta | 1:1, organizaciones | experiencia, método, casos, credenciales | Problema de negocio claro | 4 h/cliente |
| Coaching | T | cliente | alta | 1:1 | experiencia, me piden consejo, credenciales | Proceso con inicio y fin | 6 h/cliente (p. ej. 6 sesiones) |
| Taller | G | participante | media | grupo, en vivo | materiales, audiencia, red | Tema acotado, 2–3 h | 3 h/edición |
| Programa grupal | G | participante | media | grupo, en vivo | método, casos, materiales | Resultado definido en semanas | 12 h/edición |
| Producto digital (plantilla, kit, mini-curso) | P | copia | baja | contenido | materiales, método, audiencia | Audiencia o canal de distribución | 2 h de soporte |
| Ebook / guía | P | copia | baja | contenido | materiales, me piden consejo, audiencia | Tema específico | 1 h de soporte |
| Membresía | R | miembro/mes | media | contenido, grupo | audiencia, materiales | Constancia mensual | 4 h/mes |
| Experiencia o evento | G | asistente | alta | en vivo, grupo | red, audiencia | Logística y convocatoria | 8 h/edición |
| Licenciamiento o metodología | P | licencia | baja | organizaciones | método, casos, credenciales, años | **Método probado con resultados** | 3 h/licencia |
| Otro activo de conocimiento | la persona elige familia | la persona define | — | — | — | — | la persona define |

Cada tipo muestra en el resultado:
- Qué es, en una línea.
- "Tu versión piloto en 10 horas" (sección 7).
- "Qué NO se logra en 10 horas".
- Requisito honesto.

---

## 7. 10-hour scenario

Las 10 horas son el eje: **10 horas de trabajo estratégico para convertir un activo en una versión piloto y validarla.** No son para "lanzar un negocio".

**Estructura común (se adapta a cada tipo):**

| Bloque | Horas | Qué se hace | Resultado |
|---|---|---|---|
| 1 · Claridad | 2 h | Para quién es, qué problema resuelve, qué activo usas | 1 frase de oferta |
| 2 · Diseño | 3 h | Formato, alcance, precio de prueba | Descripción de la oferta piloto |
| 3 · Versión mínima | 3 h | Crear lo mínimo para entregarla o mostrarla | Piloto (índice, temario, primera sesión, borrador…) |
| 4 · Validación | 2 h | Presentarla a personas reales de tu red o audiencia | Respuestas reales: sí / no / por qué |

**Piloto por tipo (ejemplos):**
- Servicio / Consultoría: una página de una oferta con alcance y precio, más conversaciones con personas de tu red.
- Coaching: estructura de un proceso de N sesiones y una sesión piloto.
- Taller: temario de 2–3 h y fecha tentativa con lista de interesados.
- Programa: mapa de módulos y primera semana en borrador, con lista de espera.
- Producto digital / Ebook: índice y un capítulo o componente de muestra.
- Membresía: promesa mensual, formato y lista de espera.
- Evento: concepto, formato y convocatoria piloto.
- Licencia: tu método documentado en versión 0 (pasos, criterios, herramientas).

**Personalización con datos de la persona:**
- "A tu ritmo de ~U9 h/semana, son unas **C5 semanas**."
- "Esas 10 horas valen hoy **$C4** a tu tarifa actual." Esto encuadra la inversión con su propio dato.
- Si marcó bloqueos (U12), el bloque que los aborda se resalta. Ej.: "No sé qué precio cobrar" → Bloque 2. "No sé si hay mercado" → Bloque 4.

---

## 8. Proposed copy

### Hero
- Eyebrow: `Riqueza Academy™ · Mapa de Valor`
- Título: **¿Qué podrías crear** *con lo que ya sabes?*
- Sub: Un ejercicio de 5 minutos para ver tu conocimiento y tu experiencia como activos, y explorar qué podrías construir con ellos en **10 horas de trabajo estratégico**.
- Badge: `Gratis · Sin registro · Tus números, tus supuestos`

### Paso 1 · Lo que ya tienes
- Título: Antes de pensar en qué crear, mira lo que ya tienes.
- Activos: ¿Cuáles de estos ya existen en tu vida profesional? *Marca todos los que apliquen. Nadie empieza con todos.*
- Tema: Si tuvieras que resumir en una frase en qué ayudas, ¿qué dirías? *(opcional)*

### Paso 2 · Tu tiempo hoy
- Tarifa: ¿Cuánto recibes hoy por una hora de tu trabajo? *Si tienes salario, divídelo entre las horas reales. Es tu punto de referencia para comparar.*
- Valor: Cuando alguien se beneficia de una hora de tu conocimiento, ¿cuánto crees que vale ese resultado para esa persona? *Es tu estimación. La usaremos como referencia, no como verdad.*
- Horas disponibles: ¿Cuántas horas por semana podrías dedicar a construir algo propio?

### Paso 3 · Cómo te gusta aportar
- Título: No hay una sola forma de convertir conocimiento en valor.
- Sub: Cuéntanos cómo te gusta trabajar. Así te mostramos posibilidades que encajan contigo, no una fórmula única.

### Paso 4 · Tus 10 horas
- Título: Si tuvieras **10 horas** para convertir parte de lo que sabes en algo nuevo, ¿por dónde empezarías?
- Sub: Estas son las posibilidades que más encajan con tus respuestas. Elige una para explorarla. Puedes cambiarla después.

### Resultado · Tu Mapa de Valor
- Encabezado: **{Tu tema / tu área}: no empiezas desde cero.**
- Activos: "Ya tienes N activos con los que construir:" + lista.
- Tu hora hoy (etiqueta **CÁLCULO**): "Hoy recibes $U6 por hora. Estimas que tu conocimiento vale $U8 por hora para quien lo recibe. Esa diferencia, según tus propios números, suma $C3 al año."
- Tus 10 horas: "Tu versión piloto de {tipo} en 10 horas" + los 4 bloques + "Qué no se logra en 10 horas".
- Escenario (etiqueta **ESCENARIO · TUS SUPUESTOS**): "Juega con los números. Todo lo que ves aquí lo defines tú."
  - "Con {S3} {unidades} a ${S2}, el ingreso bruto del escenario sería ${E1}."
  - "Sumando las 10 h de creación y {horas} h de entrega, cada hora invertida equivaldría a ${E3}. Hoy recibes ${U6}."
  - "Para recuperar el valor de tus 10 horas (${C4}) harían falta {E5} {unidades} a este precio."
- Aviso fijo, visible y no en letra minúscula:
  > Esto es un escenario construido con tus propios supuestos. No es una proyección ni una promesa de ingresos. Los resultados reales dependen de la demanda, de tu oferta, de tu ejecución y de factores que este ejercicio no mide. Las cifras son ingresos brutos, antes de costos, comisiones e impuestos.
- Cierre: "El siguiente paso no es construir todo. Es validar una posibilidad con 10 horas bien invertidas."

### CTA (sujeto a Q10)
- Título: Trabaja tu mapa en vivo.
- Sub: En la Masterclass gratuita vemos cómo elegir una posibilidad y validarla antes de invertir más tiempo. *(Hay que confirmar que refleje lo que la Masterclass cubre.)*
- Botón: `Quiero mi lugar en la Masterclass →` (mismo enlace de systeme.io)

### Copiar resultado
```
Mi Mapa de Valor · Riqueza Academy™
Activos: N · Posibilidad que exploro: {tipo}
Mis 10 horas: {C5} semanas a mi ritmo
#MiCaminoRICA
```

---

## 9. What changes in the current calculator

### Conservar
- Diseño visual completo: tokens de color, tipografías, tarjetas, barra de progreso, sliders, navegación.
- Estructura de 5 pasos y la función `go()` / `updateProg()`.
- Trato por género, **sin nombres ficticios**.
- Sliders de años, tarifa, horas para otros y valor estimado.
- Cálculo de salario mensual y de brecha (C1–C3), con copy nuevo.
- Selector de horas disponibles.
- Enlace del CTA a systeme.io y cálculo del tercer miércoles, corrigiendo KI-12.
- Botones Recalcular y Copiar, con texto nuevo.

### Transformar
- Hero: de "¿Cuánto te cuesta no actuar?" a "¿Qué podrías crear con lo que ya sabes?".
- Bloqueos: de costo oculto en dólares a entrada del plan de 10 horas.
- Identidad (empleado/a, etc.): solo personaliza el copy.
- Área: solo copy, sin multiplicador.
- Pantalla de resultado: pasa de "costo + ROI + línea de tiempo" a "activos + tu hora hoy + posibilidades + 10 h + escenario".
- Tarjeta de decisión "Sin actuar vs Con RICA": se reemplaza por el escenario editable.

### Eliminar
- `AREA_MULT`, `expFact`, `factHoras`, `PRECIO = 297`, ROI, break-even del curso.
- Línea de tiempo "Sin actuar / Con RICA™".
- "Potencial año 1", "Estimado conservador", "10 ventas", "Es matemática".
- "El sueño de alguien más", "alguien más captura esto", "Las líderes que deciden…" con género fijo.
- Avatares "María Elena" y "Carlos".
- Pregunta de forma de cobro (`modelo`): no aporta a la nueva lógica. Se puede conservar solo como copy si Leslie lo prefiere.
- CSS huérfano del paso de captura eliminado (KI-16).

### Nuevo
- Paso de activos (U5) y tema opcional (U4).
- Paso de formas de aportar (U10, U11).
- Catálogo de 11 posibilidades como objeto de configuración.
- Afinidad (top 3 con motivo).
- Plan de 10 horas por tipo.
- Escenario editable con fórmulas visibles y sensibilidad.
- Accesibilidad básica en las opciones: `button` / `role`, teclado.

### Sin cambios de stack
Un solo archivo HTML, JS vanilla, sin dependencias nuevas, sin backend y sin IA.

---

## 10. Risks / assumptions

| Riesgo | Tipo | Mitigación |
|---|---|---|
| Quitar el marco de "pérdida" puede **bajar la conversión** a corto plazo | Hipótesis sin datos (no hay analítica, KI-17) | Medir: agregar eventos mínimos (inicio, fin, clic en CTA) antes o junto con el lanzamiento, y comparar con la versión actual si es posible |
| **Más preguntas = menos completitud** | Evidencia general de UX de formularios | Máximo 12 inputs, pasos opcionales marcados, barra de progreso |
| Las **horas de entrega por tipo** son supuestos del agente | Supuesto | Editables en pantalla, etiquetados; **Leslie los revisa antes de implementar** |
| La **afinidad** es una heurística, no un diagnóstico | Supuesto | Copy "encaja con tus respuestas"; sin porcentajes; "ver todas" |
| **Desalineación con la oferta:** la calculadora sugiere consultoría o taller, pero la Masterclass o el Método RICA hablan de "primer producto digital en 28 días" | Conflicto de mensaje | Decisión Q10 |
| Mostrar cifras, incluso como escenario, sigue teniendo **riesgo regulatorio** si el público o los anuncios son de EE. UU. | Legal (no es asesoría legal) | Aviso visible, sin lenguaje de promesa, fórmulas a la vista; revisión legal recomendada si se usa en anuncios pagados |
| La **lluvia de dinero** del hero contradice el nuevo tono | Marca | Decisión Q11 (reemplazar por una animación sutil de "activos" o eliminarla) |
| El texto libre del tema (U4) podría usarse para inyectar HTML | Seguridad | Insertar solo con `textContent` y limitar longitud |
| Hosting desconocido (Q3): no se sabe si hacer merge a `main` afecta producción | Operativo | Resolver Q3 antes del merge |
| El catálogo y la afinidad son **propiedad intelectual reutilizable** en Riqueza App (MVP: diagnóstico, activos, ruta) | Oportunidad | Mantenerlos como configuración separada de la UI; **no** construir arquitectura ahora |

---

## 11. Recommendation

Aprobar el concepto con este alcance mínimo:

1. Los 5 pasos y los 12 inputs descritos.
2. Las 4 familias de fórmula; el escenario empieza en el punto de equilibrio (E5).
3. Catálogo de 11 posibilidades; top 3 por afinidad.
4. Plan de 10 horas con 4 bloques.
5. Aviso de escenario fijo y visible.
6. Mismo archivo, mismo diseño, sin dependencias.

Fuera de alcance por ahora: captura de email (Q6), analítica (se recomienda como paso inmediato posterior), IA, backend.

Secuencia sugerida después de la aprobación:
1. Q10 (mensaje de la Masterclass) y revisión de los supuestos de horas.
2. Implementar en la rama con vista previa.
3. Revisión de Leslie en el navegador (móvil y escritorio).
4. Q3 (hosting) antes del merge.

---

## 12. DECISION NEEDED

**¿Apruebas este nuevo concepto ("Mapa de Valor · 10 Horas") como base para el rediseño?**
- A) Sí, tal como está.
- B) Sí, con cambios (indica cuáles).
- C) No, hay que replantear la dirección.
