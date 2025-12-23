# ANN
# Clasificación de Logos de Comida Rápida
Este proyecto implementa y compara diferentes arquitecturas de Redes Neuronales Convolucionales (CNN) utilizando **PyTorch** para la clasificación de logotipos de cadenas de comida rápida. El objetivo es analizar cómo afectan los diferentes hhiperparámetros al rendimiento del modelo.

## Dataset
Se ha utilizado el conjunto de datos de Kaggle: [logos-bk-kfc-mcdonald-starbucks-subway-none](https://www.kaggle.com/datasets/kmkarakaya/logos-bk-kfc-mcdonald-starbucks-subway-none/data).
 - Contiene 6 clases: Burger King, KFC, McDonalds, Starbucks, Subway, Other
 - Estructura: Una carpeta en la que el 80% del contenido esta dedicado al **entrenamiento** y el 20% a la **validación**. Una segunda carpeta dedicada al **test**
 - Preprocesamiento: Redimensionamiento a **64x64 píxeles**, normalización con media **(0.5, 0.5, 0.5)** y desviación estándar **(0.5, 0.5, 0.5)**.

## Metodología y Experimentos
Se han realizado un total de 5 experimentos.
### 1. Modelo Base (BaseCNN)
 - **Arquitectura:** 3 bloques convolucionales (Conv2d + ReLU + MaxPool) seguidos de 2 capas lineales.
 - **Hiperparámetros:** Optimizador `Adam` (lr=0.001), 15 épocas.
 - **Resultados:** Rápida convergencia pero posible Overfitting.
### 2. Cambio de Optimizador (SGD)
 - **Arquitectura:** Misma arquitectura `BaseCNN`.
 - **Hiperparámetros:** Optimizador `SGD` (lr=0.01, momentum=0.9).
 - **Resultados:** Fue más lento pero arregló el problema del posilble overfitting.
### 3. Regularización (DropoutCNN)
 - **Arquitectura:** Arquitectura Base
 - **Hiperparámetros:** Capa de `Dropout (0.5)` antes de la clasificación final.
 - **Resultados:** Mejoró un poco la generalización respecto a la arquitectura base.
### 4. Red Profunda (DeepCNN)
 - **Arquitectura:** Se aumentó la profundidad a **4 capas convolucionales**, duplicando filtros progresivamente (32 -> 64 -> 128 -> 256).
 - **Hiperparámetros:** Mismos hiperparámetros que en `BaseCNN`.
 - **Resultados:** Se aprecia una mejora en los resultados y una mayor estabilidad en los resultados. 
### 5. Data Augmentation
 - **Técnica:** Se aplicaron transformaciones aleatorias al set de entrenamiento en tiempo real:
   - `RandomHorizontalFlip`: Volteo horizontal.
   - `RandomRotation(15)`: Rotación de ±15 grados.
   - `ColorJitter`: Variación de brillo y contraste (0.2).
 - **Resultados:** Redujo mucho el overfitting, experimento con mejores resultados de estos 5 junto a la red profunda.

## Transfer Learning
Utilizamos una red neuronal ya entrenada para combinarla con la nuestra y así tratar de obtener mejores resultados.
 - **Modelo:** Se utilizó una red **ResNet18** preentrenada con el dataset **ImageNet** (1.2 millones de imágenes).
 - **Resultado:** Rendimiento superior y convergencia inmediata.
 - **¿Por qué funciona mejor?** En lugar de aprender a "ver" desde cero (bordes, texturas, formas), utilizamos una red que ya sabe reconocer características visuales complejas. El proceso:
   - **Carga de Pesos:** Se importa el modelo con los pesos aprendidos en ImageNet.
   - **Congelación (Freezing):** Se congelan las capas convolucionales (feature extractors) para no destruir la información preaprendida.
   - **Adaptación:** Se sustituye la última capa lineal (que clasificaba 1000 clases de ImageNet) por una nueva capa adaptada a nuestras **6 clases** de comida rápida.
   - **Entrenamiento:** Se entrena solamente esta última capa.
 
## Conclusiones

 - **Limitación de los datos:** Las redes propias (Fase 1) llegaron a un techo de rendimiento debido al tamaño limitado del dataset.
 - **Efectividad del Transfer Learning:** El uso de ResNet18 demostró ser la estrategia más eficiente, alcanzando una precisión casi perfecta con muy pocas épocas de entrenamiento. Esto valida que, para problemas con pocos datos, reutilizar redes preentrenadas es superior a diseñar arquitecturas desde cero.

