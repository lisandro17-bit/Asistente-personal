# Módulo compras — con **Nota de Pedido**, **Cotización (6M)** y **Asignación GUI**

## Definiciones

- **Nota de Pedido (NP)**: documento emitido por **Obra** (vía chatbot) que deja constancia de que se solicita material a Compras. No es una OC.
    
- **Cotización (COT-6M)**: “prepedido” generado **automáticamente 6 meses** antes del inicio del rubro (o manual con comando). **Sus cantidades provienen del PR-FC (forecast)**, que el **Jefe de Obra** debe actualizar previamente con rendimientos esperados más recientes.
    
- **RFQ**: ronda de cotizaciones armada por Compras en conjunto con Obra (con asistencia del bot) para el paquete de la COT-6M y/o NPs abiertas.
    
- **Orden de Compra (OC)**: documento emitido por **Compras** al proveedor tras aprobación humana; es el registro formal del pedido a proveedor.
    

## Flujo end-to-end

1. **Forecast primero**
    
    - Jefe de Obra actualiza **rendimientos esperados** del rubro en PR-FC. Eso define **cantidades base**.
        
2. **COT-6M (automática o manual)**
    
    - A **–180 días** (configurable) del inicio del rubro, el sistema crea **COT-6M** con los ítems y cantidades **desde el forecast** (considerando stock y buffers).
        
    - Se prepara el paquete para **RFQ** (incluye importables, incoterms, lotes sugeridos por etapa).
        
3. **Nota de Pedido (desde Obra, por chat)**
    
    - Obra emite **NP** (“/nota yeso fino 60 bolsas Obra A Frente B para 15/11”), quedando el registro formal del pedido a Compras.
        
    - La NP sugiere cantidades basadas en **forecast** y en la **COT-6M** vigente (si existe), pero Obra puede ajustarlas.
        
4. **Consolidador de Compras (GUI + IA)**
    
    - Compras ve **COT-6M + NPs** en una bandeja, agrupa, edita, **lanza/gestiona RFQs**, y con una **GUI optimizada** asigna **líneas → proveedores** (split por precio, plazo, calidad).
        
    - El chatbot asiste con: **histórico de precios**, **últimas OCs**, **PU de referencia**, **tendencias**, lead times e importación.
        
5. **Aprobación humana y emisión de OCs**
    
    - **Siempre validado por una persona**: el bot **no decide**. Compras aprueba la asignación y **emite OCs** (pueden ser por proveedor y en lotes).
        
    - Envío al proveedor (PDF/HTML + condiciones).
        
6. **Recepción en Obra y cierre**
    
    - Obra registra la **recepción** en la **bitácora** (remito/foto, parciales), se concilia **OC ↔ remito** (y opcionalmente factura: 3-way match).
        
    - Se actualizan **precios históricos**, equivalencias y, si hubo sustituciones o desvíos, se propone **ticket de rubrado**.
        

## Reglas clave

- **COT-6M siempre toma cantidades del PR-FC (forecast)**: fomenta planificar con datos actualizados.
    
- El bot **solo sugiere** (cantidades, proveedores, precios de referencia); **Compras decide y aprueba**.
    
- Si el calendario está por debajo del lead time objetivo, se marca **alerta de atraso** y se prioriza RFQ urgente.
    
- Importables se tratan con **landed cost** (incoterms, flete, aranceles, tiempos).
    

## Estados

- **NP**: Borrador → En revisión Compras → Consolidada en RFQ/OC → Cerrada | Rechazada.
    
- **COT-6M**: Generada → En RFQ → Parcialmente cubierta → Cubierta → Expirada.
    
- **RFQ**: Enviada → Recibiendo ofertas → Evaluación → Adjudicada → Cerrada.
    
- **OC**: Aprobada → Enviada → Parcialmente recibida → Completada → Cerrada/Cancelada.
    

## Datos/Entidades

- **NotaPedido**(obra, rubro, frente, ítems, cantidades_solicitadas, fecha_objetivo, urgencia, referencia_forecast, adjuntos).
    
- **Cotizacion6M**(obra, rubro, fecha_inicio_rubro, ítems, cantidades_forecast, importables, lotes, lead_time).
    
- **RFQ**(proveedores invitados, fecha_límite, specs técnicas, respuestas).
    
- **Asignación**(línea→proveedor, precio, plazo, condiciones).
    
- **OC**(proveedor, líneas, precios, plazos, entregas, estado).
    
- **Recepción**(remito, cantidades, fotos, fecha, conciliación).
    

## Comandos & GUI

- `*/nota <ítem> <cant> <UM> <obra> [frente] [fecha]*` → crea NP.
    
- `*/cotizar6m <obra> <rubro>*` → genera/actualiza COT-6M desde forecast.
    
- `*/rfq <cotizacion#|obra:rubro>*` → arma RFQ (siempre revisada por Compras).
    
- `*/comparar <ítem>*` → histórico de precios/proveedores.
    
- **GUI Compras**: tablero para **asignar líneas** a proveedores, ver RFQs, NPs y COT-6M, y emitir OCs.
    

## Ejemplo breve

- Rubro **Seco** inicia **01/04** → el **01/10** se crea **COT-6M** con cantidades del **forecast** (placas, perfiles, tornillos).
    
- En noviembre, Obra emite una **NP** por lotes de arranque.
    
- Compras consolida COT-6M + NP, lanza **RFQ**, asigna líneas (importación de placas, local para tornillería), **aprueba** y **emite OCs**.
    
- Obra recibe, registra en **bitácora**, se concilia y se actualizan históricos.