# 📊 Bank Marketing — Análisis y Predicción de Depósitos a Plazo

> Análisis exploratorio y modelo de clasificación para predecir si un cliente bancario aceptará una oferta de depósito a plazo, a partir de datos de campañas de marketing telefónico de una entidad portuguesa.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)
![Status](https://img.shields.io/badge/Status-En%20progreso-yellow)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📋 Tabla de Contenidos

- [Descripción](#descripción)
- [Datos](#datos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Metodología](#metodología)
- [Resultados](#resultados)
- [Conclusiones](#conclusiones)
- [Próximos pasos](#próximos-pasos)

---

## 📌 Descripción

Este proyecto analiza datos de una campaña de marketing telefónico de un banco portugués. El objetivo es predecir si un cliente suscribirá un **depósito a plazo** (`y = yes/no`), en base a su perfil socioeconómico y el contexto de la campaña.

- **Objetivo**: Clasificar clientes según su probabilidad de aceptar el producto financiero
- **Motivación**: Optimizar la estrategia de contacto y aumentar la tasa de conversión de la campaña
- **Alcance**: EDA, limpieza de datos, análisis de atributos predictivos y evaluación de modelo de clasificación binaria


---

## 📦 Datos

| Campo        | Detalle                                                                 |
|--------------|-------------------------------------------------------------------------|
| **Fuente**   | [Kaggle — Bank Marketing Dataset](https://www.kaggle.com/datasets/henriqueyamahata/bank-marketing) |
| **Origen**   | UCI Machine Learning Repository                                         |
| **Formato**  | CSV (separador `;`)                                                     |
| **Volumen**  | 39.855 observaciones × 21 variables (post-limpieza)                    |
| **Target**   | `y` — si el cliente suscribió el depósito a plazo (`yes` / `no`)       |

### Variables principales

| Variable | Tipo | Descripción |
|----------|------|-------------|
| `age` | Numérica | Edad del cliente |
| `job` | Categórica | Ocupación laboral |
| `marital` | Categórica | Estado civil |
| `education` | Categórica | Nivel educativo |
| `default` | Categórica | ¿Tiene crédito en mora? |
| `housing` | Categórica | ¿Tiene préstamo hipotecario? |
| `loan` | Categórica | ¿Tiene préstamo personal? |
| `contact` | Categórica | Tipo de contacto (celular / teléfono) |
| `month` | Categórica | Mes del último contacto |
| `day_of_week` | Categórica | Día de la semana del contacto |
| `duration` | Numérica | Duración de la última llamada (segundos) |
| `campaign` | Numérica | Número de contactos en esta campaña |
| `poutcome` | Categórica | Resultado de campaña anterior |
| `euribor3m` | Numérica | Tasa Euribor a 3 meses |
| `nr.employed` | Numérica | Número de empleados (indicador macro) |
| `y` | Binaria | **Target**: suscribió depósito (`yes`/`no`) |

---

## ⚙️ Instalación

### Requisitos previos

- Python 3.x
- pip

### Pasos

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/bank-marketing.git
cd bank-marketing

# 2. Crear entorno virtual
python -m venv venv
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows

# 3. Instalar dependencias
pip install -r requirements.txt
```

### Dependencias principales

```txt
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
```

---

## 🚀 Uso

```bash
# Iniciar Jupyter Notebook
jupyter notebook notebooks/Analiysis.ipynb
```

> ⚠️ Asegurate de que el archivo `bank-additional-full.csv` esté ubicado en `data/` antes de ejecutar el notebook.

---

## 🔬 Metodología

### 1. Exploración de Datos (EDA)
Análisis inicial del dataset: tipos de variables, distribuciones y descripción estadística. Se identificaron 21 variables (categóricas, numéricas continuas y macroeconómicas) y el target binario `y`.

### 2. Limpieza y Preprocesamiento
Los valores faltantes estaban codificados como `"unknown"`. Se aplicó el siguiente criterio:

- **Eliminación de filas**: variables `job`, `housing` y `education` (categoría `illiterate`) por su volumen significativo de unknowns.
- **Imputación por moda**: variables `marital` y `loan`, dado que la cantidad de unknowns era pequeña y las variables están muy desbalanceadas.

Resultado final: **39.855 filas × 21 columnas**.

### 3. Análisis de Atributos Predictivos
Se evaluaron dos variables con mayor poder predictivo sobre el target:

- **`job` (ocupación)**: Ciertas ocupaciones como estudiantes y jubilados presentan una proporción notablemente mayor de respuestas `yes`.
- **`age` (edad)**: Los clientes jóvenes (~20 años) y adultos mayores (>60 años) muestran mayor probabilidad de aceptar el producto, aunque con menor volumen de datos en los extremos.

### 4. Modelado *(en desarrollo)*
Problema de **clasificación binaria** con datos desbalanceados (predominancia de `no`). Métricas de evaluación previstas:

| Métrica | Descripción |
|---------|-------------|
| Accuracy | Proporción total de aciertos |
| Precision | % de predicciones `yes` correctas |
| Recall | % de `yes` reales correctamente identificados |
| F1-Score | Balance entre precision y recall |
| ROC-AUC | Capacidad de separación entre clases |

---

## 📈 Resultados

- 🔍 **Ocupación**: Estudiantes y jubilados presentan la mayor proporción de suscripciones (`yes`), posiblemente correlacionado con el rango etario.
- 📊 **Edad**: Los extremos etarios muestran mayor tasa de conversión, aunque con menor volumen de datos — lo que puede distorsionar la interpretación.
- ⚠️ **Dataset desbalanceado**: La variable target tiene predominancia de `no`, lo que requiere métricas más allá del accuracy para evaluar correctamente el modelo.

---

## 💡 Conclusiones

El perfil socioeconómico del cliente —especialmente la ocupación y la edad— tiene influencia en la decisión de suscribir un depósito a plazo. La distribución desbalanceada del target exige un enfoque cuidadoso en la evaluación del modelo. Las variables macroeconómicas (`euribor3m`, `nr.employed`) también podrían aportar valor predictivo relevante en etapas posteriores.

---

## 🔮 Próximos pasos

- [ ] Analizar variables macroeconómicas como atributos predictivos
- [ ] Aplicar técnicas de balanceo de clases (SMOTE, undersampling)
- [ ] Entrenar modelos de clasificación (Logistic Regression, Random Forest, XGBoost)
- [ ] Comparar modelos con métricas de Precision, Recall, F1 y ROC-AUC
- [ ] Exportar visualizaciones al informe final

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT**.

---

*Proyecto académico desarrollado para la materia de Introducción de Aprendizaje Automatico.*
