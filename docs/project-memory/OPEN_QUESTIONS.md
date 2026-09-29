# OPEN QUESTIONS

Se preguntan a Leslie **una a la vez**, en orden de prioridad. Estado: ABIERTA / RESUELTA.

## Q1 — ¿Este repositorio es el repo de Riqueza App? · RESUELTA (D-008: opción A)

**Conflicto:** CLAUDE.md define "Riqueza App" (backend, AI service, dashboard, progreso). El repo `calculadora-rica` solo contiene una calculadora estática de captación (`calculadora-app.html`).

Opciones:
- A) Crear un repo nuevo para Riqueza App y mantener `calculadora-rica` como lead magnet independiente (recomendación del agente: separa un activo de marketing que ya funciona de un producto en construcción).
- B) Convertir `calculadora-rica` en el repo de Riqueza App y la calculadora pasa a ser una pieza dentro (p. ej. el "Diagnóstico" del MVP).
- C) Este repo es solo la calculadora; Riqueza App vive en otro lugar ya existente.

## Q2 — ¿Dónde está `docs/RIQUEZA_APP_MASTER_AGENT_PROJECT_v1.md`? · ABIERTA · BLOQUEANTE para Riqueza App (irá al repo nuevo)

CLAUDE.md lo declara obligatorio. No existe en el repo ni en su historial. Tampoco existen: Master Context, Technical Architecture aprobada, reglas de seguridad (niveles 3–5 de la jerarquía de verdad de CLAUDE.md §4).

## Q3 — ¿Dónde está publicada la calculadora hoy? · ABIERTA

No hay configuración de hosting en el repo (¿systeme.io embebido, GitHub Pages, otro?). Necesario para saber si un cambio en `main` impacta producción.

## Q4 — ¿La lógica financiera de la calculadora está aprobada? · ABIERTA · PREGUNTADA 2026-09-29

Multiplicadores por área (`AREA_MULT`), factor de experiencia, factor de conversión por horas (15–60 %), precio `$297` y proyección a 24 meses (×2.8) están codificados sin fuente documentada. Ver KI-03.

## Q5 — ¿El precio del Método Rica IA™ es $297? · ABIERTA

Valor fijo en `calculadora-app.html` (`PRECIO = 297`).

## Q6 — ¿Se quiere recuperar la captura de email dentro de la calculadora? · ABIERTA

Se eliminó en `40db451`; hoy la captura ocurre en systeme.io y el resultado del diagnóstico no viaja con el lead.

## Q7 — ¿Cuándo y con qué nombre se crea el repo de Riqueza App? · ABIERTA

Depende de D-008. No se creará sin confirmación explícita de Leslie (acción externa).

## Q8 — ¿Qué hacer con `CLAUDE.md` en este repo? · ABIERTA

Describe Riqueza App, no la calculadora. Bajo D-008 pertenece al repo nuevo. Se mantiene aquí temporalmente (solo en la rama de trabajo) hasta crear ese repo.
