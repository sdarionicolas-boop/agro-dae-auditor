# agro-dae-auditor
Auditoría de series temporales agrícolas mediante Denoising Autoencoders (LSTM). Validación de coherencia ecofisiológica en datos satelitales (NDVI/NDMI) y climáticos.
Agro-DAE-Auditor: Auditoría de Calidad con Coherencia Ecofisiológica
Este repositorio implementa un flujo de trabajo avanzado para la validación y limpieza de series temporales agrícolas (NDVI, NDMI y variables climáticas) utilizando Deep Learning ejecutado en entorno local.

El Problema: Ruido vs. Estrés Real
En la agricultura de precisión, las caídas abruptas en los índices de vegetación a menudo son causadas por nubosidad o fallas en la captura de imágenes, no por un problema real en el cultivo. Este proyecto utiliza un Denoising Autoencoder (DAE) para aprender la dinámica temporal real y separar la señal del ruido.

Características Principales
Arquitectura LSTM: Captura la estacionalidad compleja mediante ventanas temporales de 12 meses.

Denoising Robusto: Entrenado para reconstruir señales corrompidas artificialmente, aprendiendo la "fisiología subyacente" del cultivo.

Score de Anomalía: Genera una métrica de confianza para auditar automáticamente si un dato es representativo o debe ser descartado.

Coherencia Ecofisiológica: Mantiene la relación biológica entre vigor (NDVI) y contenido hídrico (NDMI) durante la reconstrucción.

Uso
El sistema recibe un archivo CSV con series temporales y genera:

Un reporte de Score de Anomalía.

Una serie temporal "limpia" recomendada para alimentar modelos de predicción como Random Forest.
