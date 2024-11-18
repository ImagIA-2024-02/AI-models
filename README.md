# Descripción del Modelo para el Reconocimiento de Autores
Este modelo fue desarrollado en Google Colab utilizando TensorFlow. Su objetivo es clasificar obras de arte según el autor, utilizando una arquitectura de MobileNetV2 como base para optimización y velocidad, ideal para dispositivos móviles. La construcción del modelo incluyó varios pasos, desde la carga y preprocesamiento de datos hasta la creación y el entrenamiento de la red neuronal.

## Proceso de Entrenamiento
- Aumentación de Datos: Se utilizó ImageDataGenerator para simular condiciones reales de captura de imágenes, como rotaciones, desplazamientos y ajustes de brillo.
- Entrenamiento de Capas Superiores: Inicialmente, solo se entrenaron las capas superiores, con las capas base congeladas para evitar el sobreajuste temprano.
- Fine-Tuning: Posteriormente, se descongelaron capas adicionales de MobileNetV2 para mejorar la precisión en las últimas etapas del entrenamiento.
## Problemas Encontrados
Conversión a TensorFlow Lite: Durante la conversión a TFLite, el modelo experimentó errores de compatibilidad con el delegado XNNPack. Este problema se resolvió deshabilitando el delegado en la configuración del intérprete.
Errores de Dimensión: Durante las pruebas, hubo varios problemas con la dimensión del tensor de entrada. Esto se resolvió ajustando la redimensión y la normalización de las imágenes.
## Link al Notebook de Google Colab
[[Enlace al notebook en Colab](https://colab.research.google.com/drive/1zNUN2m8Yqs4IebR2McDBQSlPpxp4yyfw?usp=sharing)]
[[Cuanderno descargado en este Repositorio](/ReconocimientoAutorSimpifPlayground.ipynb)]

# Descripción del Modelo de Restauración de Imágenes
Este proyecto implementa un modelo de restauración de imágenes desarrollado en VSCode usando TensorFlow. El modelo sigue una arquitectura de tipo U-Net, diseñada para transformar imágenes degradadas en versiones restauradas, corrigiendo efectos como ruido, desenfoque, desvanecimiento de colores y grietas.

## Proceso de Entrenamiento
### Dataset
- Se generó un conjunto de datos con imágenes degradadas artificialmente. Las degradaciones incluyen adición de ruido, desvanecimiento de colores aleatorio, desenfoque, y superposición de texturas de grietas.
- Las imágenes originales fueron preprocesadas para evitar sobresaturación y se aplicaron métodos probabilísticos para garantizar una mayor variabilidad en las degradaciones.
### Entrenamiento
- El modelo fue entrenado para aprender a restaurar estas imágenes degradadas, utilizando la función de pérdida de error cuadrático medio (MSE) para medir la diferencia entre las imágenes restauradas y las originales.
- Los datos se manejaron en lotes pequeños para optimizar el uso de memoria.

## Problemas Enfrentados y Soluciones Implementadas
### 1. Saturación de Colores:
Al inicio, el modelo sobresaturaba los colores de las imágenes restauradas. Para solucionar esto:
- Se ajustó el proceso de degradación, implementando desvanecimiento de colores aleatorio con probabilidades controladas.
- Esto aumentó la diversidad del dataset, mejorando la capacidad del modelo para generalizar.
### 2. Uso de Memoria:
Durante el entrenamiento en Google Colab y sistemas locales con GPU, surgieron limitaciones de memoria:
- Se redujo el tamaño de lote (batch_size) y se configuró el uso dinámico de memoria en la GPU.
- Se implementaron pipelines con tf.data.Dataset para cargar los datos por lotes, optimizando el rendimiento.
### 3. Manchas Negras en Imágenes Restauradas:
Inicialmente, las imágenes restauradas presentaban manchas negras debido a una falta de diversidad en el dataset.
- Se ampliaron las variaciones en las texturas de grietas y degradaciones.
- Además, se incluyó protección para áreas blancas, evitando que el ruido degradara regiones clave de las imágenes originales.
### 4. Formato y Portabilidad:
El modelo se guardó en formato TensorFlow (SavedModel) para permitir vsu carga y uso eficiente, reduciendo el impacto en la memoria RAM durante las evaluaciones.
## Link al Notebook
[[Cuanderno descargado en este Repositorio](/restorationv2/PlaygroundRegeneration.ipynb)]
## Conclusión
Esta versión del modelo ha demostrado ser más robusta y eficiente para restaurar imágenes degradadas, ofreciendo resultados significativamente mejores gracias a las optimizaciones realizadas en el dataset, el entrenamiento y el manejo de recursos.

# Descripción del Modelo Delimitador con YOLOv5
Este modelo fue desarrollado en Google Colab utilizando PyTorch y exportado a TensorFlow Lite para su implementación en dispositivos móviles. Su objetivo principal es detectar cuadros u obras de arte dentro de imágenes, generando coordenadas precisas de las áreas delimitadas (bounding boxes). El modelo es ideal para aplicaciones que requieren alta precisión y velocidad, como aplicaciones móviles o sistemas embebidos.

## Proceso de Entrenamiento
- Modelo Base: Se utilizó la arquitectura YOLOv5, conocida por su balance entre precisión y velocidad, como base para la detección de objetos.
- Dataset Personalizado: Las imágenes fueron etiquetadas en formato YOLO para entrenar el modelo en la detección de cuadros dentro de diversos contextos.
- Aumentación de Datos: Incluyó rotaciones, cambios de escala y ajustes de brillo/contraste para simular escenarios reales.
- Entrenamiento: Se entrenó el modelo en múltiples épocas, utilizando GPUs de Google Colab para acelerar el proceso. Se configuró un umbral de confianza para filtrar detecciones menos precisas.
## Conversión a TensorFlow Lite
- Exportación: El modelo entrenado en PyTorch fue exportado directamente a TensorFlow Lite usando el script export.py de Ultralytics.
- Optimización: Se aplicó la optimización de cuantización para reducir el tamaño del modelo y mejorar su rendimiento en dispositivos con recursos limitados.
## Problemas Encontrados
1. Errores de Compatibilidad: Durante la conversión a TensorFlow Lite, surgieron problemas con ciertas capas del modelo. Esto se resolvió ajustando el script de exportación.
2. Configuración de Entrada: Se detectaron problemas con las dimensiones de entrada durante las pruebas. Esto se solucionó redimensionando las imágenes a 640x640 y normalizándolas a valores entre 0 y 1.
3. Interpretación de Resultados: Al principio, los valores de salida del modelo no coincidían con las expectativas. Esto requirió una reconfiguración de la estructura de salida del modelo.
## Link al Notebook de Google Colab
[[Enlace al notebook en Colab](https://colab.research.google.com/drive/1AiyJ4cQnDVnyxSng1UCqZ4kaluPIcAe6?usp=sharing)]
[[Cuanderno descargado en este Repositorio](/PlaygroundArtworkReco.ipynb)]

Este modelo está listo para ser implementado en aplicaciones móviles, donde se pueden utilizar bounding boxes generados para procesar imágenes y brindar una experiencia de usuario óptima.