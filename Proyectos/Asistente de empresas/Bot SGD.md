### 📌 Funciones del bot de consulta

- **🔎 Búsqueda semántica avanzada**
    - Entiende consultas en lenguaje natural (ej. “el presupuesto de junio para EdifCentral”).
    - Soporta filtros por fecha, proyecto, cliente, tipo de documento, estado, responsable, etc.
        
- **📂 Rutas múltiples / vistas virtuales**
    - Permite acceder al mismo documento desde varias rutas lógicas (por proyecto, por cliente, por mercado…).
    - Sugiere atajos adicionales si detecta patrones de uso.
        
- **📜 Legajo histórico de documentos**
    - Muestra dónde estuvo ubicado el archivo en el pasado.
    - Registra quién lo creó, movió, aprobó o modificó y en qué fecha.
    - Permite recuperar archivos que “desaparecieron” de su ubicación actual.
        
- **🤖 Completar información faltante**
    - Si la orden del usuario está incompleta, pregunta lo que falta (ej. estado, versión, cliente).
    - Sugiere valores comunes (“¿en revisión o terminado?”).
        
- **🔀 Historial de acciones de usuario**
    - Recuerda qué búsquedas hiciste y te permite repetirlas.
    - Sugiere accesos rápidos a consultas frecuentes.
        
- **📊 Reportes automáticos**
    - “Mostrame todos los contratos que vencen este mes.”
    - “Listá los presupuestos en revisión del área comercial.”
        
- **⚠️ Manejo de excepciones**
    - Si un archivo fue eliminado o falta, el bot lo indica y propone:
        > “El documento no está disponible en la ubicación actual, pero su última copia estaba en… ¿Querés restaurarlo?”
        
- **💬 Interacción colaborativa**
    - Puede discutir con el usuario cómo organizar archivos o crear nuevas vistas.
    - Simula escenarios antes de aplicar cambios (vista previa del reordenamiento).