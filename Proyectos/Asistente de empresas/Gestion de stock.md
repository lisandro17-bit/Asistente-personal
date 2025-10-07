## Gestión de **stock & consumos por rubro en obra** (v1)

**Objetivo:** cerrar la brecha típica entre compras/ingresos a obra y consumos reales por rubro, para poder medir rendimientos y detectar desvíos/mermas a tiempo.

### A. Entradas

- **Compras**: OC, remitos/facturas, fecha, proveedor, artículo, UM, cantidad, costo unitario, lote/partida (cuando aplique), obra/almacén destino.
    
- **Maestro de ítems**: código, descripciones, UM base, UM alternativas y **factores de conversión** (p.ej., _1 bolsa de Portland = 50 kg = X m³ de mortero estándar_).
    
- **Rubrado/WBS**: estructura de partidas con **recetas**/insumos esperados (BOM por rubro) y **rendimientos** planeados.
    
- **Avances físicos**: % avance y fechas por rubro/frente (carga típica semanal/quincenal por arquitectura).
    
- **Movimientos de stock**: ingresos, transferencias internas, egresos/consumos, devoluciones.
    

### B. Proceso (lógica del módulo)

1. **Conciliación automática compras→stock**: cada remito genera un _ingreso de stock_ en el almacén de obra con su lote/fecha.
    
2. **Catálogo normalizado & equivalencias**: todas las entradas se normalizan a la **UM base**; las equivalencias permiten comparar con consumos teóricos del rubro.
    
3. **Sugerencia de consumo por heurística** (si no hay parte de consumo declarado):
    
    - _Trigger_: transcurridos N días desde la compra sin egresos registrados.
        
    - _Candidatos de uso_: rubros **activos** (con avances reportados) que **consumen** ese ítem según su receta.
        
    - _Ponderación_: cercanía temporal entre avances y compra, volumen de avance, histórico de consumo por ese rubro en esa obra.
        
    - _Propuesta_: "Se compraron **200 bolsas de Portland** el 10/09 y no hay consumos asociados. Candidatos: **Hormigón de estructura**, **Revoques**, **Contrapisos**. ¿Confirmás consumo estimado: 120/60/20 bolsas?"
        
4. **Circuito de validación** (jefe de obra / capataz): aceptar, editar o rechazar la propuesta → se generan egresos por rubro.
    
5. **Consolidación quincenal**: cierre que obliga a reconciliar _compras sin consumo_ y _avances sin consumo_ (o viceversa) antes de aprobar el período.
    
6. **Retroalimentación a rendimientos**: consumos validados vs avance físico alimentan el rendimiento real por rubro.
    

### C. Reglas y controles

- **Tolerancias** por rubro: mermas admisibles (%), diferencia máxima entre consumo teórico y real antes de alerta.
    
- **Aging de stock**: alarma por ítems sin movimiento > X días (parámetro por categoría).
    
- **Bloqueos suaves**: no se puede cerrar quincena si hay >Y% del valor comprado sin rubro asignado.
    
- **Consumo negativo/devoluciones**: flujo específico para ajustar inventario y compensar rendimientos.
    
- **Transferencias** entre frentes/almacenes: deben conservar el historial de lote/fecha.
    

### D. Eventos que generan alertas/comentarios

1. **Compra grande sin consumo**: “Se compraron 200 bolsas de Portland hace 20 días y no hay consumos; ¿siguen en obra?”
    
2. **Consumo sin avance**: “Se registró consumo de hierro φ12 sin avance en Estructura: revisar imputación.”
    
3. **Avance sin consumo**: “Revoques reporta 30% de avance sin consumo de arena/cemento: posible carga incompleta.”
    
4. **Desvío de rendimiento**: “Rendimiento real de Revoques es 1.35× del plan: revisar cuadrilla, mezcla o desperdicio.”
    
5. **Stock envejecido**: “5 big bags de arena sin movimiento desde hace 45 días.”
    

### E. Interfaz (independiente de herramienta)

- **Móvil/obra**: parte rápido de consumo por rubro (scan de ítem/lote, cantidad, rubro, frente, foto opcional).
    
- **Tablero**: tarjetas por ítem con estado (compras, stock actual, consumos vs teórico, aging, próximos faltantes).
    
- **Bandeja de conciliación**: lista de “pendientes de imputar” y propuestas de asignación por IA.
    
- **Ficha de rubro**: curva teórica vs real de consumos y rendimiento acumulado.
    

### F. Datos & trazabilidad

- Kardex por ítem/obra (ingresos/egresos/saldos).
    
- Bitácora de decisiones (quién validó cada imputación y por qué).
    
- Vínculo a **frentes** y **cuadrillas** para análisis de productividad.
    

### G. KPIs

- % de **stock conciliado** (valor y unidades) por quincena.
    
- **Días de cobertura** por ítem crítico (stock/consumo promedio 7–14 días).
    
- **Desvío de rendimiento** por rubro (real/plan).
    
- **Rotación** de inventario por familia de insumos.
    
- Costo de **mermas** estimadas vs tolerancia.
    

### H. Casos límite (edge cases)

- Compras a **depósito central** con consumos luego en obra (trazabilidad multi-almacén).
    
- **Materiales equivalentes** o sustitutos (mantener factor de corrección y nota técnica).
    
- **Producción interna** (p. ej., hormigón en obra) con receta variable: registrar lote/mezcla.
    
- **Paquetes** (palet de cerámica) con fraccionamiento: controlar unidades abiertas.
    

### I. Workflows tipo

**WF1 – Compra sin consumo detectado**

1. Ingreso por remito → 200 bolsas Portland.
    
2. Pasan 14 días sin egresos → _alerta_.
    
3. Sistema sugiere imputación 120/60/20 a Estructura/Revoques/Contrapisos según avances.
    
4. Jefe de obra valida 150/30/20; 0 quedan en stock.
    
5. Se actualiza rendimiento de esos rubros.
    

**WF2 – Avance con consumo insuficiente**

1. Arquitectura carga 25% de Revoques.
    
2. Consumo esperado: 100 bolsas; real registrado: 40 → _alerta_.
    
3. Bandeja de conciliación propone revisar partes de capataz o cargar consumo estimado con nota.
    

### J. Ganchos para IA (cuando lo integremos)

- **Matching** compra→rubro con modelo supervisado (features: fecha, proveedor, histórico, receta, avance).
    
- **NLP de comentarios**: generación de mensajes naturales a jefes de obra.
    
- **Pronóstico** de faltantes y del **punto de pedido** por ítem crítico.
    
- **Detección de anomalías** en rendimientos.
    

### K. Salidas del módulo

- Partes de **consumo por rubro** validados.
    
- **Ajuste de rendimientos** reales por rubro para retroalimentar Presupuesto.
    
- **Alertas** y **tareas** de conciliación.
    
- Informe quincenal de **conciliación stock–avance**.
    

---