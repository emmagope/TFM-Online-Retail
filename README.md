# Predicción de Recompra en E-commerce (TFM)
Trabajo Fin de Máster: análisis y modelado predictivo de recompra de clientes usando el dataset Online Retail (UCI).
Proyecto orientado a negocio, con dashboards y chatbot para explicar resultados a perfiles no técnicos.

🎯 Objetivo

Construir un flujo reproducible que permita:

Limpiar y explorar datos transaccionales (EDA).

Generar features de cliente (RFM extendido, ratios, tendencias).

Entrenar y evaluar modelos para predecir recompra a 30 días.

Explicar y operacionalizar el modelo mediante dashboards y un chatbot.

📦 Requisitos

Python ≥ 3.10

Recomendado: entorno virtual con venv o conda

# con venv
python -m venv .venv
source .venv/bin/activate   # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt


Sugerencia de contenidos de requirements.txt:
pandas numpy scikit-learn matplotlib plotly seaborn jupyter ipywidgets tqdm
(añade paquetes específicos si tu notebook los usa)

🗂️ Estructura sugerida del repositorio
TFM-Online-Retail/
├── data/
│   └── Online Retail.xlsx              # (no se versiona si es privado)
├── notebooks/
│   └── TFM_online_retail.ipynb         # notebook principal
├── imgs/                               # capturas para README
│   ├── dashboard1_a.png                # (equivalentes a captura28–31)
│   ├── dashboard2.png                  # (equivalente a captura32)
│   ├── chatbot.png                     # (equivalente a captura33)
│   ├── roc_test.png                    # (equivalente a captura23)
│   └── pr_test.png                     # (equivalente a captura24)
├── src/                                # (opcional) funciones auxiliares
│   ├── features.py
│   └── modeling.py
├── requirements.txt
├── .gitignore
└── README.md


.gitignore recomendado:

__pycache__/
.ipynb_checkpoints/
.DS_Store
.env/
.venv/
data/*.csv
data/*.xlsx

🚀 Cómo reproducir

Clonar el repo y crear el entorno (ver Requisitos).

Colocar el dataset Online Retail.xlsx en data/.

Fuente: UCI Machine Learning Repository (ver Bibliografía).

Abrir el notebook:

jupyter notebook notebooks/TFM_online_retail.ipynb


Ejecutar secuencialmente:

Carga y limpieza

EDA

Feature engineering (RFM extendido, ratios, deltas, log1p)

Modelado (baseline + Random Forest + tuning)

Predicción en test y evaluación

Dashboards + Chatbot (en el propio notebook)

🔬 Metodología (resumen)

EDA: calidad de datos, outliers, distribución logarítmica, temporalidad (mes/semana/hora), concentración por país/producto.

Features: Recency, Frequency, Monetary (30/60/90d), variedad, ticket medio, ratios y deltas; variables temporales.

Target: recompra ≤ 30 días (binaria).

Split temporal: Train (≤ Jun 2011), Valid (Jun–Sep 2011), Test (≥ Sep 2011).

Modelos: Regresión Logística (baseline), Random Forest (tuning), pruebas con GB/SMOTE/KBest.

Selección final: Random Forest por equilibrio rendimiento–estabilidad–explicabilidad.

Umbral operativo: ~0.4803 (índice de Youden, validación).

Explicabilidad: importancia de variables, dashboards y chatbot.

📈 Resultados clave

Test:

Accuracy ≈ 0.72

ROC-AUC ≈ 0.75

PR-AUC ≈ 0.70

F1 ≈ 0.63 (umbral ~0.48)

Concentración por deciles (priorización de campañas):

Top 10% → 22% de recompras

Top 20% → 38%

Top 30% → 53%

Interpretación para negocio: el modelo prioriza correctamente los clientes con mayor probabilidad de recompra, permitiendo actuar primero sobre los segmentos de mayor retorno esperado.

🧭 Dashboards y Chatbot

Dashboard 1 – Dataset (KPIs, series temporales, top productos, RFM, geografía)


Dashboard 2 – Modelo (matriz de confusión por umbral, ROC/PR, gains & lift)


Chatbot explicativo (consultas en lenguaje natural dentro del notebook)


🔁 Reutilización en otras empresas

El flujo está diseñado para ser replicable en un único notebook:

Cambiar fuente de datos (mismo esquema transaccional: fecha, cliente, producto, cantidad, precio, país).

Ajustar ventanas temporales y definiciones de target según negocio.

Reentrenar y validar con split temporal.

Usar dashboards + chatbot para comunicar resultados a negocio.

Siguiente paso natural: empaquetar como pipeline (sklearn + joblib) y servir dashboards en Streamlit/Dash.

⚠️ Limitaciones

Dataset de un único negocio (2010–2011).

Ventanas fijas (30/60/90d) — podrían optimizarse por sector.

Costes de FP/FN no modelados explícitamente (añadir función de coste).

No se incluyeron modelos GBDT tipo LightGBM/CatBoost en la versión final.

📚 Bibliografía

Dua, D. & Graff, C. (2019). UCI Machine Learning Repository: Online Retail Dataset. University of California, ICS. https://archive.ics.uci.edu/dataset/352/online+retail

Reinartz, W., & Kumar, V. (2002). The mismanagement of customer loyalty. Harvard Business Review.

Fader, P. S., & Hardie, B. G. (2009). Probability models for customer-base analysis. Journal of Interactive Marketing, 23(1), 61–69.

Gupta, S., & Lehmann, D. R. (2003). Customers as assets. Journal of Interactive Marketing, 17(1), 9–24.

Hosseini, S. M., Maleki, A., & Gholamian, M. R. (2010). Cluster analysis… Expert Systems with Applications, 37(7), 5259–5264.

Kotler, P., & Keller, K. L. (2016). Marketing Management. Pearson.

Cantú, D., & González, J. (2016). Análisis de RFM… Revista de Métodos Cuantitativos para la Economía y la Empresa.

UNCTAD (2021). Estadísticas de comercio electrónico global.

