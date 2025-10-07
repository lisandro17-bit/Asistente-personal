## **Avances físicos & Bitácora conversacional** (v1)

**Objetivo:** capturar avances, consumos y eventos **durante la jornada** mediante una **bitácora tipo chat** usada por arquitectos, capataces y auxiliares; convertir esas interacciones en datos estructurados y devolver **feedback activo** (recordatorios y sugerencias) sin ser invasivo.

### A. Entradas (por chat/bitácora)

- **Avances**: tareas ejecutadas, frentes, metrajes/unidades, fotos, ubicación.
    
- **Logística**: materiales **recibidos** (remito/foto), equipos en sitio, movimientos de cuadrillas.
    
- **Consumos**: cantidades usadas cuando se conozcan; si no, se infiere luego (ver M-01).
    
- **Incidencias**: impedimentos, clima, calidad/NCR, seguridad.
    
- **Notas rápidas**: texto libre tipo “post-it” que el sistema clasificará.
    

### B. UX conversacional

- **Plantillas de prompts**: “Decime tarea, frente y metraje” / “¿Qué materiales recibiste?” / “¿Hubo retrabajos?”
    
- **Atajos** (quick actions): _/avance_, _/consumo_, _/recepción_, _/foto_, _/ncr_, _/paro_.
    
- **Reconocimiento** de entidades: rubro, frente, unidad de medida, ítem de catálogo, subcontrata.
    
- **Adjuntos**: fotos, remitos, audio a texto.
    

### C. Procesamiento

1. **Parseo** y normalización (UM, frentes, rubros).
    
2. **Validaciones suaves**: incoherencias (p. ej., metraje > plan del frente) → se marca _pendiente de confirmar_, no bloquea.
    
3. **Auto‑link** con M‑01: recepciones ↔ stock; avances ↔ consumos teóricos.
    
4. **Auto‑link** con M‑02: cambios que suenen a VO/CR generan **borrador de RFC**.
    

### D. Feedback y sugerencias (no invasivo)

- **Nudges** contextuales en el chat: “Cargaste 80 m² de revoque en Torre A. ¿Querés adjuntar foto?” / “Recibiste 20 bolsas: ¿imputamos al frente 3?”
    
- **Recordatorios** configurables: cierre parcial de mañana/tarde; checklist de frentes activos.
    
- **Sugerencias de control**: “Avance sin consumo de arena/cemento en Revoques. ¿Lo revisamos?” (link a bandeja de conciliación M‑01).
    
- **Resúmenes on‑demand**: “/resumen hoy” → avance por rubro, recepciones, incidencias.
    

### E. Bandejas & vistas

- **Timeline de bitácora** con filtros por obra, frente, usuario, tipo de evento.
    
- **"To‑review"**: entradas con validación pendiente (metrajes altos, rubro dudoso, consumo faltante).
    
- **Mapa/Plano** (opcional) para ubicar avances por frente/piso.
    

### F. Integraciones

- **M‑01**: genera propuestas de imputación de consumos y aging de stock.
    
- **M‑02**: dispara RFC/VO/CR cuando un avance o recepción implica cambio de rubro o alcance.
    
- **M‑06**: frases que sugieren **ajuste de receta/rendimiento** crean **tickets de rubrado**.
    
- **M‑11**: todas las **asunciones** (p. ej., inferencia de rubro) quedan visibles en la planilla de auditoría.
    

### G. KPIs

- **Frecuencia de carga** por usuario/cuadrilla.
    
- **% de avances con evidencia** (foto/remito).
    
- **Tiempo medio de validación** de entradas _to‑review_.
    
- **Cobertura de frentes** informados por día.
    

### H. Workflows tipo

**WF20 – Carga continua de jornada**

1. 08:30 capataz: _/avance_ “Muro tabique Frente B 35 m² foto”
    
2. 10:10 auxiliar: _/recepción_ “Yeso fino 60 bolsas remito #123”
    
3. 11:00 arquitecto: “Se decidió porcelanato en lugar de cerámica en hall nivel 1” → el sistema crea **RFC borrador** (M‑02).
    
4. 14:00 capataz: _/consumo_ “Arena 5 m³ Frente B revoques”
    
5. 17:00 “/resumen hoy” → tablero diario.
    

**WF21 – Nudge de control**

1. Bitácora detecta avance sin consumo teórico asociado.
    
2. Envía nudge: “Revoques Frente B 35 m² sin consumo de cemento/arena. ¿Querés revisar o imputar estimado?”
    
3. Usuario abre bandeja M‑01, valida o corrige.