# **Predicción y Modelado de Denuncias por Cibercriminalidad en España (2022–2025)**

## **Objetivo del Proyecto**

Desarrollar un ecosistema predictivo capaz de estimar la **evolución** de las **denuncias por cibercriminalidad en España** a nivel provincial. Utilizando datos oficiales del **Sistema Estadístico de Criminalidad (SEC)** y variables demográficas del **INE**, el proyecto transforma registros históricos en inteligencia accionable para anticipar tendencias delictivas con alta precisión.

---

## **App Interactiva (Dashboard de Control)**

Como capa final del proyecto, se ha desarrollado una **interfaz interactiva en Streamlit** que organiza el análisis en cuatro bloques:

- **Introducción y validación:** Contexto del SEC, definición de métricas y validación del modelo 2025 frente al Balance de Criminalidad oficial.
- **Evolución Nacional (2022–2025):** Series temporales del total de denuncias por cibercrimen, fraude informático y otros ciberdelitos, comparando datos reales (2022–2024) con la predicción para 2025.
- **Fraude Informático (Análisis 2025):** Mapas de peso del fraude, ranking de provincias por tasa, variación interanual (VAR%) y evolución provincial con predicción 2025.
- **Otros Ciberdelitos (Análisis 2025):** Mapas de tasa total de “Otros ciberdelitos”, mapa de crecimiento (Δ Tasa 2025 vs 2024), rankings de incidencia y crecimiento, evolución provincial y desglose de tipologías por provincia.

> **Ejecución:**  
> `streamlit run 05_App/app_cibercrimen.py`

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

---

## **Resumen de Resultados**

- **Precisión Robusta:** R² de 0.97 en *Otros Ciberdelitos*.  
- **Ajuste Global:** Desviación agregada del **2,97 %**.  
- **Fidelidad:** La predicción 2025 mantiene la estructura delictiva real reportada por el Ministerio del Interior.

---

## **Nota técnica**

Las predicciones corresponden exclusivamente al **ámbito nacional provincial**, excluyendo las infracciones cometidas **en el extranjero**, ya que el dataset original tampoco las incluye.

La comparación debe realizarse únicamente con el bloque **“Cibercriminalidad (infracciones penales cometidas por medio ciber)”** del ámbito nacional.

---

## **Estructura de Trabajo**

### **01 · Análisis Exploratorio de Datos (EDA)**

- Limpieza, normalización y validación técnica.  
- Visualización avanzada: mapas, tendencias y distribución por tipologías.

### **02 · Modelado Predictivo**

- Entrenamiento de modelos RandomForest y XGBoost.  
- Evaluación con MAE, WAPE y R².  
- Predicción de denuncias 2025.

---

## **Mapas Interactivos (Análisis Espacial)**

Debido a las limitaciones de GitHub, los mapas pueden visualizarse mediante:

- **nbviewer:**  
    https://nbviewer.jupyter.org/https://github.com/rvad-datascient/Proy_Cibercriminalidad.git/tree/main/02_Notebooks/
  
- **Archivos HTML locales:**  
  Carpeta `02_Notebooks/mapas_interactivos/`

---

## **Agrupación Estratégica (Clustering)**

Basada en la clasificación oficial del Ministerio del Interior (SEC).

| Grupo penal | Delitos incluidos |
| --- | --- |
| fraude_informatico | Estafas, estafas bancarias, tarjetas, inversores. |
| interferencia_en_los_datos_y_en_el_sistema | Ataques a sistemas, sabotaje digital. |
| amenazas_y_coacciones | Amenazas, extorsión, acoso. |
| delitos_sexuales | Grooming, sextorsión, pornografía de menores. |
| falsificacion_informatica | Usurpación de identidad, falsificación documental. |
| contra_el_honor | Injurias, calumnias, perfiles falsos. |
| acceso_e_interceptacion_ilicita | Intrusismo, acceso ilegal, revelación de secretos. |
| contra_la_propiedad_industrial_intelectual | Piratería, espionaje industrial. |

---

## **Especificaciones Técnicas**

| Componente | Implementación |
| --- | --- |
| Modelado | RandomForest (Fraude) · XGBoost (Otros) |
| Feature Engineering | Lags T-1/T-2, Media móvil, VAR_pct, Δ Tasa |
| Preprocesamiento | RobustScaler, OneHotEncoder |
| Validación Temporal | Train 2023 · Test 2024 |
| Optimización | Optuna, GridSearchCV |
| Explicabilidad | SHAP |
| Despliegue | Pipelines `.joblib` |

---

## **Estructura del Proyecto**

```text
Proy_Cibercriminalidad/
├── 01_Data/
│   ├── Process/
│   └── Predictions/
├── 02_Notebooks/
│   ├── mapas_interactivos/
│   ├── 01_EDA.ipynb
│   └── 02_Feature_ML.ipynb
├── 03_SRC/
├── 04_Models/
├── 05_App/
│   └── app_cibercrimen.py
├── 06_Test/
├── requirements.txt
└── README.md
```
---

# **Instrucciones: Clonar y Ejecutar**
- git clone https://github.com/rvad-datascient/Proy_Cibercriminalidad.git
- cd Proy_Cibercriminalidad
- pip install -r requirements.txt
- streamlit run 05_App/app_cibercrimen.py

---

## **Sobre mí**

**¡Hola! Soy Raquel, Data Analyst – Data Science**

Me encanta convertir datos complejos en decisiones estratégicas. Este dashboard es mi **Proyecto de Fin de Máster en Data Science & Machine Learning** y refleja mi capacidad para integrar análisis estadístico, *Machine Learning* y desarrollo de aplicaciones.

* **LinkedIn:** [Raquel Vadillo](https://www.google.com/search?q=https://www.linkedin.com/in/raquelvadillo)

---

## **Aviso Legal**

Este es un proyecto educativo y técnico. Las predicciones son estimaciones estadísticas basadas en datos históricos. No deben utilizarse como base para la planificación de operaciones policiales o decisiones de seguridad crítica.