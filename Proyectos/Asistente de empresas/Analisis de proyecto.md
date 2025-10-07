
### **Bloque 1 – Input inicial y normativa**

Este módulo recibe el número de padrón, ubica el terreno y consulta la normativa vigente. El usuario puede definir preferencias estratégicas (calidad, pisos, mix de apartamentos, estacionamientos, amenities), y la herramienta devuelve un **resumen claro de lo que permite la normativa**. El cliente confirma o ajusta estos datos antes de avanzar.

**Características principales:**

- Carga de padrón y ubicación.
- Preferencias de proyecto: costo/calidad, pisos, mix tipológico, estacionamientos, amenities.
- Consulta automática de normativa: altura, FOS/FOT, retiros, usos, estacionamientos.
- Resumen ejecutivo de normas con fuente y versión.
- Validación del usuario antes de seguir al modelado.

---

### **Bloque 2 – Modelado 3D y documentación**

Con la normativa confirmada, el sistema genera un **modelo 3D básico (massing)** del edificio y calcula superficies construidas y vendibles. También produce **planos esquemáticos** y una ficha técnica con todos los datos del proyecto. Esto permite al cliente visualizar la idea de inmediato y tener métricas objetivas.

**Características principales:**

- Modelo 3D tentativo del edificio según norma y preferencias.
    
- Planos automáticos:
    - Corte transversal.
    - Planta baja.
    - Planta tipo.
    - Planta de SUM/rooftop.

- Ficha técnica en PDF con:
    - Metros construidos y vendibles.
    - Cantidad de apartamentos por tipología.
    - Garajes y amenities.
    - Observaciones y supuestos.

- Ajuste de viabilidad: amenities restan m² vendibles pero suben precio de venta.

---

### **Bloque 3 – Análisis financiero y viabilidad**

Usando los m² calculados y los coeficientes de costo/venta por sector, la herramienta construye un **modelo financiero completo**. Estima inversiones, ventas, cronogramas y flujos de caja, calculando los principales indicadores de retorno para inversores. Los resultados se presentan en un **dashboard interactivo** y documentos exportables.

**Características principales:**

- Cálculo de costos de obra, ingresos y utilidad bruta.
- Flujo de caja mensual con CAPEX, ventas, gastos y deuda.
- KPIs: Costo total, Ingreso total, TIR proyecto, TIR equity, VAN, payback.
- Escenarios: Base / Optimista / Conservador.
- Sensibilidades ±5/10/15% en precio, costo y plazo.
- Dashboard interactivo con gráficos de flujo, estructura de capital y absorción de ventas.
- Exportables:
    - PDF 1-página ejecutivo.
    - Excel con supuestos y cálculos.

---

### **Capacidades generales de la herramienta**

En conjunto, la herramienta **automatiza el ciclo completo de factibilidad**: desde ingresar un padrón hasta entregar un informe financiero y técnico listo para inversores. Permite iterar con el cliente, ajustar supuestos y generar entregables profesionales en cuestión de horas.

**Características generales:**

- Proceso completo automatizado en **n8n**.
- Trazabilidad de supuestos y fuentes en cada salida.
- Iteración guiada con el cliente en cada etapa.
- Escalable: análisis puntual de un padrón o procesamiento masivo de terrenos.
- Entregables claros: planos, ficha técnica, dashboard, KPIs y escenarios de viabilidad.


# 💵 Pricing sugerido para inmobiliarias

- **Fee unitario**: igual que con inversores, USD 900 por estudio.
- **Pack de terrenos**: ej. 5 estudios/mes → USD 3.500 (ahorro para volumen).
- **Plan “Pro inmobiliarias”**: suscripción mensual que les da derecho a cargar X terrenos por mes, con logo y branding de la inmobiliaria en los entregables → fidelización directa.

---

# 🎯 Posicionamiento comercial

- A inversores/desarrolladores: “Te damos un estudio de factibilidad completo en 24 horas.”
- A inmobiliarias: “Convertimos tu terreno en un producto de inversión con planos, métricas y ROI para vender más rápido y mejor.”

---

# 🚀 Estrategia de entrada

1. **Casos piloto**: tomás 1 o 2 inmobiliarias chicas y les hacés un par de estudios gratis o a precio reducido → generás ejemplos concretos.
2. **Muestras visuales**: creás un catálogo de “antes/después”: terreno vacío → ficha + modelo 3D + ROI.
3. **Campaña B2B**: orientada a inmobiliarias premium que venden terrenos grandes o con potencial de desarrollo.

---

👉 Con esto tenés dos flujos de clientes:

- **Inversores/developers** → pagan porque necesitan decidir dónde poner su dinero.
- **Inmobiliarias** → pagan porque necesitan vender más rápido y mejor.