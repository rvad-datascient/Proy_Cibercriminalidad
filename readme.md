
# 🛡️ Cibercrimen en España: Predicción y Modelado (2022–2025)

## 💡 Objetivo del Proyecto
Desarrollar un ecosistema predictivo capaz de estimar la evolución de la cibercriminalidad en España a nivel provincial. Utilizando datos oficiales del **Sistema Estadístico de Criminalidad (SEC)** y variables demográficas del **INE**, el proyecto transforma registros históricos en inteligencia accionable para anticipar tendencias delictivas con alta precisión.

---

## 🚀 App Interactiva (Dashboard de Control)
Como capa final del proyecto, se ha desarrollado una **interfaz interactiva en Streamlit** que permite visualizar las predicciones de 2025 de forma dinámica.

*   **Mapa de Calor Provincial:** Visualización de la tasa de riesgo por cada 1.000 habitantes.
*   **Semáforo de Riesgo:** Indicador inteligente que clasifica la peligrosidad (Baja/Media/Alta) según la provincia seleccionada.
*   **Análisis de Tipologías (Radar):** Desglose visual de los 8 grupos delictivos mediante gráficos radiales.
*   **Glosario Integrado:** Consulta rápida de las tipologías legales incluidas en cada clúster.

> **Acceso a la App:** `streamlit run app.py` *(https://proycibercriminalidad.streamlit.app/)*

---

## 📊 Validación Real (Hito 2025)
El modelo ha sido validado contrastando las predicciones generadas con los datos reales publicados por el Ministerio del Interior para el cierre de 2025, demostrando una robustez excepcional:

*   **WAPE (Error Ponderado):** 5.72%
*   **Desviación Real vs. Predicción:** < 3% en volumen total.

| Indicador | Dato Oficial SEC | Predicción Modelo | Desviación |
| :--- | :--- | :--- | :--- |
| **Total Cibercrimen** | 489.248 | 500.117 | **+2.2%** |
| **Fraude Informático** | 430.493 | 446.555 | **+3.7%** |
| **Otros Ciberdelitos** | 58.755 | 53.562 | **-8.8%** |

---

## 🧠 Estructura de Trabajo
El proyecto se articula en cuatro fases modulares en formato Notebook:

1.  **`01_Introducción`**: Contexto legal y fuentes de datos (SEC e INE).
2.  **`02_EDA_Limpieza`**: Gestión de nulos, duplicados y normalización de nombres provinciales.
3.  **`03_EDA_Visual`**: Framework de métricas (Tasa x 1000, Peso del Delito y VAR%). Identificación de outliers.
4.  **`04_ML_Modelado`**: Ingeniería de variables (Lags, Medias Móviles), entrenamiento (Random Forest/XGBoost) y generación del CSV final de predicciones.

---

## 🧩 Agrupación Estratégica (Clustering)
Para mitigar la granularidad excesiva y mejorar la potencia del modelo, se definieron **8 grupos estratégicos**:

| Grupo Penal | Delitos Incluidos (Resumen) |
| :--- | :--- |
| **Fraude Informático** | Estafas bancarias, tarjetas, criptoactivos e inversiones. |
| **Interferencia** | Sabotaje informático y ataques a sistemas/datos. |
| **Amenazas/Coacciones** | Extorsión, acoso digital y amenazas en red. |
| **Delitos Sexuales** | Sexting, grooming y pornografía de menores. |
| **Falsificación** | Usurpación de identidad y falsificación documental. |
| **Contra el Honor** | Injurias, calumnias y hostigamiento (cyber-bullying). |
| **Acceso Ilícito** | Revelación de secretos e interceptación de datos. |
| **Propiedad Industrial** | Espionaje industrial y piratería intelectual. |

---

## ⚙️ Especificaciones Técnicas
*   **Modelado Segmentado:** 
    *   `Random Forest` para Fraude Informático (patrones estables).
    *   `XGBoost` para Otros Delitos (captura mejor la volatilidad).
*   **Feature Engineering:** Creación de rezagos temporales (Lags T-1, T-2) para captar la inercia delictiva.
*   **Tratamiento de Datos:** `RobustScaler` para manejar la disparidad de volumen entre grandes metrópolis (Madrid/Barcelona) y zonas rurales.

---


## 👩‍💻 Sobre mí (y este proyecto)

**👋 ¡¡Hola! Soy Raquel, Data Analyst – Business & Financial Analytics – Data Science**

Me encanta pillar un montón de datos desordenados y convertirlos en decisiones que sirvan para algo. Este dashboard es mi **Proyecto de Fin de Máster en Data Science & Machine Learning** y es mi forma de demostrar cómo la IA puede ayudarnos a entender (y predecir) algo tan complejo como el cibercrimen.

*   **El truco:** He usado datos oficiales del Ministerio del Interior para que lo que veas aquí sea lo más cercano posible a la realidad.
*   **Hablamos en:** [LinkedIn](www.linkedin.com/in/raquelvadillo)

---

## ⚠️ ¡Un segundo! (Advertencia)

Esto es un proyecto **educativo y técnico**. Aunque el modelo es potente y los datos son reales, las predicciones son estimaciones. El cibercrimen cambia por mil cosas (política, nuevas leyes, o que a un hacker le dé por algo nuevo mañana), así que usa esto para flipar con los datos, no para planificar una operación policial real. 🕵️‍♀️

---
