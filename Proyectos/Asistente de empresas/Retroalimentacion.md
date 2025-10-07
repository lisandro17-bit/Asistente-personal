## **Retroalimentación automática a presupuesto (tickets de rubrado)** (v1)

**Objetivo:** capturar señales de campo (bitácora, stock, VO) e insights de informes para **mejorar el rubrado base** sin romper el análisis de la obra en curso. Diferenciar **edición de rubro existente** vs **creación de nuevo rubro**, con **tickets** que se aprueban y publican en fecha programada.

### A. Tipos de tickets

- **TR‑Editar rubro**: ajustar **receta** (insumos, proporciones), **rendimientos estándar**, **PUs técnicos**, **tolerancias de merma**, **equivalencias** (M‑10) y **UM/factores**.
    
- **TR‑Nuevo rubro**: alta de **partida/variante** (p. ej., Revoque con capa mecafino; Impermeabilización con membrana líquida). Incluye código, familia, receta, rendimiento, PU y **reglas de mapeo WBS**.
    
- (Opcional) **TR‑Deprecación de rubro**: marcar rubro obsoleto y sugerir sustitutos.
    
- (Opcional) **TR‑Actualizar mapper PV↔PC**: cuando el cambio requiere nuevo prorrateo (ver M‑02).
    

### B. Orígenes (triggers)

- **Bitácora (M‑03)**: frases como “se agregó capa extra”, “se usó Viapol 7000”, “cambiamos porcelanato” → crean **borrador de ticket** con evidencia (fotos, remitos, usuarios).
    
- **Stock/Compras (M‑01/M‑10)**: **sustituciones repetidas** o diferencias de consumo vs receta **> umbral**.
    
- **Informes (M‑12)**: desvíos persistentes de **rendimiento** o **desperdicio**; waterfall de margen que identifica impacto por receta.
    
- **Manual**: comando de chat _/ticket rubro_ o desde la ficha de rubro.
    

### C. Ciclo de vida

Estados: **Borrador → Por revisar (técnico) → En evaluación (sandbox) → Aprobado → Programado → Publicado → Desplegado en obras seleccionadas → Cerrado**.

- **Roles**: Autor (obra), Revisor técnico, **Curador de rubrado** (aprueba), Admin (publica).
    
- **SLA** y **reglas de quorum** (p. ej., 1 curador + 1 obra afectada).
    

### D. Sandbox / Impacto

- **Diff de rubro**: vN vs vN+1 (receta, rendimiento, PU, sustitutos, equivalencias).
    
- **Simulación**: impacto en **PR‑FC** de obras abiertas, **PTJ** futuros y **margen** (AFE).
    
- **Ámbito de aplicación**: _Sólo base corporativa futura_ / _Aplicar a Obra X desde fecha Y_ / _Rebaselinar Obra X_ (requiere comité de cambios, ver M‑02).
    

### E. Interfaz

- **Bandeja de tickets** con filtros por obra, tipo, estado, familia, impacto estimado.
    
- **Wizard** para TR‑Editar/TR‑Nuevo con **plantillas** por familia.
    
- **Adjuntos & evidencias** (fotos, remitos, planillas, enlaces a bitácora).
    
- **Programación** de publicación (fecha/hora) y lista de obras a las que se ofrece **migrar**.
    

### F. Integración

- **M‑03**: genera borradores de tickets desde la bitácora.
    
- **M‑10**: actualiza equivalencias/compatibilidades cuando el cambio involucra productos.
    
- **M‑02**: si el ticket implica cambio contractual → sugiere **VO/CR**; si no, **ajuste interno**.
    
- **M‑11**: todos los tickets, supuestos y decisiones quedan en la **planilla de auditoría**.
    

### G. KPIs

- **Tiempo a aprobación** y **a publicación**.
    
- % de **tickets por tipo** (editar vs nuevo vs deprecado).
    
- **Impacto acumulado en margen** por cambios de rubrado (últimos 90 días).
    
- **Adopción**: obras migradas a la última versión del rubrado base.
    

### H. Workflows tipo

**WF30 – Ticket desde bitácora (capa extra de yeso)**

1. Bitácora: “Revoque yeso + capa mecafino en Frente B (20 m²)” + foto.
    
2. Trigger crea **TR‑Nuevo rubro** (variante) con receta sugerida.
    
3. Revisor técnico ajusta rendimiento y PU; Curador **aprueba**.
    
4. Publicación programada; se ofrece **migrar** a obras similares.
    

**WF31 – Ticket desde informe mensual (rendimiento fuera de rango)**

1. Informe detecta que Revoques rinde 18% por debajo 3 meses.
    
2. Crea **TR‑Editar rubro** para subir HH y ajustar receta.
    
3. Sandbox muestra impacto en AFE (–1.8 pts de margen si no se ajusta).
    
4. Curador aprueba; se aplica a base futura y a obra actual desde el 01/11.
    

**WF32 – Ticket por VO/variante**

1. Se aprueba VO para “Impermeabilización con membrana líquida”.
    
2. Sistema sugiere **TR‑Nuevo rubro** con receta/ficha técnica.
    
3. Se publica en catálogo y queda disponible para futuros PTJ.
    

---