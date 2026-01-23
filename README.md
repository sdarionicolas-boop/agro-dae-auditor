Agro-DAE-Auditor
Auditoría de series temporales agrícolas mediante Denoising Autoencoders (LSTM)

Agro-DAE-Auditor implementa un flujo de trabajo para la auditoría, validación y limpieza de series temporales agrícolas, utilizando Deep Learning aplicado a datos satelitales (NDVI, NDMI) y variables climáticas.

El objetivo del proyecto no es predecir ni recomendar manejo, sino evaluar la confiabilidad de los datos antes de que sean utilizados en modelos productivos o sistemas de toma de decisión.

🧩 El problema: ruido vs. estrés real

En agricultura de precisión, las caídas abruptas de índices de vegetación no siempre reflejan un problema real del cultivo.
Con frecuencia, estos descensos están asociados a:

nubosidad

baja cantidad de imágenes disponibles

ruido en la captura satelital

Distinguir ruido de observación de estrés ecofisiológico real es un paso crítico que suele omitirse.

Agro-DAE-Auditor aborda este problema utilizando un Denoising Autoencoder (DAE) que aprende la dinámica temporal normal del sistema y permite auditar cada observación en función de su coherencia histórica, climática y ecofisiológica.

⚙️ Enfoque metodológico

El sistema se basa en un autoencoder temporal con arquitectura LSTM, entrenado sobre ventanas móviles de 12 meses, lo que permite capturar:

estacionalidad

transiciones fenológicas

relaciones entre índices espectrales y clima

Durante el entrenamiento, las series son corrompidas artificialmente (simulando nubosidad y baja calidad de observación), y el modelo aprende a reconstruir la señal coherente subyacente.

🔍 Características principales

Arquitectura LSTM
Captura dinámicas temporales complejas y estacionales mediante ventanas de 12 meses.

Denoising robusto
El modelo es entrenado para separar señal ecofisiológica de ruido de observación.

Score de anomalía
El error de reconstrucción se utiliza como una métrica de confianza que permite identificar observaciones sospechosas.

Coherencia ecofisiológica
La reconstrucción preserva la relación biológica entre vigor vegetal (NDVI) y estado hídrico (NDMI).

Auditoría previa a modelos productivos
El sistema actúa como una capa de control de calidad antes de alimentar modelos de predicción o zonificación.

📥 Uso general

El sistema recibe como entrada un archivo CSV con series temporales que incluyen:

NDVI

NDMI

variables climáticas (ej. precipitación, temperatura mínima)

métricas de calidad de observación (nubosidad, cantidad de imágenes)

Como salida, el flujo genera:

un reporte de score de anomalía temporal

una serie temporal auditada / limpia, recomendada para ser utilizada en modelos posteriores (por ejemplo, Random Forest u otros enfoques de análisis productivo)

⚠️ Qué hace y qué no hace este proyecto

✔️ Audita la confiabilidad de los datos
✔️ Identifica observaciones inconsistentes
✔️ Mejora la calidad de series temporales

❌ No predice rendimiento
❌ No recomienda manejo agronómico
❌ No reemplaza el criterio técnico

🧠 Idea central

Antes de decidir qué hacer con un cultivo,
conviene saber si el dato con el que decidimos es confiable.

Agro-DAE-Auditor se enfoca exactamente en ese paso previo.

Flujo general de auditoría

El siguiente esquema resume el rol del sistema dentro de un flujo típico de análisis agrícola.
El modelo actúa como una **capa de auditoría previa**, evaluando la confiabilidad de los datos
antes de que sean utilizados en análisis productivos o modelos predictivos.


┌────────────────────┐
│ NDVI / NDMI crudo  │
│ Variables climáticas│
│ Calidad de captura │
└─────────┬──────────┘
          ↓
┌────────────────────┐
│ Denoising          │
│ Autoencoder (LSTM) │
└─────────┬──────────┘
          ↓
┌────────────────────┐
│ Score de anomalía  │
│ (error de reconstr.)│
└─────────┬──────────┘
          ↓
┌────────────────────┐
│ Serie auditada     │
│ (dato confiable)   │
└─────────┬──────────┘
          ↓
┌────────────────────┐
│ KVPI / RF / Otros  │
│ modelos            │
└────────────────────┘

