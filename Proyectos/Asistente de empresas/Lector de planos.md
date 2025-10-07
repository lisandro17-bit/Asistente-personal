
## 🟦 Lector de Planos 2D para Metrajes

- **Entrada**
    
    - Archivos DWG/DXF (APL 2D).
    - Memoria descriptiva DWG
    - Reglas de medición predefinidas (YAML/JSON o plantillas en la UI).
    - Escala/unidades configurables o referencia manual.

- **Motor de cálculo (determinístico, sin IA)**
    
    - Lectura de capas, polilíneas, hatches y bloques (`ezdxf`).
    - Operaciones geométricas (áreas, longitudes, conteos) con `shapely`/`rtree`.
    - Filtros por capas, nombres de bloque, espesores.
    - Deducciones automáticas (ej. descontar vanos de muros).
    - Manejo de tolerancias y limpieza de geometría.

- **Validación visual**
    
    - Render a SVG/Canvas con colores por regla.
    - Overlay de elementos medidos y descontados.
    - Tooltips: entidad usada + valor calculado.

- **Salida**
    
    - Tabla de metrajes (resumen + detalle).
    - Exportación a Excel/PDF.
    - Paquete reproducible (plano normalizado + reglas + resultado).

- **Uso previsto**
    
    - Extremadamente sencillo: subir plano → elegir reglas → calcular → exportar.
    - Plantillas listas: muros, plateas, revoques, aberturas, etc.
    - Usuario sin conocimientos técnicos puede generar metrajes validados.
        
- **Tecnología base**
    
    - Python (FastAPI backend).
    - Librerías: `ezdxf`, `shapely`, `rtree`, `openpyxl`.
    - Frontend: React/Electron con visor SVG.
    - Conversión DWG→DXF (ODA File Converter).