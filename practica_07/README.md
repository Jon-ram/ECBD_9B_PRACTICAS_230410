# Práctica 07: Generación de Dataset de Pacientes con Indicadores para Clasificar y Predecir Diabetes

## Descripción

En esta práctica se generó un dataset de **5000 pacientes** del estado de Puebla, con el objetivo de contar con una base de datos que contenga indicadores clínicos, sociodemográficos y de estilo de vida relevantes para la clasificación y predicción de diabetes mediante técnicas de análisis de datos y aprendizaje automático.

El dataset incluye tanto personas sanas como personas con diabetes no diagnosticada, ya que su propósito es servir como conjunto de prueba: a partir de la información contenida en este datasest, se busca poder determinar si un paciente tiene o no diabetes, sin partir de un diagnóstico previo. 

El dataset resultante (`dataset_diabetes_puebla_muestra5000.csv`) contiene 26 columnas que combinan variables demográficas, antecedentes clínicos, mediciones antropométricas, indicadores bioquímicos y hábitos de vida de cada paciente.

## Descripción de las columnas

| Columna | Descripción |
|---|---|
| `id_paciente` | Identificador único del paciente. |
| `estado` | Estado de residencia del paciente. |
| `municipio` | Municipio de residencia del paciente. |
| `zona` | Tipo de zona geográfica de residencia (Urbana o Rural). |
| `edad` | Edad del paciente en años. |
| `genero` | Género del paciente (M = Masculino, F = Femenino). |
| `nivel_socioeconomico` | Nivel socioeconómico del paciente (Bajo, Medio, Alto). |
| `antecedentes_familiares_diabetes` | Indica si el paciente tiene antecedentes familiares de diabetes (1 = sí, 0 = no). |
| `embarazos` | Número de embarazos registrados (aplica a pacientes de género femenino). |
| `imc` | Índice de Masa Corporal del paciente. |
| `circunferencia_cintura_cm` | Circunferencia de cintura del paciente, medida en centímetros. |
| `presion_sistolica` | Presión arterial sistólica, medida en mmHg. |
| `presion_diastolica` | Presión arterial diastólica, medida en mmHg. |
| `trigliceridos_mgdl` | Nivel de triglicéridos en sangre, medido en mg/dL. |
| `hdl_mgdl` | Nivel de colesterol HDL (colesterol "bueno"), medido en mg/dL. |
| `glucosa_ayunas_mgdl` | Nivel de glucosa en sangre en ayunas, medido en mg/dL. |
| `hba1c_pct` | Porcentaje de hemoglobina glucosilada (HbA1c), indicador del control glucémico a largo plazo. |
| `ogtt_2h_mgdl` | Nivel de glucosa en sangre dos horas después de la prueba de tolerancia oral a la glucosa (OGTT), medido en mg/dL. |
| `insulina_serica_uUmL` | Nivel de insulina sérica del paciente, medido en µU/mL. |
| `actividad_fisica_min_semana` | Minutos de actividad física realizados por semana. |
| `fumador` | Indica si el paciente es fumador (1 = sí, 0 = no). |
| `consumo_alcohol` | Frecuencia de consumo de alcohol del paciente (Nunca, Ocasional, Frecuente, etc.). |
| `horas_sueno` | Promedio de horas de sueño diarias del paciente. |
| `indice_calidad_dieta` | Índice que refleja la calidad general de la dieta del paciente. |
| `azucar_diario_g` | Consumo diario de azúcar del paciente, medido en gramos. |
| `frecuencia_ultraprocesados_semana` | Frecuencia semanal de consumo de alimentos ultraprocesados. |

## Objetivo de la práctica

Contar con un dataset representativo y estructurado, sin diagnóstico previo etiquetado, que permita:

- Explorar la relación entre variables clínicas, sociodemográficas y de estilo de vida con un posible cuadro de diabetes.
- Aplicar técnicas de análisis exploratorio de datos (EDA).
- Entrenar, probar y evaluar modelos de clasificación que, a partir de los indicadores del dataset, predigan si un paciente tiene o no diabetes.