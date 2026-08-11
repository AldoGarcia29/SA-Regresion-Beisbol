# SA - Regresión con beisbol.csv

Proyecto correspondiente al ejercicio 1 de la segunda evaluación de la materia **SA: Análisis Supervisado y No Supervisado**.

## Objetivo

Predecir la cantidad de carreras anotadas (`runs`) a partir del número de bateos (`bateos`) utilizando un algoritmo de regresión.

## Conjunto de datos

El archivo `beisbol.csv` contiene información de 30 equipos:

- `equipos`: nombre del equipo.
- `bateos`: número de oportunidades de bateo.
- `runs`: carreras anotadas.

La columna `equipos` se utiliza únicamente para identificar los puntos en las gráficas. El modelo utiliza `bateos` como variable de entrada y `runs` como variable objetivo.

## Algoritmo utilizado

Se implementó una **regresión polinómica con regularización Ridge**.

La regresión polinómica permite representar una posible relación curva entre los bateos y las carreras. Ridge agrega regularización para controlar los coeficientes y reducir el riesgo de sobreajuste.

El modelo se construyó mediante un `Pipeline` formado por:

1. `PolynomialFeatures`
2. `StandardScaler`
3. `Ridge`

## Diseño del modelo

El notebook realiza los siguientes pasos:

1. Importación de bibliotecas.
2. Lectura y exploración de `beisbol.csv`.
3. Eliminación de columnas innecesarias.
4. Revisión de valores faltantes.
5. Definición de las variables de entrada y objetivo.
6. División en 80 % para entrenamiento y 20 % para prueba.
7. Construcción del pipeline.
8. Búsqueda de hiperparámetros.
9. Entrenamiento del mejor modelo.
10. Evaluación mediante métricas.
11. Generación de gráficas.
12. Guardado del modelo entrenado.

## Optimización

Se utilizó `GridSearchCV` con validación cruzada de cinco particiones.

Los hiperparámetros evaluados fueron:

- Grado polinómico: 1, 2 y 3.
- Alpha de Ridge: 0.01, 0.1, 1, 10 y 100.

La mejor configuración encontrada fue:

- Grado polinómico: `3`
- Alpha: `1`

## Resultados

Las métricas obtenidas fueron:

| Métrica | Resultado |
|---|---:|
| RMSE de validación cruzada | 63.397 |
| MAE de prueba | 51.583 |
| RMSE de prueba | 71.969 |
| R² de prueba | -0.506 |

El R² negativo indica que `bateos` por sí solo no explica completamente la cantidad de carreras. También influyen otras características deportivas que no están incluidas en el conjunto.

## Gráficas

El notebook contiene:

- Gráfica de dispersión del comportamiento entre bateos y carreras.
- Curva generada por el modelo optimizado.
- Gráfica comparativa de valores reales contra predichos.
- Identificación de los equipos utilizados en la prueba.

## Contenido del repositorio

```text
SA-Regresion-Beisbol/
├── regresion_beisbol.ipynb
├── beisbol.csv
└── models/
    └── modelo_regresion_beisbol.joblib
