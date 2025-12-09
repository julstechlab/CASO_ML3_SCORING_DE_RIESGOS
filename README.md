## 🏦 Scoring de Riesgos — Machine Learning Project

Este proyecto desarrolla un modelo de Machine Learning para evaluación de riesgo crediticio, con el objetivo de estimar la probabilidad de impago de clientes y clasificar su nivel de riesgo para decisiones financieras.

El trabajo abarca desde el análisis exploratorio hasta la creación del pipeline de producción, empleando múltiples modelos para estimar componentes clave del riesgo financiero: PD (Probability of Default), EAD (Exposure at Default) y LGD (Loss Given Default).

---

## 🎯Objetivo del Proyecto

Responder a la pregunta principal:

¿Cómo identificar clientes con alto riesgo crediticio y asignarles un scoring confiable para mejorar decisiones de aprobación?

El modelo permite priorizar préstamos, minimizar pérdidas y apoyar estrategias de mitigación de riesgo.

---

## 📑 Datos Utilizados

- |---------- Dataset / Archivo ----------| ---------- Tipo de Información ----------    | ---------- Descripción ----------|

- prestamos.csv ------>   Información histórica de préstamos y clientes ------> Base principal para modelado


--- 

## 🧩 Metodología

Pipeline aplicado de forma end-to-end:
	
**1. Data Understanding**

Se realizó un análisis del dataset prestamos.csv, identificando la naturaleza de las variables (numéricas, categóricas, comportamiento histórico), su relación con la variable objetivo y las necesidades específicas del negocio crediticio.
Se definieron hipótesis sobre qué factores podrían influir en el riesgo, por ejemplo: monto solicitado, historial previo, atrasos, tasa otorgada, empleo, entre otros.
     
**2. Calidad de Datos**

Se evaluó la calidad de la información detectando valores nulos, inconsistencias, duplicados y datos atípicos.
Se aplicaron estrategias de imputación, eliminación o corrección según su impacto en el modelo.
También se realizaron normalizaciones básicas sobre campos temporales y monetarios.
     
**3. Análisis Exploratorio(EDA)**

En esta fase se exploraron correlaciones, distribuciones, y segmentación de clientes según riesgo.
Se detectaron patrones como características comunes en clientes que incumplieron pagos, variación del riesgo según ingreso, edad, o capacidad de crédito.
Se generaron visualizaciones para interpretar comportamiento y validar hipótesis.

**4. Feature Engineering(Transformación de Datos)**

Se construyeron nuevas variables con potencial predictivo y se transformaron aquellas que requerían preparación antes del modelado.
Acciones aplicadas:
- Encoding de variables categóricas (One-Hot, Label Encoding)
- Escalado de variables numéricas (StandardScaler / MinMaxScaler según el modelo)
- Creación de métricas derivadas (ratio deuda/ingreso, antigüedad crediticia, historial de pagos)
- Normalización de montos y scores

      
**5. Modelización PD - Probabilidad de Default (Clasificación)**

Se entrenaron modelos de clasificación para estimar la Probabilidad de Incumplimiento (PD).
Se compararon distintos algoritmos para evaluar su desempeño:

- Logistic Regression
- Random Forest
- XGBoost / Gradient Boosting

Se evaluaron mediante métricas clave: ROC-AUC, Recall, Precision, F1-Score, priorizando detección de casos de alto riesgo.
  
**6. Modelización EAD & LGD - Severidad del riesgo**

Además del riesgo de ocurrencia, se estimaron componentes financieros del riesgo crediticio:

  1. EAD (Exposure at Default) ------> Regresión ------> Cuánto dinero estaría expuesto ante impago
  2. LGD (Loss Given Default) ------> Regresión ------> Qué porcentaje del crédito se perdería realmente

Se entrenaron modelos de regresión para predecir valores continuos usando enfoques como:
  - Random Forest Regressor
  - XGBoost Regressor
  - Linear Models / Regularización L1-L2

**7. Integración de riesgo - Expected Loss**

Con PD, EAD y LGD estimados, se construyó la métrica final:

Expected Loss = PD × LGD × EAD

Esta métrica permite priorizar otorgamiento de crédito basándose en riesgo-coste esperado y retorno potencial.

**8.Pipeline de producción y reentramiento**

Los pasos anteriores se integraron en un pipeline reproducible usando notebooks y scripts-

Se preparó código para:

- Cargar nuevo dataset y transformar datos automáticamente
- Generar scoring y pérdida esperada por cliente
- Ejecutar reentrenamiento programado (batch o incremental)

--- 

## 🛠️ Herramientas usadas

- Python
- Pandas
- NumPy
- Scikit-Learn
- Matplotlib
- Seaborn
- Jupyter Notebook
