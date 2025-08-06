# Challenge2_Telecom-X_Parte2
# Predicción de Abandono de Clientes (Churn) en TelecomX

## Descripción del Proyecto

Este proyecto tiene como objetivo predecir el abandono de clientes (Churn) en la empresa de telecomunicaciones TelecomX. Se realiza un análisis exploratorio de los datos, se identifican los factores clave que influyen en el abandono y se desarrollan y evalúan diferentes modelos de clasificación para predecir qué clientes son más propensos a irse.

## Dataset

El dataset utilizado es `datos_TelecomXprocesado.csv`, que contiene información sobre los clientes de TelecomX, incluyendo datos demográficos, servicios contratados, información de facturación y si el cliente ha abandonado o no.

**Variables clave:**

*   `Churn`: Variable objetivo (0: No abandona, 1: Abandona)
*   `gender`: Género del cliente
*   `SeniorCitizen`: Indica si el cliente es un ciudadano mayor (0: No, 1: Sí)
*   `Partner`: Indica si el cliente tiene pareja (0: No, 1: Sí)
*   `Dependents`: Indica si el cliente tiene dependientes (0: No, 1: Sí)
*   `tenure`: Antigüedad del cliente en la empresa (en meses)
*   `PhoneService`: Indica si el cliente tiene servicio telefónico (0: No, 1: Sí)
*   `MultipleLines`: Indica si el cliente tiene múltiples líneas telefónicas (0: No, 1: Sí)
*   `InternetService`: Tipo de servicio de internet (DSL, Fiber optic, No)
*   `OnlineSecurity`: Indica si el cliente tiene servicio de seguridad en línea (0: No, 1: Sí)
*   `OnlineBackup`: Indica si el cliente tiene servicio de copia de seguridad en línea (0: No, 1: Sí)
*   `DeviceProtection`: Indica si el cliente tiene servicio de protección de dispositivo (0: No, 1: Sí)
*   `TechSupport`: Indica si el cliente tiene servicio de soporte técnico (0: No, 1: Sí)
*   `StreamingTV`: Indica si el cliente tiene servicio de streaming de TV (0: No, 1: Sí)
*   `StreamingMovies`: Indica si el cliente tiene servicio de streaming de películas (0: No, 1: Sí)
*   `Contract`: Tipo de contrato (Month-to-month, One year, Two year)
*   `PaperlessBilling`: Indica si el cliente tiene facturación electrónica (0: No, 1: Sí)
*   `PaymentMethod`: Método de pago
*   `Charges.Monthly`: Cargo mensual del cliente
*   `Charges.Total`: Cargo total del cliente

## Análisis Exploratorio de Datos (EDA)

Se realizó un análisis exhaustivo para comprender la distribución de la variable objetivo y la relación entre las variables predictoras y el abandono. Los hallazgos clave incluyen:

*   La distribución de Churn muestra un desbalance (aproximadamente 74% No Churn, 26% Churn).
*   El género no parece ser un factor determinante en el abandono.
*   Los ciudadanos mayores y los clientes sin pareja o dependientes muestran una mayor tendencia al abandono.
*   La antigüedad es un factor crucial, con una mayor densidad de abandono en los primeros meses de servicio.
*   El tipo de contrato tiene un impacto significativo, siendo los contratos mes a mes los que presentan mayor tasa de abandono.
*   El servicio de Fibra Óptica y el método de pago "Electronic check" están asociados con un mayor abandono.
*   Los servicios adicionales (seguridad, soporte técnico, etc.) parecen contribuir a la retención de clientes.
*   Los cargos mensuales altos y los cargos totales bajos se relacionan con una mayor probabilidad de abandono.

## Preprocesamiento de Datos

*   Se eliminó la columna `customerID`.
*   Se aplicó One-Hot Encoding a las variables categóricas para convertirlas en un formato numérico adecuado para los modelos.
*   Se normalizaron las variables numéricas utilizando MinMaxScaler para asegurar que estén en una escala similar.

## Modelos de Clasificación

Se entrenaron y evaluaron los siguientes modelos de clasificación para predecir el abandono, utilizando `class_weight='balanced'` para abordar el desbalance de clases y ajustando los hiperparámetros con `GridSearchCV` optimizando el F1-score:

1.  **Decision Tree Classifier:** Se exploraron diferentes profundidades máximas y mínimos de muestras por split.
2.  **Random Forest Classifier:** Se probaron diferentes números de estimadores, profundidades máximas y mínimos de muestras por split.
3.  **Logistic Regression:** Se ajustaron los parámetros de regularización (C y penalty) y el solver.

## Resultados y Evaluación

Los modelos fueron evaluados utilizando métricas como Exactitud, Precisión, Recall y F1-score en un conjunto de validación. Se generaron matrices de confusión para visualizar el rendimiento de cada modelo.

Los resultados del ajuste de hiperparámetros con scoring='f1' mostraron que la **Regresión Logística** obtuvo el mejor F1-score en el conjunto de validación, destacando por su capacidad para identificar correctamente a los clientes que van a abandonar (alto Recall).

## Conclusiones y Recomendaciones

*   Los factores más importantes en la predicción del abandono son la **antigüedad**, el **tipo de contrato**, el **servicio de internet (Fibra Óptica)**, el **método de pago (Electronic check)**, los **cargos** y la presencia de **servicios adicionales de internet**.
*   El balanceo de clases fue crucial para mejorar el Recall de los modelos.
*   La **Regresión Logística** sintonizada con F1-score es el modelo recomendado para este problema, priorizando la identificación de clientes en riesgo.

**Recomendaciones para reducir el Churn:**

*   Implementar programas de **retención temprana** para clientes nuevos.
*   Revisar y mejorar el **rendimiento técnico de la Fibra Óptica**.
*   Fomentar la contratación de **contratos a largo plazo** mediante beneficios y promociones.
*   Promover la utilización de **servicios adicionales** (seguridad, soporte técnico, etc.).
*   Mantener un **seguimiento activo de los clientes**, tanto nuevos como antiguos, para ofrecer promociones y beneficios personalizados.


## Conclusiones
Después de un análisis exhaustivo, preprocesamiento, entrenamiento de modelos y ajuste de hiperparámetros para predecir el abandono de clientes (Churn), podemos sacar las siguientes conclusiones y realizar una limpieza del notebook:

1.  **Factores Determinantes del Abandono:** Los análisis gráficos y las importancias de características de los modelos confirman consistentemente que los factores más influyentes en el abandono de clientes son:
    *   **Antigüedad (tenure):** Clientes con menor tiempo en la empresa son más propensos a abandonar.
    *   **Tipo de Contrato:** Los contratos mes a mes tienen una tasa de abandono significativamente más alta que los contratos a largo plazo (uno o dos años).
    *   **Servicio de Internet:** La Fibra Óptica está asociada con un mayor abandono, mientras que no tener servicio de internet se asocia con menor abandono.
    *   **Método de Pago:** El pago electrónico (Electronic Check) es el método con mayor tasa de abandono.
    *   **Cargos:** Cargos mensuales altos y cargos totales bajos (relacionados con baja antigüedad) son predictores de abandono.
    *   **Servicios Adicionales:** La ausencia de servicios de seguridad y soporte técnico aumenta la probabilidad de abandono.

2.  **Impacto del Balanceo de Clases:** La aplicación de `class_weight='balanced'` fue fundamental para mejorar la capacidad de los modelos (especialmente Árbol de Decisión y Regresión Logística) para identificar correctamente la clase minoritaria (Churn), aumentando significativamente el **Recall**. Sin embargo, esto resultó en una disminución de la Precisión y un aumento de los falsos positivos.

3.  **Resultados del Ajuste de Hiperparámetros (Scoring F1):** Al ajustar los hiperparámetros utilizando el F1-score (una métrica más adecuada para datasets desbalanceados):
    *   La **Regresión Logística** sintonizada (`best_logreg_clf`) obtuvo el **mejor F1-score en el conjunto de validación (0.63)** y un alto **Recall (0.81)** para la clase Churn. Esto la posiciona como la mejor opción si el objetivo principal es identificar a la mayor cantidad posible de clientes que van a abandonar.
    *   El **Random Forest** sintonizado (`best_rf_clf`) también mostró un buen F1-score (0.62) y un recall razonable (0.81). Es una alternativa robusta.
    *   El **Árbol de Decisión** sintonizado (`best_tree_clf`) tuvo un F1-score ligeramente menor (0.61) pero un recall comparable (0.83), manteniendo su ventaja en interpretabilidad.

4.  **Modelo Recomendado:** Considerando el balance entre Precision y Recall para la clase minoritaria reflejado en el F1-score, la **Regresión Logística con `class_weight='balanced'` y sintonizada con scoring='f1'** (`best_logreg_clf`) es el modelo más prometedor para este problema de predicción de abandono, especialmente si se prioriza la identificación de clientes en riesgo.

**Recomendaciones:**
1. Retención temprana: Muchos usuarios dan de baja el servicio los primeros meses. Para contrarrestar esto, se necesita un programa de políticas de beneficios para poder mantenerlos.

2. Fibra óptica: Hay una marcada tendencia de abandono del servicio de los usuarios que contratan este tipo de servicio. Se tiene que revisar y mejorar el rendimiento técnico del mismo.

3. Contratos: Fomentar los contratos a largo plazo, ya que son los que menos abandono tienen, mediante algún sistema de beneficios y promociones.

4. Tipos de servicios: Promover la utilización de los servicios adicionales como el streamingTV o de servicio técnico.

5. Control: Mantener un seguimiento de los clientes nuevos y antiguos para poder evitar que abandonen los servicios mediante promociones y beneficios.

AUTOR: Nicolás Fernando Vales

PLATAFORMA: ALURA LATAM
<img src="https://iili.io/Fizm16J.th.jpg" alt="Fizm16J.th.jpg" border="0" width="100" height="120">

HERRAMIENTAS UTILIZADAS:
GitHub:
<img src="https://github.com/user-attachments/assets/aa8ccf5d-8e6d-44da-b598-821c307d4cca" width="100" height="120">

Google Colab:
<img src="https://github.com/user-attachments/assets/cf43207b-0dc0-438d-90a8-d1b1b9262374" width="100" height="120">

Python:
<img src="https://github.com/user-attachments/assets/a041acd4-4fe1-4906-b091-74f8d20dfb45" width="100" height="120">

