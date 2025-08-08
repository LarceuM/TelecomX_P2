# TelecomX_P2
Analisis de los clientes que renuncian (dejan) a TelecomX 
# Predicción de Cancelación de Clientes (Churn Prediction)

Este proyecto tiene como objetivo predecir la evasión (churn) de clientes de una empresa de telecomunicaciones. Basándose en características del cliente, tipo de servicio y comportamiento de pago, se construye un modelo predictivo para ayudar a la empresa a anticiparse a la pérdida de clientes y tomar decisiones estratégicas para su retención. 

---

##  Contenidos

- [Objetivo del proyecto](#objetivo-del-proyecto)
- [Contexto de negocio](#contexto-de-negocio)
- [Dataset](#dataset)
- [Herramientas utilizadas](#herramientas-utilizadas)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Análisis exploratorio](#análisis-exploratorio)
- [Modelado predictivo](#modelado-predictivo)
- [Resultados](#resultados)
- [Cómo ejecutar el proyecto](#cómo-ejecutar-el-proyecto)
- [Recomendaciones y próximos pasos](#recomendaciones-y-próximos-pasos)


---

## Objetivo del proyecto

Identificar a los clientes con mayor probabilidad de abandonar la compañía utilizando técnicas de análisis de datos y modelos de predicción supervisada.
generar una  modelo que pueda ser usando en ambientes productivos  y generar concluciones que ayuden a enfrentar y adelantarse a la posibilidad de abondono de la compañia haciendo recomendaciones de trabajo con las variables mas  relevantes.

---

##  Contexto de negocio

La retención de clientes es clave en las empresas de telecomunicaciones. Este proyecto busca apoyar al área comercial y de atención al cliente con información predictiva que permita implementar estrategias proactivas para reducir la pérdida de clientes.

---

##  Dataset

El dataset, contiene información demográfica, de servicios contratados y comportamiento histórico de clientes, incluyendo si abandonaron o no la compañía.  
, nace desde el archivo "TelecomX_Data.json"   el que es convertido y tratado  su estructura original esta compuesta por 7.267 registros y 21 columnas  las cuales se detalla  acontinuacion:

```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7267 entries, 0 to 7266
Data columns (total 21 columns):
 #   Column                     Non-Null Count  Dtype  
---  ------                     --------------  -----  
 0   customerID                 7267 non-null   object 
 1   Churn                      7267 non-null   object 
 2   customer_gender            7267 non-null   object 
 3   customer_SeniorCitizen     7267 non-null   int64  
 4   customer_Partner           7267 non-null   object 
 5   customer_Dependents        7267 non-null   object 
 6   customer_tenure            7267 non-null   int64  
 7   phone_PhoneService         7267 non-null   object 
 8   phone_MultipleLines        7267 non-null   object 
 9   internet_InternetService   7267 non-null   object 
10   internet_OnlineSecurity    7267 non-null   object 
11   internet_OnlineBackup      7267 non-null   object 
12   internet_DeviceProtection  7267 non-null   object 
13  internet_TechSupport        7267 non-null   object 
14  internet_StreamingTV        7267 non-null   object 
15  internet_StreamingMovies    7267 non-null   object 
16  account_Contract            7267 non-null   object 
17  account_PaperlessBilling    7267 non-null   object 
18  account_PaymentMethod       7267 non-null   object 
19  account_Charges_Monthly     7267 non-null   float64
20  account_Charges_Total       7267 non-null   object 
dtypes: float64(1), int64(2), object(18)
memory usage: 1.2+ MB
```

## Herramientas utilizadas

- Python 3.11+
- Pandas
- NumPy
- Matplotlib / Seaborn
- Scikit-learn,  XGBoost, LightGBM
- SMOTE (balanceo de clases)
- Jupyter Notebook / Google Colab

---

## Estructura del proyecto

```bash
📦 churn-prediction
├── data/                  # Archivos de datos (limpios o crudos)
├── notebooks/             # Jupyter Notebooks
├── src/                   # Código fuente (funciones, módulos)
├── models/                # Modelos entrenados (opcional)
├── README.md
├── requirements.txt       # Librerías necesarias
└── churn_analysis.ipynb   # Notebook principal

```
## Análisis exploratorio

* Preprocesamiento de Datos
Se procede a la carga de los datos desde la planilla Excel generado en el Challange anterior ya que los datos originalmente venian en formato .json
* Borrado de Columnas no relevantes para analisis,  customerID y cuenta_diaria
* Encoding, Transformar las variables categóricas a formato numérico para hacerlas compatibles con los algoritmos de machine learning. Se utilizara el método Onehotencoding 
* Verificación de la Proporción de Cancelación (Churn)
>* Activos 73.4 %
>* Churn 26.6 %

* Normalización o Estandarización
>* 'customer_tenure' Modelo de Normalizacion StandardScaler, Tiene rango amplio (0–72), y afecta distancia/pesos.
>* 'account_Charges_Monthly', Modelo de Normalizacion StandardScaler, Diferencias fuertes entre cargos bajos y altos.
>* 'account_Charges_Total', Modelo de Normalizacion Log y StandardScaler, Escala muy asimétrica y valores extremos

* Correlación y Selección de Variables
>se analizo la correlacion de las variables ademas se grafico la matriz de correlacion y se genero el VIF , con la intencion de determinar las variables mas relevantes.

* Selección de variables relevantes,
>se genera un subconjunto del DataFrame con las variables sugeridas desde el analisis
>* internet_InternetService_Fiber optic
>* account_PaymentMethod_Electronic check
>* account_PaperlessBilling_Yes
>* account_Charges_Monthly_scaled
>* customer_SeniorCitizen
>* account_Contract_Two year
>* customer_tenure_scaled
...

## Modelado predictivo
* Entrenamiento y evaluación de modelos
>* Baseline
>* Regresión Logística
>* KNN
>* Árbol de Decisión
>* Random Forest
>* XGBoost ✅
>* LightGBM

* Balanceo con SMOTE
> Se evaluan todos los modelos con un vbalannce de tipo SMOTE , mejorando el desempeño de algunos modelos se utiliza la Matriz de Confusion y la cuerva RoC
> Importtancia de Variables y  Ajuste de umbral de clasificación
...

## Resultados

Métricas utilizadas: 
* AUC-ROC,
* Recall,
* Precisión,
* F1-Score

##Comparación y selección del Champion Model

##Modelo elegido ( Champion): **XGBoost**

* Mejor balance entre recall y capacidad discriminativa (AUC)

##Importancia de variables:

* Contrato a dos años (Contract_TwoYear)
* Tipo de internet (InternetService_Fiber optic)
* Antigüedad del cliente (customer_tenure)

##Prueba en entorno productivo

Se construye un set de datos sintéticos para simular la aplicación del modelo en producción.

| Modelo           | AUC-ROC | Recall | F1-Score | Observaciones Clave                                    |
| ---------------- | ------- | ------ | -------- | ------------------------------------------------------ |
| **XGBoost**      | 0.834   | 0.846  | Alta     | Mejor balance general. Excelente para detectar churn.  |
| **LightGBM**     | 0.816   | 0.832  | Alta     | Muy competitivo. Más rápido que XGBoost.               |
| **RandomForest** | 0.806   | 0.837  | Alta     | Buen rendimiento, pero menor capacidad discriminativa. |

...
## Cómo ejecutar el proyecto

##Cómo usar este repositorio
###Clona el repositorio:

git clone https://github.com/tu_usuario/TelecomX_P2_Challange.git

###Instala los requerimientos:

  pip install -r requirements.txt

###Abre el notebook en Colab
Ejecuta los notebooks
  conectese a colab , suba el archivo
  suba el data set
  ejecute
...
## Recomendaciones y próximos pasos

Basado en las variables más importantes del modelo Champion (XGBoost):

* Incentivar contratos de largo plazo: Los clientes con contrato de dos años presentan menor propensión a cancelar.
* Evaluar la experiencia de clientes con internet de fibra óptica: Este grupo muestra mayor riesgo de churn.
* Retener a clientes nuevos (<12 meses): Son más propensos a irse. Estrategias de onboarding o beneficios exclusivos pueden ayudar.
* Revisar métodos de pago: Quienes usan Electronic check tienen mayor tasa de churn. Puede implicar menor fidelización.

Análisis exploratorio
Se realizaron análisis visuales y estadísticos para entender las variables más asociadas al abandono de clientes. Entre los hallazgos:

* Los clientes con contratos mensuales tienden a abandonar más.
* Los que no tienen servicios adicionales (como internet o soporte técnico) muestran mayor churn.

Adicionalmente se agrego un dashboard para visualizar los resultados

...

## 👤 Autor

[![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github&logoColor=white)](https://github.com/LarceuM)
[![LinkedIn](https://img.shields.io/badge/-LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/lorenzoarceumorla)

**Lorenzo Arceu Morla**  
Proyecto de análisis predictivo en el contexto de cancelación de servicios en telecomunicaciones.
