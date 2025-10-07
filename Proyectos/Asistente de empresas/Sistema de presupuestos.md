## **Presupuestos multiversión & control de cambios** (v1)

**Objetivo:** permitir convivir y relacionar **tres presupuestos** principales y sus derivados sin “contaminar” el análisis económico de la obra: 1) **Presupuesto de cotización/venta** (cara al cliente), 2) **Presupuesto de costo (baseline interno)**, y 3) **Presupuesto de realidad/forecast** (lo ejecutado y lo proyectado), además de **adicionales/cambios (VO/CO)** con trazabilidad contractual.

### A. Tipos de presupuesto

1. **Venta (PV)**: el que se presenta y firma en contrato. Puede tener ajustes comerciales (márgenes, metrajes promocionales, alternancias de calidades).
    
2. **Costo (PC)**: baseline técnico interno. Mismos metrajes “ejecutables” y **PUs técnicos** (material, mano de obra, equipos, indirectos) sin maquillaje comercial. **Se bloquea** al iniciar la obra.
    
3. **Realidad/Forecast (PR-FC)**: espejo vivo con **ejecutado** + **proyección a término**. Se actualiza con avances, consumos, certificaciones y tendencias.
    
4. **Adicionales/Cambios (VO/CO)**: variaciones contra PV, con estado: _propuesto → en negociación → aprobado → rechazado_. Cada VO tiene su **impacto en PV** (ingreso) y en **PC/PR-FC** (costo/plazo).
    

### B. Relaciones y mapeos

- **WBS Mapper**: herramienta para mapear partidas cuando PV difiere de PC (p. ej., ventas agrupa “Terminaciones” en una sola partida y PC las desagrega en Revoques/Pintura/Cerámica). Mantiene **reglas de prorrateo** y **traducciones**.
    
- **Trazabilidad**: cada ítem de PC referencia su(s) ítem(s) padre en PV. Los VO pueden **crear** nuevas partidas o **dividir** existentes con mapeo automático.
    
- **Bloqueos**: PV y PC quedan **inmutables** tras su aprobación inicial (solo se **versionan** con motivo documentado).
    

### C. Artefactos

- **Contrato** (condiciones, alcance, hitos de facturación, reajustes/escalas, PS/PC provisionales).
    
- **Cuadro comparativo PV vs PC** con márgenes por rubro y margen total.
    
- **Libro de cambios (VO log)** con firma digital y anexos.
    
- **Plan de mediciones**: definiciones de metrajes que gobiernan certificación.
    

### D. Procesos clave

1. **Armado de PV**: parte del **Presupuesto Técnico Justo (PTJ)** generado por ingeniería → Comercial aplica reglas (margen, ajustes de metraje/terminaciones) → se emite PV vX con _rationale_.
    
2. **Consolidación de PC**: copia del PTJ con precios técnicos + indirectos + riesgos → **PC v1** se bloquea al _Inicio de Obra_.
    
3. **Certificación mensual** (contra cliente): según PV + VO aprobados. Genera **Ingreso Reconocido** y afecta cashflow.
    
4. **Seguimiento de costo**: PR-FC se nutre de avances, consumos y contratos de subcontrata → **Costo Ejecutado** y **ETC** (Estimate To Complete).
    
5. **Gestión de VO/CO**: cualquier cambio detectado crea **RFC** (request for change) con triple impacto: Alcance/Plazo/Costo. Si se aprueba: impacta PV (ingresos) y PC/PR-FC (costos/plazos). Si se rechaza: queda como **riesgo** o **costo no recuperable** (tracking aparte).
    
6. **Rebaselining controlado**: solo por comité y con justificación (p. ej., cambio mayor de alcance). Guarda **snapshot** anterior.
    
7. **Carga flexible de forecast**: el PR-FC puede incorporar:
    
    - **Rendimientos actuales de obra**: extrapolados a las partidas futuras de la misma obra.
        
    - **Rendimientos de otras obras**: cuando hay evidencia más reciente o comparable (ejemplo: misma tarea se ejecutará en 6 meses, se cargan rendimientos frescos de otra obra).
        
    - **Presupuestos de suministros y subcontratos**: actualización de precios futuros según cotizaciones recientes o contratos firmados.
        
    - **Proyecciones de gastos fijos adicionales**: p. ej., extensión de fecha de entrega que incrementa oficina técnica, alquileres, seguros, administración.
        
    - **Rendimientos de adicionales/VO**: integrados al forecast para calcular **beneficio esperado total de la obra** con cambios.
        

### E. Reglas para no “contaminar” el resultado

- **Separación estricta** de **ingresos PV** vs **costos PC/PR-FC**.
    
- Los **VO pendientes** no se cuentan como ingreso hasta estar **aprobados**; sí pueden figurar en **escenarios** (best/base/worst).
    
- **Partidas comerciales** (bundles) se reparten a PC por regla estable (mapper) y deben mantenerse consistentes toda la obra.
    
- **Provisiones**: montar provisión de costo/ingreso cuando el hecho generador es firme pero la documentación está en curso.
    
- **Auditoría**: toda edición genera **bitácora** (quién, cuándo, por qué, adjunto).
    

### F. Interfaz sugerida

- **Comparador PV–PC–PR/FC** por rubro y total con semáforos (margen, desvío de costo, slippage de plazo).
    
- **Editor de VO** con wizard: motivo → alcance → metraje/precio → impacto → documentos → estados.
    
- **Mapper visual de WBS** con drag & drop para prorratear y consolidar partidas.
    
- **Tablero de márgenes**: Margen al adjudicar (PV–PC), Margen actual (PV+VO aprobados – PR/FC), **AFE** (At-Finish Estimate) y **variación vs adjudicación**.
    

### G. KPIs

- **Margen adjudicado** vs **margen forecast** (Δ y %).
    
- **Valor de VO**: aprobado / en negociación / rechazado / pendiente (por obra).
    
- **Slippage** de costo (PR/FC vs PC) y de plazo (hitos desplazados).
    
- **% de partidas PV mapeadas** a PC (objetivo: 100%).
    
- **Nº de rebaselines** y motivos.
    

### H. Casos especiales

- **Sumas y costos provisionales**: reglas de cierre (fecha/índice) y cómo convergen a ítems definitivos.
    
- **Escaladores de precio** (índices): simulación y liquidación.
    
- **Contratos mixtos**: precio global + unitarios.
    
- **Alcances alternativos** (opciones del cliente) que se activan por evento.
    

### I. Datos/Modelo

- Entidades: **Budget(PV/PC/PR-FC)**, **BudgetItem**, **WBS**, **WBSMapping**, **ChangeOrder(VO/CO)**, **Contract**, **Valuation/Certificate**, **Forecast**.
    
- Campos clave: versión, estado, fecha, justificación, vínculo a documentos.
    

### J. Workflows tipo

**WF1 – Comercial ajusta PV**

1. Ingeniería genera PTJ.
    
2. Comercial aplica margen + simplifica partidas (bundle Terminaciones).
    
3. Mapper define prorrateo a PC (Revoques/Pintura/Cerámica).
    
4. Se aprueba PV v3; PC v1 queda bloqueado.
    

**WF2 – Se detecta adicional en obra**

1. Arquitectura reporta metraje extra de muros.
    
2. Se crea RFC con medición y respaldo fotográfico.
    
3. Comercial prepara VO: +1.200 m² × PU → impacto en ingreso y plazo.
    
4. VO aprobado → PV aumenta; PR/FC incorpora costo y cronograma ajusta hitos.
    

**WF3 – Cambio/reemplazo de rubro**

1. Se decide **cambiar un tipo de piso** (ej. cerámica → porcelanato) o un tipo de muro.
    
2. Se registra el evento como **Cambio de Rubro (CR)** con motivo (estético, técnico, disponibilidad).
    
3. Sistema solicita imputación: ¿es un **VO** con impacto en PV (adicional) o solo un **ajuste interno** (sin ingreso)?
    
4. El CR crea relación entre **Rubro saliente** (eliminado/reducido) y **Rubro entrante** (nuevo/sustituto).
    
5. Se comparan metrajes, precios unitarios y rendimientos: diferencia neta → impacta en **PC/PR-FC** (costo real).
    
6. Si el cliente acepta que el cambio es adicional: se genera VO con nuevo alcance y se actualiza PV.
    
7. Si no corresponde VO (p. ej. reemplazo sin costo adicional): queda registrado solo en PC/PR-FC como **ajuste de forecast**.
    
8. Reporte automático: "Se reemplazó Rubro X por Rubro Y. Impacto: –$45.000 en costo, +15 días en plazo, sin cambio en ingreso."
    

**WF4 – Rubro eliminado sin sustituto**

1. Se decide suprimir una tarea completa (ej. revestimiento opcional no ejecutado).
    
2. El rubro queda con avance 0 en PR-FC.
    
3. El sistema solicita definición: ¿se descuenta también del PV (reducción de alcance/VO negativo) o solo del PC (ahorro interno)?
    
4. Se documenta decisión en libro de cambios y se recalcula margen.
    

**WF5 – Nuevo rubro no previsto**

1. Se detecta tarea nueva (ej. impermeabilización adicional).
    
2. Se crea RFC → nuevo ítem en WBS.
    
3. Evaluación: si es VO → se cotiza al cliente; si no → se carga directo al PC/PR-FC como costo no recuperable.
    
4. Forecast se actualiza y genera alerta: "Nuevo rubro no previsto impacta 2% en costo de obra."