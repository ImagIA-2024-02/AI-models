# Modelo para el reconocimiento de Autores
## Descripción del Modelo
Este modelo fue desarrollado en Google Colab utilizando TensorFlow. Su objetivo es clasificar obras de arte según el autor, utilizando una arquitectura de MobileNetV2 como base para optimización y velocidad, ideal para dispositivos móviles. La construcción del modelo incluyó varios pasos, desde la carga y preprocesamiento de datos hasta la creación y el entrenamiento de la red neuronal.

## Proceso de Entrenamiento
- Aumentación de Datos: Se utilizó ImageDataGenerator para simular condiciones reales de captura de imágenes, como rotaciones, desplazamientos y ajustes de brillo.
- Entrenamiento de Capas Superiores: Inicialmente, solo se entrenaron las capas superiores, con las capas base congeladas para evitar el sobreajuste temprano.
- Fine-Tuning: Posteriormente, se descongelaron capas adicionales de MobileNetV2 para mejorar la precisión en las últimas etapas del entrenamiento.
## Problemas Encontrados
Conversión a TensorFlow Lite: Durante la conversión a TFLite, el modelo experimentó errores de compatibilidad con el delegado XNNPack. Este problema se resolvió deshabilitando el delegado en la configuración del intérprete.
Errores de Dimensión: Durante las pruebas, hubo varios problemas con la dimensión del tensor de entrada. Esto se resolvió ajustando la redimensión y la normalización de las imágenes.
## Link al Notebook de Google Colab
[[Aquí agrega el link a tu notebook de Colab](https://colab.research.google.com/drive/1-MFu6PRMrIcmPzDOvuuu1QpHxlRLSM6t?usp=sharing)]