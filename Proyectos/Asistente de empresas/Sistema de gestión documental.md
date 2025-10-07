
### 🔑 Estructura base (ya sin carpetas físicas tipo Windows)

- El sistema **no depende del nombre del archivo ni de la ruta**.
- Cada documento tiene un **ID único** (ej. `DOC-000123`).
- Toda la organización se hace por **metadatos (etiquetas)**.
- Los metadatos son **ocultos para el usuario**, pero el bot los usa para ordenar, buscar y relacionar.
## 🏷️ Metadatos principales (ejemplos)

- **Área** (`ADM`, `CON`, `FIN`, `COM`, etc.).
- **Categoría** (`PROY`, `PROC`, `DOCU`, `IDEA`, `CONO`, `REP`).
- **Tipo de documento** (`FACT`, `REC`, `CHEQ`, `CONT`, `PRES`, etc.).
- **Mercado** (`LOC`, `EXT`, `DIG`).
- **Proyecto** (`PRJ:EDIFCENT`).
- **Contraparte** (`CP:ClienteX`).
- **Estado** (`BORR`, `REV`, `APROB`, `FIRM`, `VENC`).
- **Versión** (`v1`, `v1.2`, `v2`).
- **Fecha clave** (creación, vencimiento, modificación).
- **Responsable / dueño** (`OWN:MFerreira`).
- **Sensibilidad** (`PUB`, `INT`, `CONF`).

👉 El usuario no necesita escribir nada: el bot etiqueta con base en la orden y pregunta lo que falta.

## 🔀 Múltiples rutas / atajos

- Un mismo documento puede **pertenecer a varios “vistas”** sin duplicarse.
- Ejemplo:
    - Ruta 1: `COM/LOC/CLIENTEX/PRESUPUESTOS`
    - Ruta 2: `PROY/EDIFCENT/COMERCIAL/PRESUPUESTOS`
- El sistema genera “atajos virtuales” → mismo archivo, distintos accesos.

## 📜 Legajo del documento (historial)

Cada archivo mantiene un **legajo inmutable** con:

- **Historial de ubicaciones virtuales** (todas las vistas en que estuvo).
- **Acciones realizadas** (creado, editado, aprobado, movido).
- **Usuarios que intervinieron**.
- **Fechas** de cada evento.