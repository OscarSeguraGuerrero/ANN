# ANN
Trabajo FSI
# Clasificación de Logos de Comida Rápida
Este proyecto implementa y compara diferentes arquitecturas de Redes Neuronales Convolucionales (CNN) utilizando **PyTorch** para la clasificación de logotipos de cadenas de comida rápida. El objetivo es analizar cómo afectan los diferentes hhiperparámetros al rendimiento del modelo.

## Dataset
Se ha utilizado el conjunto de datos de Kaggle: `logos-bk-kfc-mcdonald-starbucks-subway-none`.
 - Contiene 6 clases: Burger King, KFC, McDonalds, Starbucks, Subway, Other
 - Estructura: Una carpeta en la que el 80% del contenido esta dedicado al **entrenamiento** y el 20% a la **validación**. Una segunda carpeta dedicada al **test**
 - Preprocesamiento: Redimensionamiento a **64x64 píxeles**, normalización con media **(0.5, 0.5, 0.5)** y desviación estándar **(0.5, 0.5, 0.5)**.

## Metodología y Experimentos
Se han realizado un total de 5 experimentos.
### 1. Modelo Base (BaseCNN)
 - **Arquitectura:** 
 - **Hiperparámetros:**
 - **Resultados:**
### 2. Cambio de Optimizador (SGD)
 - **Arquitectura:** 
 - **Hiperparámetros:**
 - **Resultados:**
### 3. Regularización (DropoutCNN)
 - **Arquitectura:** 
 - **Hiperparámetros:**
 - **Resultados:**
### 4. Red Profunda (DeepCNN)
 - **Arquitectura:** 
 - **Hiperparámetros:**
 - **Resultados:**
### 5. Data Augmentation
 - **Arquitectura:** 
 - **Hiperparámetros:**
 - **Resultados:**
