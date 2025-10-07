## **Sistema de informes (semanal, mensual, trimestral)** (v1)

**Objetivo:** transformar los datos de obra en **inteligencia accionable** con informes automáticos y consistentes. Sin ser invasivo: disponibles on‑demand y también programables.

### A. Fuentes de datos

- **M‑03 Bitácora**: avances, incidencias, evidencias.
    
- **M‑01 Stock/Consumos**: recepciones, consumos, aging, conciliaciones.
    
- **M‑02 Presupuestos/Forecast/VO**: PV, PC, PR‑FC, VO/CO, márgenes.
    
- (Cuando estén) **M‑04/M‑05/M‑07/M‑08/M‑09**: cronograma, valor ganado, calidad/NCR, contratistas, riesgos.
    

### B. Tipos de informe

1. **Semanal (operativo, 1–3 páginas)**
    
    - **Enfoque**: resultados y **rendimientos** de la semana.
        
    - **Resumen ejecutivo**: % avance semanal vs plan, **productividad** por rubro clave (real vs estándar), **burn rate** semanal, top‑5 desvíos y alertas.
        
    - **Hitos próximos (14 días)** y semáforo de frentes.
        
    - **Consumos vs teórico** y **stock crítico** (días de cobertura).
        
    - **VO/CR**: movimientos de la semana (ingresados/aprobados).
        
    - **KPIs**: RUP por rubro, **CPI/SPI semanal** _(SPI/CPI “light” hasta integrar M‑05)_, % avances con evidencia, tiempo medio de validación.
        
    - **Gráficos**: barras productividad real/plan; mini‑sparklines 4 semanas.
        
    - **Acciones**: checklist corto con responsables y fechas compromiso.
        
2. **Mensual (táctico, 5–10 páginas)**
    
    - **Enfoque**: **históricos** y **esperados**.
        
    - **Resumen ejecutivo**: **margen adjudicado vs margen forecast**, variación mensual y acumulado YTD.
        
    - **Curva S “light”**: PV/EV/AC mensual y acumulado (luego se integra con M‑05).
        
    - **Serie de rendimientos** por rubro (últimos 6–12 meses) y causas de desvío.
        
    - **Cashflow** ejecutado vs plan; compras mayores e imputación.
        
    - **VO/CO**: aprobados, en negociación y su impacto en costo/ingreso/plazo.
        
    - **Forecast 90 días**: ETC/EAC (At‑Finish Estimate) por rubro y total.
        
    - **KPIs**: slippage de costo/plazo, rotación de inventario, aging de stock, % mapeos PV↔PC, Nº rebaselines.
        
    - **Gráficos**: líneas EV/AC/PV, waterfall de **variación de margen** (VO, rendimientos, precios, overhead).
        
3. **Trimestral (estratégico, 10–20 páginas)**
    
    - **Enfoque**: análisis profundo del **trimestre** y **proyección** al cierre.
        
    - **Post‑mortem parcial**: tendencias, desviaciones persistentes, **causa raíz** (5 porqués) y lecciones aprendidas.
        
    - **Benchmark** vs otras obras y vs baseline corporativo (recetas M‑10, rendimientos corporativos).
        
    - **Escenarios de cierre** (best/base/worst) con **AFE** y buffers de plazo; sensibilidad a precios de insumos críticos.
        
    - **Roadmap de acciones** para el próximo trimestre.
        

### C. Motor de informes (Report Builder)

- **Parámetros**: obra, período, alcance (operativo/táctico/estratégico), formato (**PDF/HTML/XLSX**), granularidad (rubro, frente), escenarios.
    
- **Plantillas**: secciones con tokens (p. ej., {{avance_semana}}, {{kpi_cpi}}, {{vo_aprobados}}), tema visual corporativo.
    
- **Pipeline**: extracción → validación de calidad de datos → cálculos (rendimientos, EV/AC/PV, forecast) → armado → revisión → publicación.
    
- **Distribución**: lista de destinatarios, permisos, **firma digital**; historial de versiones.
    

### D. Integración con la UX

- **Comandos de chat**: _/reporte semanal_, _/reporte mensual_, _/reporte trimestral_, _/programar reportes_.
    
- **Bandeja “Reportes generados”**: estado, versión, quién lo pidió, enlaces a evidencias (bitácora, VO, stock).
    
- **Nudges de calidad de datos**: si faltan validaciones claves, el informe advierte e incluye un apéndice de **Datos pendientes**.
    

### E. Tablas y columnas sugeridas

- **Rendimientos (Semanal)**: _Rubro | UM | Rend. plan | Rend. real semana | Δ% | Causa | Acción | Responsable | Fecha compromiso_.
    
- **Comparativo (Mensual)**: _Rubro | PV | PC | Ejecutado (AC) | EV | Δ costo | Δ plazo | EAC | Comentarios_.
    
- **VO/CO**: _Código | Estado | Impacto ingreso | Impacto costo | Impacto plazo | Evidencia | Responsable_.
    

### F. KPIs globales de reporting

- **On‑time rate** de emisión de reportes; **data completeness** (% campos críticos completos).
    
- **Tiempo de ciclo** desde cierre de período hasta publicación.
    
- **% de acciones cerradas** del plan anterior.
    

### G. Diagramación (resumen)

- **Portada** → **Resumen ejecutivo** → **KPIs** → **Rendimientos** → **Costos/Curva S** → **Stock/Consumos** → **VO/CR** → **Riesgos/Calidad** (si aplica) → **Acciones** → **Anexos**.
    

### H. Notas

- Mientras **M‑05 (Valor Ganado)** esté pendiente, se usa la **Curva S light**; al activarla, se integran SPI/CPI formales y métricas derivadas.