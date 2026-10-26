# WX Analytics: Clasificador de Confort Térmico (Fase 2)

## 📌 Descripción del Proyecto
Implementación de un modelo preentrenado de Procesamiento de Lenguaje Natural (NLP) basado en el ecosistema Hugging Face. Este prototipo procesa tickets de *Workspace Experience* (WX) para detectar fricciones térmicas en el corporativo y actúa como disparador preventivo para controladores HVAC (BACnet). Diseñado para salvaguardar el confort y el OPEX.

## 📂 Documentación del Dataset y Scripts de Soporte
**1. Origen del Dataset:**
El dataset `wx_tickets_bbva.csv` fue generado sintéticamente de forma *ad-hoc* mediante un script de Python. Simula la telemetría real de un sistema de tickets corporativos enfocado en la experiencia de usuario (Workspace Experience) sobre el confort térmico en un entorno Open Space.

**2. Estructura de los Datos (Diccionario):**
El archivo consta de 50 registros con 3 campos críticos:
* `ticket_id` (String): Identificador único del reporte (ej. WX-001). Llave primaria para cruce con Facility Management.
* `texto` (String): Comentario del colaborador en lenguaje natural (ej. "Hace muchísimo frío").
* `etiqueta_real` (String): Ground Truth de negocio (`POS`=Confort, `NEU`=Consulta/Rutina, `NEG`=Fricción térmica).

**3. Script Reproducible:**
La generación de datos no fue manual. Se construyó mediante un script reproducible en **Python (Pandas)**, incrustado en la **Celda 1** del cuaderno principal de Google Colab. Al ejecutar la celda, el entorno genera el dataframe y compila el archivo físico CSV automáticamente.

## 📊 Justificación del Modelo Seleccionado
El análisis de *trade-offs* entre latencia y exactitud determinó lo siguiente:
* Se descartaron los modelos multilingües y destilados (`bert-multilingual` y `distilbert-student`) debido a una degradación inaceptable de precisión (F1-Score del 70%).
* **Decisión:** Se seleccionó **`pysentimiento/robertuito-sentiment-analysis`**. El modelo demostró una asertividad perfecta (Accuracy 100%) con una latencia operativa de ~50 ms por ticket. Esta velocidad (*ultra-low latency*) permite integrarlo al ecosistema IoT sin riesgo de falsos positivos en Facility Management.
