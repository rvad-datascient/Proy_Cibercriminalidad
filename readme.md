# **Predicción y Modelado de Denuncias por Cibercriminalidad en España (2022–2025)**

**Objetivo del Proyecto**

Desarrollar un ecosistema predictivo capaz de estimar la **evolución** de las **denuncias por cibercriminalidad en España** a nivel provincial. Utilizando datos oficiales del **Sistema Estadístico de Criminalidad (SEC)** y variables demográficas del **INE**, el proyecto transforma registros históricos en inteligencia accionable para anticipar tendencias delictivas con alta precisión.

---

## **App Interactiva (Dashboard de Control)**

Como capa final del proyecto, se ha desarrollado una **interfaz interactiva en Streamlit** que organiza el análisis en cuatro bloques:

- **Introducción y validación:** Contexto del SEC, definición de métricas y validación del modelo 2025 frente al Balance de Criminalidad oficial.
- **Evolución Nacional (2022–2025):** Series temporales del total de denuncias por cibercrimen, fraude informático y otros ciberdelitos, comparando datos reales (2022–2024) con la predicción para 2025.
- **Fraude Informático (Análisis 2025):** Mapas de peso del fraude, ranking de provincias por tasa, variación interanual (VAR%) y evolución provincial con predicción 2025.
- **Otros Ciberdelitos (Análisis 2025):** Mapas de tasa total de “Otros ciberdelitos”, mapa de crecimiento (Δ Tasa 2025 vs 2024), rankings de incidencia y crecimiento, evolución provincial y desglose de tipologías por provincia.

> **Ejecución:**  
> [`streamlit run 05_App/app_cibercrimen.py`](https://proycibercriminalidad.streamlit.app/)

---

# **Validación Real (Hito 2025)**

El modelo se ha validado frente a los datos oficiales del Ministerio del Interior (Balance de Criminalidad 2025). La desviación total es inferior al **3 %**, con un ajuste superior al **96 %** en ambas tipologías principales.

## **Validación del modelo frente al Balance de Criminalidad 2025 (SEC)**

| Indicador | Dato Oficial SEC | Predicción Modelo | Desviación |
| --- | --- | --- | --- |
| Total Cibercrimen | 489.248 | 503.812 | +2,97 % |
| Fraude Informático | 430.493 | 447.118 | +3,86 % |
| Otros Ciberdelitos | 58.755 | 56.694 | -3,50 % |

## **Rendimiento de los modelos**

| Dataset | Modelo | MAE | WAPE (%) | R² |
| --- | --- | --- | --- | --- |
| FRAUDE | RandomForest | 0.4663 | 5.76 % | 0.8552 |
| OTROS | XGBoost | 0.0132 | 8.16 % | 0.9778 |

* **MAE (Mean Absolute Error)**: Error medio en miles de denuncias.
* **WAPE (Weighted Average Percentage Error)**: Precisión relativa ponderada.
* **R²**: Coeficiente de determinación (capacidad explicativa del modelo).

## **Resumen de Resultados**

> * **Precisión Robusta:** El modelo alcanza un R² de 0.97 en *Otros Ciberdelitos*, garantizando una alta fiabilidad en las proyecciones.
> * **Ajuste Global:** La desviación agregada de apenas un **2,97 %** valida el enfoque de entrenamiento basado en Random Forest y XGBoost.
> * **Fidelidad:** La proyección 2025 confirma que el modelo no solo predice el volumen, sino que mantiene la estructura delictiva real reportada por el Ministerio del Interior.
> *Nota: Este proceso de validación forma parte del pipeline automatizado definido en `03_SRC/evaluation_utils.py`, asegurando que la comparación contra datos oficiales sea replicable y auditable.*
>
>

---

## **Nota técnica**

Las predicciones generadas por el modelo corresponden exclusivamente al **ámbito nacional provincial**; es decir, **no incluyen** las infracciones cometidas **en el extranjero**, ya que el dataset original utilizado para entrenar el modelo tampoco las incorpora.

Por este motivo, la comparación debe realizarse únicamente con el bloque **“Cibercriminalidad (infracciones penales cometidas por medio ciber)”** del ámbito nacional, excluyendo el apartado **“En el extranjero”** (pág. 507 del informe oficial).

*Informe oficial:* [Balance de Criminalidad – Cuarto Trimestre 2025](https://estadisticasdecriminalidad.ses.mir.es/publico/portalestadistico/dam/jcr:7d3776cd-9ca4-4c02-8ca4-96b2571dbee4/Balance%20de%20Criminalidad%20Cuarto%20Trimestre%202025.pdf)

---

## **Estructura de Trabajo**

El proyecto se articula en dos fases modulares:

**01_Análisis Exploratorio de Datos (EDA)**:

* Definición del problema, marco teórico y objetivos del modelo.
* Ingesta de fuentes crudas, tratamiento de nulos, normalización de provincias y validación técnica.
* Visualización avanzada: Mapas de calor, tendencias temporales y distribución por tipologías.

**02_Modelado_Predictivo (Predictive Modeling)**:

* Entrenamiento de algoritmos y evaluación de métricas.
* Proyecciones de denuncias por cibercriminalidad 2025.

---

## **Agrupación Estratégica (Clustering)**

Para mitigar la granularidad excesiva y mejorar la potencia del modelo, se inspeccionaron los hechos basados en los bloques definidos por el Ministerio del Interior.

> **Referencia Metodológica:** [Metodología de Cibercriminalidad (SEC)](https://estadisticasdecriminalidad.ses.mir.es/publico/portalestadistico/dam/jcr:d96d4063-98d8-4647-8c76-d46a331a4ba3/03_Metodolog%C3%ADa_Cibercriminalidad.pdf).

| Grupo penal | Delitos incluidos según SEC |
| --- | --- |
| **fraude_informatico** | Estafas, estafas bancarias, tarjetas, inversores. |
| **interferencia_en_los_datos_y_en_el_sistema** | Ataques a sistemas, sabotaje digital, datos o programas. |
| **amenazas_y_coacciones** | Amenazas, extorsión, coacciones, acoso. |
| **delitos_sexuales** | Sexting, grooming, pornografía de menores, agresión/abuso sexual. |
| **falsificacion_informatica** | Usurpación de identidad, falsificación de documentos/moneda/DNI. |
| **contra_el_honor** | Injurias, calumnias, perfiles falsos, difusión ilícita de contenidos. |
| **acceso_e_interceptacion_ilicita** | Acceso ilegal a sistemas, revelación de secretos, intrusismo. |
| **contra_la_propiedad_industrial_intelectual** | Delitos contra propiedad industrial/intelectual, espionaje industrial. |

---

## **Especificaciones Técnicas**

| Componente | Implementación |
| --- | --- |
| Modelado | RandomForest (Fraude) · XGBoost (Otros) |
| Feature Engineering | Lags T-1/T-2, Media móvil, VAR_pct |
| Preprocesamiento | RobustScaler, OneHotEncoder, Pipelines sin leakage |
| Validación Temporal | Train 2023, Test 2024, TimeSeriesSplit |
| Optimización | Optuna, GridSearchCV |
| Explicabilidad | SHAP (Top variables por tipología) |
| Despliegue | Pipelines finales guardados con joblib |

---

```text
Proy_Cibercriminalidad/
├── 01_Data/
│   ├── Process/            # Datos limpios y GeoJSON
│   └── Predictions/        # Salidas del modelo (2025)
├── 02_Notebooks/
│   ├── mapas_interactivos/ # Visualizaciones HTML
│   ├── 01_EDA.ipynb
│   └── 02_Feature_ML.ipynb
├── 03_SRC/                 # Scripts modulares (DRY)
├── 04_Models/              # Pipelines guardados (.joblib)
├── 05_App/
│   └── app_cibercrimen.py  # Código del Dashboard
├── 06_Test/                # Tests unitarios
├── requirements.txt        # Dependencias
└── README.md

```
---

# **Instrucciones: Clonar y Ejecutar**
- git clone https://github.com/rvad-datascient/Proy_Cibercriminalidad.git
- cd Proy_Cibercriminalidad
- pip install -r requirements.txt
- streamlit run 05_App/app_cibercrimen.py

---

## Sobre mí

**¡Hola! Soy Raquel, Data Analyst – Data Science**

Me encanta convertir datos complejos en decisiones estratégicas. Este dashboard es mi **Proyecto de Fin de Máster en Data Science & Machine Learning** y refleja mi capacidad para integrar análisis estadístico, *Machine Learning* y desarrollo de aplicaciones.

* **LinkedIn:** [Raquel Vadillo](https://www.google.com/search?q=https://www.linkedin.com/in/raquelvadillo)

---

## **Aviso Legal**

Este es un proyecto educativo y técnico. Las predicciones son estimaciones estadísticas basadas en datos históricos. No deben utilizarse como base para la planificación de operaciones policiales o decisiones de seguridad crítica.
