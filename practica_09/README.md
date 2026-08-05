# Práctica 09: Calcular el Riesgo de Infarto en Pacientes de Xicotepec (Análisis Supervisado)

## Objetivo

Desarrollar un modelo de aprendizaje supervisado capaz de estimar el nivel de riesgo de infarto en pacientes del municipio de Xicotepec, utilizando variables clínicas, demográficas y hábitos de vida. Además, integrar análisis geoespacial para identificar zonas prioritarias de atención médica.

---

## Dataset

El conjunto de datos contiene información simulada de pacientes del municipio de Xicotepec, incluyendo variables como:

- Edad
- Género
- Índice de Masa Corporal (IMC)
- Presión arterial
- Glucosa en ayunas
- Hemoglobina glucosilada (HbA1c)
- Triglicéridos
- HDL
- Insulina sérica
- Actividad física
- Consumo de alcohol
- Tabaquismo
- Coordenadas geográficas (latitud y longitud)

---

## Herramientas utilizadas

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Folium

---

## Modelos implementados

- Regresión Logística
- Random Forest
- K-Nearest Neighbors (KNN)

---

## Métricas evaluadas

- Accuracy
- Precision
- Recall
- F1-Score
- Matriz de confusión

---

## Resultados

Se comparó el desempeño de los modelos implementados y se seleccionó el algoritmo con mejor capacidad predictiva para estimar el riesgo de infarto.

Posteriormente se realizó un análisis geográfico mediante mapas interactivos y mapas de calor para identificar zonas con mayor concentración de pacientes con riesgo elevado.

---

## Estructura del proyecto

```
Proyecto/

│
├── data/
│   ├── raw/
│   └── processed/
│
├── README.md
│
└── Practica09.ipynb
```

---

## Conclusiones

El uso de modelos de aprendizaje supervisado permitió estimar el riesgo de infarto a partir de variables clínicas y demográficas.

La incorporación de análisis geoespacial facilitó la identificación de zonas prioritarias de atención y la propuesta de ubicaciones para unidades médicas de respuesta rápida.

Los resultados tienen fines académicos y fueron obtenidos a partir de un conjunto de datos simulado.