## **Catálogo de productos, equivalencias y matching a rubros** (v1)

**Objetivo:** puentear la brecha entre **lo comprado** (nombres comerciales, variantes, químicos específicos) y **lo presupuestado** (recetas técnicas por rubro), manejando sustituciones, sinónimos y confirmación en obra.

### A. Modelo de datos (base)

- **Producto**: código interno, nombre comercial, marca, familia (cemento, impermeabilizante, yeso), presentación (kg, lata, bidón), concentración, ficha técnica (PDF), **UM base** y equivalencias.
    
- **Atributos técnicos**: uso (revoque, impermeabilización, adhesivo), **compatibilidades** (con sistemas y sustratos), rendimiento nominal (m²/litro a espesor X), curva de cobertura por condición.
    
- **Sinonimias**: tabla de alias ("hidrófugo", "Viapol 7000", "membrana líquida", etc.) con _score_ de equivalencia.
    
- **Receta por rubro (BOM)**: lista de insumos esperados con tolerancias y **sustitutos válidos**.
    
- **Matriz Producto↔Rubro**: relación many‑to‑many con tipo de vínculo: _principal, sustituto, complementario, desconocido_.
    
- **Versionado**: cada receta tiene versión y fecha de vigencia (para el feedback evolutivo post‑obra).
    

### B. Lógica de matching

1. **Normalización** (NLP + reglas): limpiar descripciones de remitos/facturas (marca, formato, variantes) y mapear a un código de Producto.
    
2. **Reglas de equivalencia**: buscar coincidencias en Sinonimias y Compatibilidades; si match ≥ umbral → sugerir rubros candidatos.
    
3. **Contexto de obra**: ponderar por rubros activos, avances y recetas de esa obra.
    
4. **Detección de sustitución**: si el Producto no está en la receta del rubro, pero es equivalente (p. ej., _hidrófugo_ ↔ _Viapol 7000_), clasificar como **sustituto** y disparar _pregunta de confirmación_.
    
5. **Composición**: productos compuestos (sistemas impermeables de varias manos) se reconocen como **kits**; se reparte el consumo entre rubro(es) involucrados.
    

### C. Flujo de consulta/validación en obra

- **Caso 1 – Producto desconocido**: "Ingresó _Viapol 7000_ (impermeabilizante) sin receta asociada. ¿Se usará en **Impermeabilización de muros** en lugar de **hidrófugo**?" → opciones: _Sí (sustituto de Hidrófugo)_ / _No, uso en otro rubro_ / _Mantener en stock_.
    
- **Caso 2 – Ajuste de proceso**: "Se detectó una compra asignada a este rubro que no corresponde al rubrado original. ¿Deseás modificar el rubro?" → si redefine: actualizar **receta v+1** para próximas obras.
    
- **Caso 3 – Producto multi‑rubro**: "Membrana líquida aplicada en baños y azotea" → asistente propone **split de imputación** por frente/área según metraje.
    

### D. Reglas de gobierno del catálogo

- **Curaduría**: responsable técnico aprueba nuevas relaciones Producto↔Rubro y cambios en recetas.
    
- **Umbrales**: por familia, definir _match score_ mínimo para imputación automática.
    
- **Listas blancas/negras**: marcas aprobadas/evitadas por desempeño o garantía.
    
- **Back‑learning**: cada validación en obra alimenta Sinonimias y Compatibilidades.
    

### E. Integración con M‑01 y M‑02

- En **M‑01** (stock): el matching permite **imputar consumos** aunque el producto no coincida 1:1 con la receta presupuestada.
    
- En **M‑02** (presupuestos): si hay **sustitución** recurrente que cambia costo/rendimiento, se propone **actualizar PC/PTJ** y, de corresponder, disparar **VO**.
    

### F. KPIs

- % de compras **mapeadas automáticamente** a rubro.
    
- Nº de **consultas de validación** por quincena y tiempo medio de resolución.
    
- **Impacto por sustituciones** en costo y rendimiento (Δ vs receta original).
    
- **Cobertura del catálogo**: productos con ficha técnica y relaciones activas.
    

### G. Workflows tipo

**WF10 – Impermeabilizante distinto al presupuestado**

1. Ingreso: _Viapol 7000_ 60 baldes.
    
2. Motor de equivalencias lo mapea a familia _impermeabilizante membrana líquida_.
    
3. Detecta que receta del rubro espera _hidrófugo_ → abre consulta al jefe de obra.
    
4. Jefe confirma sustitución para muros húmedos; se recalcula **rendimiento esperado** y **costo unitario real** del rubro.
    
5. Si el cambio afecta alcance/costo contractual → se genera **RFC/VO**; si no, se registra como **ajuste interno** y se alimenta la receta v+1.
    

**WF11 – Revoque con capa adicional**

1. Avance reporta _yeso fino_ + capa de _yeso mecafino_.
    
2. Sistema propone: **subpartida** en Revoque de yeso (material + HH extras) o **nuevo rubro**.
    
3. Según elección, se actualiza PR‑FC y se compara contra PC; alerta de **desvío de rendimiento**.
    
4. Feedback: catálogo agrega _mecafino_ como **complementario** del rubro para futuras obras.