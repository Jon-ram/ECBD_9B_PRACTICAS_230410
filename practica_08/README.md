# Práctica 08: Visualización de personas diagnosticadas con diabetes en el estado de Puebla

## Descripción

En esta práctica se realiza el análisis geoespacial de un dataset clínico simulado de pacientes del estado de Puebla, con el objetivo de visualizar la distribución de pacientes por municipio y de entrenar modelos de clasificación supervisada capaces de predecir el municipio de un paciente a partir de sus coordenadas GPS (latitud y longitud).

El dataset grupal fue construido a partir de los datasets individuales de 5,000 pacientes generados por cada integrante del equipo en la Práctica 07, fusionados en un único dataset con coordenadas geográficas por municipio.

## Herramientas utilizadas

- **Python 3.13**
- **pandas / numpy** — manipulación y limpieza de datos
- **geopandas / shapely** — manejo de geometrías y polígonos municipales, unión espacial
- **folium** (con los plugins `HeatMap` y `MarkerCluster`) — mapas interactivos
- **matplotlib / seaborn** — gráficas estáticas (barras, matriz de confusión)
- **scikit-learn** — codificación de variables, división de datos y modelos de clasificación (KNN, Random Forest, Regresión Logística)
- **Jupyter Notebook**

## Estructura de carpetas

```
practica_08/
├── data/
│   ├── raw/
│   │   └── dataset_diabetes_puebla.csv      # Dataset grupal con coordenadas
│   └── 21_puebla/
│       └── conjunto_de_datos/
│           └── 21mun.shp                    # Shapefile de municipios de Puebla (INEGI)
├── Analisis_Puebla.ipynb                    # Notebook principal de la práctica
└── README.md
```

## Fuentes geográficas

Los polígonos de los municipios de Puebla se obtuvieron del **Marco Geoestadístico del INEGI** (entidad 21 = Puebla):
https://www.inegi.org.mx/app/biblioteca/ficha.html?upc=889463770541

El shapefile original viene en el sistema de coordenadas `MEXICO_ITRF_2008_LCC` (proyectado, en metros), por lo que fue reproyectado a `EPSG:4326` (WGS84, grados decimales) para que coincidiera con el sistema de referencia de las coordenadas de los pacientes antes de cualquier operación espacial.

## Metodología

1. **Preparación de datos**: se conservó una copia de referencia del dataset completo (`df_referencia`) y se generó una versión de modelado sin columnas de ubicación directa (`estado`, `municipio`), para evitar que el modelo "aprendiera" el municipio en lugar de inferirlo desde las coordenadas.
2. **Georreferenciación**: las coordenadas de los pacientes se convirtieron en geometrías de punto (`GeoDataFrame`) y se cruzaron mediante una **unión espacial** (`gpd.sjoin`, `predicate="within"`) contra los polígonos municipales, generando la columna `municipio_objetivo` — el municipio real de cada paciente según su ubicación geográfica exacta, y no según el municipio autorreportado.
3. **Análisis exploratorio**: se calculó la distribución de pacientes por municipio, identificando los municipios con mayor y menor concentración, y se generaron visualizaciones de barras.
4. **Visualización geográfica**: se construyeron mapas interactivos con Folium — puntos individuales, heatmap de concentración, capa de polígonos municipales y mapa coroplético por cantidad de pacientes — y se compararon entre sí.
5. **Modelado supervisado**: usando únicamente `latitud` y `longitud` como variables predictoras (`X`) y `municipio_objetivo` codificado numéricamente como variable objetivo (`y`), se dividieron los datos en 80% entrenamiento / 20% prueba (con `stratify`) y se entrenaron tres modelos de clasificación: K-Nearest Neighbors, Random Forest y Regresión Logística Multiclase.
6. **Evaluación**: se calcularon exactitud, precisión, recall y F1-score para cada modelo, se generó la matriz de confusión del mejor modelo y se analizaron los municipios con mayor error de clasificación, relacionándolos con su cercanía geográfica y su cantidad de registros disponibles.
7. **Predicción con nuevos datos**: se probaron los modelos con coordenadas nuevas y se compararon sus predicciones contra la asignación real obtenida por unión espacial.

## Resultados principales

- El dataset grupal contiene **22,000 pacientes**. Tras la unión espacial, **21,238 pacientes (96.5%)** quedaron correctamente asociados a un municipio; el 3.5% restante no pudo asignarse, probablemente por caer cerca de los límites municipales (imprecisión propia de las coordenadas simuladas y del shapefile).
- Los pacientes quedaron distribuidos en **30 municipios** de los 217 que tiene el estado, reflejando que el dataset se concentra en zonas específicas de Puebla y no representa la totalidad del territorio estatal.
- El municipio con mayor concentración es **Puebla** (4,678 pacientes), seguido de Tehuacán, San Martín Texmelucan y Atlixco. La mayoría de los 217 municipios del estado (187) no tienen ningún paciente asignado.
- Comparando los tres modelos de clasificación entrenados:

  | Modelo | Exactitud | Precisión | Recall | F1-score |
  |---|---|---|---|---|
  | KNN | 0.9934 | 0.9936 | 0.9934 | 0.9934 |
  | Random Forest | 0.9941 | 0.9940 | 0.9941 | 0.9939 |
  | Regresión Logística | 0.4018 | 0.1817 | 0.4018 | 0.2432 |

  **Random Forest** obtuvo el mejor desempeño, muy cerca de KNN, mientras que la Regresión Logística tuvo un desempeño notablemente inferior — esperable, ya que al ser un modelo lineal no logra capturar fronteras de decisión irregulares como las que forman los límites geográficos reales entre municipios.

- Dado que los municipios presentes en el dataset están, en su mayoría, bien separados geográficamente entre sí, la confusión entre clases fue mínima: la comparación entre las predicciones del modelo y la asignación real por polígonos mostró una coincidencia del **100%** en la muestra evaluada.
- Se concluye que el modelo supervisado aproxima bien la ubicación de un paciente a partir de solo sus coordenadas, pero la **unión espacial por polígonos oficiales sigue siendo el método más preciso** para determinar la ubicación real, especialmente cerca de los límites municipales o en municipios con pocos registros de entrenamiento.
