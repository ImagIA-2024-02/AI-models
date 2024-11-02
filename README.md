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
[[Enlace al notebook en Colab](https://colab.research.google.com/drive/1-MFu6PRMrIcmPzDOvuuu1QpHxlRLSM6t?usp=sharing)]

# Descripción del Modelo de Restauración de Imágenes
Este proyecto utiliza un modelo de restauración de imágenes desarrollado en Google Colab usando TensorFlow. El modelo sigue una arquitectura de tipo U-Net para transformar imágenes degradadas en versiones restauradas, eliminando efectos como ruido, desenfoque y desvanecimiento de colores.

## Proceso de Entrenamiento
- Dataset: Se creó un conjunto de datos con imágenes degradadas artificialmente mediante técnicas como la adición de ruido, desvanecimiento de colores, desenfoque y superposición de texturas de grietas.
- Entrenamiento: El modelo fue entrenado para aprender a restaurar estas imágenes degradadas, utilizando una función de pérdida de error cuadrático medio (MSE) para comparar la imagen restaurada con la imagen original.

## Problemas Enfrentados
Durante el desarrollo, surgieron algunos desafíos:

- Saturación de Colores: Al inicio, el modelo tendía a sobresaturar los colores de las imágenes restauradas. Se ajustó el proceso de degradación para que el desvanecimiento de colores fuera aleatorio, mejorando así la variabilidad del dataset y la capacidad del modelo para generalizar.
- Uso de Memoria: El entrenamiento en Google Colab con GPU enfrentó limitaciones de memoria, lo que requirió ajustes en el tamaño de lote y la estructura del modelo.
## Link al Notebook de Colab
[[Enlace al notebook en Colab](https://colab.research.google.com/drive/1G2QUdpgXdyjSKZ4eeszoDaZTYmW1hTQS?usp=sharing)]