
## 1) Objetivo

- Pasar de “búsqueda random” a **investigación encargada**, con: alcance definido, fuentes verificadas, bitácora completa y entregables formales (doc, PPT, resúmenes, audio).

## 2) Flujo UX (WhatsApp / chat)

1. **Invocación**: “Quiero investigar _tecnologías ecosustentables de construcción_.”
2. **Alineación rápida (2–4 turnos)**
    - Bot: _Objetivo, público, país/región, horizonte temporal, profundidad, entregables (doc/PPT/audio), deadline, idioma._
    - Usuario confirma un **brief** (JSON visible).
        
3. **Confirmación**: Bot devuelve **Plan de Investigación v0.1** (temas, fuentes target, criterios de calidad, formato de salida) y pide “OK para iniciar”.
4. **Ejecución**: Bot consulta, contrasta, puntúa fuentes, compila borradores de hallazgos y **log de pasos**.
5. **Entrega**: Bot presenta entregable(s) + **Anexo de auditoría** y guarda todo en el DMS con metadatos.
6. **Follow-up opcional**: “¿Actualizar manual/proceso X con esta evidencia?” (crea propuesta de cambio).

## 3) Componentes clave

### A) Brief estructurado (JSON)

- `topic`: “tecnologías ecosustentables de construcción”
- `scope`: alcance y exclusiones
- `region`: “Uruguay/LatAm/Global”
- `time_window`: “últimos 24 meses”
- `depth`: “ejecutivo / técnico / mixto”
- `deliverables`: `["doc", "ppt", "audio-3min"]`
- `audience`: “dirección / compras / obra”
- `decisions_to_inform`: p.ej. “selección de proveedor / CAPEX 2026”
- `constraints`: “solo fuentes primarias / citar costos en USD”
- `deadline`: fecha/hora
- `language`: ES/EN

> El brief queda **firmado** (hash + timestamp) y anclado al legajo del proyecto.

### B) Criterios de calidad (reglas)

- **Fuentes mínimas**: ≥3, con ≥2 independientes y ≥1 primaria (paper/ley/dato oficial).
- **Frescura**: si es “tendencias/actualidad”, ≥70% de fuentes ≤24 meses.
- **Reputación**: dominios .gub.uy, .edu, .org, whitepapers de fabricantes, normas (ISO/IRAM/UNIT).
- **Consenso**: destacar convergencias y conflictos.
- **Trazabilidad**: cada afirmación relevante enlaza a cita con fecha del **evento** y **publicación**.

### C) Bitácora de investigación (Audit Log)

Para cada paso se registra:

- **query** usada, **fuentes abiertas**, **hora**, **extracciones** (hechos atómicos JSON), **puntuación de fuente**, **consenso/conflictos**, **decisión** (incluir/excluir) y **motivo**.
- Guardado en DB + DMS como:  
    `INV/LOG/AAAA-MM_Tema - [PRJ:xxx][OWNER:yy][VER:v1]`.

### D) Score de confianza (0–1)

`conf = 0.3*reputación + 0.25*consenso + 0.2*frescura + 0.15*claridad_cifras + 0.1*primarias`

- Umbrales:
    
    - ≥0.75 ✅ sólido
    - 0.55–0.74 ⚠️ con caveats
    - <0.55 ⛔️ no concluyente (se documenta como tal)

## 4) Entregables (formatos)

- **Informe escrito** (Markdown/Docx, 3 niveles: 1 pág / 5 págs / 12 págs).
- **Presentación PPTX** (ejecutivo: problema → hallazgos → costos/beneficios → riesgos → próximos pasos).
- **Audio** (1–3 min) con **resumen narrado**.
- **Anexo de auditoría** (tabla de hechos → cita → URL → fecha evento/publicación → nota de calidad).
- **Dataset** (CSV/JSON) con hechos atómicos y metadatos.

## 5) Integración con Manual de Procesos / Cargos

- Bot detecta secciones del manual impactadas y propone **“Propuesta de Actualización”**:
    - _Qué cambia, por qué (evidencia y citas), impacto en costos/tiempos, versión nueva de tarea, responsables._
        
- Flujo de aprobación: **borrador → revisión semanal → aprobado** (o permisos directos por roles).
- Al aprobar, se versiona: `PROC/… [VER:v1.3][FUENTE:INV-2025-09-eco]`.

## 6) DMS y Metadatos (ocultos)

- **Proyecto** `PRJ:INV_ECOSUST_2025_09`
- **Categoría** `INV` (investigación), **DOCU/REP/PPT/AUDIO/LOG**
- **Estado** `REV/APROB`
- **Sensibilidad** `INT/CONF`
- **Dueño** `OWN:usuario`
- **Fechas** creación/cortes/eventos

## 7) n8n – Esqueleto de workflow

**Fase A: Brief**

- `Webhook` → `Function (normalize)` → `LLM (planner de brief)` → `If (falta info)` → _preguntas_ → `Confirm Brief` → `DB Insert (Brief)`

**Fase B: Investigación**

- `LLM (plan de búsqueda)` → `HTTP (motores)` → `Function (dedup/variedad)` → `HTTP (fetch)` → `Extract (HTML/PDF)`
- `LLM (hechos atómicos → JSON)` → `Function (score fuente)` → `Function (cross-check)` → `Function (confidence)`
- `DB Insert (Audit Log)` en cada iteración/k-fold

**Fase C: Redacción y Entrega**

- `LLM (redactor, formatos)` → `File (Docx/PPTX/MP3)` → `DMS Upload (con metadatos)` → `Responder (links + resumen + score + citas)`
- `Propuesta de actualización de manual` (si aplica) → `Queue revisión`

## 8) Mensajería modelo (WhatsApp)

**Bot**: “¿Iniciamos investigación sobre _tecnologías ecosustentables de construcción_?  
Definime: público objetivo, región, profundidad (ejecutivo/técnico), y formato (doc/ppt/audio).”

**Usuario**: “Dirección, Uruguay, ejecutivo, doc + ppt.”  
**Bot**: “Perfecto. Ventana temporal: ¿últimos 24 meses? ¿Decisiones a informar?”  
**Usuario**: “Sí, selección de tecnologías para licitación 2026.”  
**Bot**: “Listo. Te presento el **Plan v0.1** (temas, fuentes, criterios). ¿Confirmás para iniciar?”  
**Usuario**: “Confirmo.”  
**Bot**: “En marcha. Se generará informe + ppt + anexo de auditoría. Te aviso cuando estén listos y quedarán guardados en `INV/…` con trazabilidad completa.”

_(En tu implementación real, el bot puede ir adelantando borradores parciales y miniresúmenes; todo queda logueado.)_

## 9) Plantillas (resumen de salida)

**Resumen ejecutivo (máx. 8 líneas)**

- Qué se buscó
- Hallazgos clave (3–5 bullets con cifras/fechas)
- Implicancias para decisión
- Riesgos y vacíos de información
- **Confianza global** + por capítulo

**Citas**: Título — dominio — fecha (evento|publicación) — URL

## 10) Gobernanza y compliance

- **PII**: enmascarado por defecto.
- **Legal/Salud/Finanzas**: disclaimer + preferencia de fuentes primarias.
- **Política pública/Normativa**: doble verificación y citas oficiales.
- **Reproducibilidad**: todo paso replicable desde el Audit Log.