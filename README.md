# Predicción del Customer Lifetime Value (CLTV) a 6 meses

El Customer Lifetime Value (CLTV) es una métrica fundamental para los negocios de comercio electrónico, ya que permite estimar el valor económico futuro que un cliente generará para la empresa. Contar con estimaciones confiables de CLTV facilita la priorización de clientes, la asignación eficiente del presupuesto de marketing y la definición de estrategias de retención.

En este proyecto se aborda el problema de estimar el CLTV de los clientes en un horizonte de 6 meses, utilizando su historial transaccional y comportamiento de compra.

## 2. Pregunta a resolver

**Dado el historial y comportamiento del cliente, ¿cuál será su CLTV en los próximos 6 meses?**

## 3. Objetivos del proyecto

### Objetivo principal

Construir un modelo predictivo basado en redes neuronales (MLP) que permita estimar el CLTV de los clientes a 6 meses, incorporando variables temporales derivadas del historial de transacciones.

### Preguntas finales

- ¿La clasificación ABC de clientes mejora al utilizar el CLTV predicho?
- ¿El modelo contribuye a una mejor asignación del presupuesto de marketing?

---

## 4. Dataset

Se utilizó el dataset **Online Retail**, disponible en Kaggle.

El conjunto de datos contiene transacciones de una tienda de comercio electrónico del Reino Unido, correspondientes al período 2009–2010. Cada registro representa una línea de producto dentro de una transacción.

Las variables incluyen información como:

- Identificador del cliente
- Identificador de producto
- Fecha y hora de la transacción
- Cantidad de productos comprados
- Factura
- Precio unitario
- País del cliente
- Precio

Este dataset es adecuado para la estimación del CLTV, ya que permite construir variables de comportamiento histórico como recencia, frecuencia y valor monetario, además de variables temporales.

Es importante destacar que el dataset se encuentra a nivel de línea de producto.
Cada registro corresponde a un producto específico incluido dentro de una factura.
Cuando una factura contiene múltiples productos, cada uno de ellos se representa como un registro independiente, con su respectiva cantidad, precio unitario y referencia a la factura asociada.

En consecuencia, múltiples registros pueden pertenecer a una misma factura, y todas las facturas están asociadas a un cliente.

---

## 5. Metodología

El desarrollo del proyecto se organizó en etapas, siguiendo la metodología CRISP-DM, adaptada al contexto de predicción del Customer Lifetime Value (CLTV).

### 5.1 Exploración inicial de los datos

En esta etapa se realizó un análisis preliminar para comprender la estructura general del dataset y evaluar su idoneidad para el problema planteado.
Se analizaron aspectos como:

- Dimensiones del conjunto de datos
- Tipos de variables
- Presencia de valores faltantes
- Rango temporal de las transacciones
- Identificación inicial de registros anómalos

---

### 5.2 Limpieza de datos

A partir de los hallazgos de la exploración inicial, se aplicaron procesos de limpieza para mejorar la calidad de los datos, incluyendo:

- Tratamiento de valores faltantes
- Eliminación de registros inválidos o inconsistentes
- Filtrado de transacciones no representativas para el análisis de CLTV

---

### 5.3 Análisis Exploratorio de Datos (EDA)

Se llevó a cabo un análisis exploratorio más profundo con el objetivo de identificar patrones relevantes en el comportamiento de los clientes.
El EDA incluyó:

- Análisis de distribuciones de variables clave
- Evaluación de la heterogeneidad del valor del cliente
- Comportamiento temporal de las compras
- Relación entre métricas transaccionales y CLTV

---

### 5.4 Feature Engineering

Para capturar la dinámica temporal del comportamiento del cliente, se implementó una estrategia de Ventanas Deslizantes (Rolling Windows). Esto permitió multiplicar los ejemplos de entrenamiento generando cortes de 3 meses de observación para predecir los siguientes 6 meses.

Las transformaciones clave incluyeron:

- Métricas RFM+V: Cálculo de Recencia, Frecuencia, Valor Monetario y Variedad de Productos (Product Variety).

- Log-Transformation: Aplicación de np.log1p a las variables numéricas para reducir el sesgo (skewness) de los datos y facilitar la convergencia de la red neuronal.

- Estacionalidad: Codificación del mes de inicio (month_start) mediante One-Hot Encoding para capturar patrones estacionales.

- Escalado: Estandarización de datos (StandardScaler) ajustado exclusivamente al set de entrenamiento para evitar fuga de datos (Data Leakage).

Estas features permitieron representar de forma más rica la dinámica de compra de cada cliente.

---

### 5.5 Modelado

Se diseñó y entrenó una Red Neuronal Artificial (MLP) utilizando TensorFlow/Keras con la siguiente configuración:

- Arquitectura: Estructura de capas densas (64, 32, 16 neuronas) con función de activación ReLU.

- Regularización: Implementación de capas de Dropout (0.2) para prevenir el sobreajuste (overfitting).

- Optimización: Uso del optimizador Adam y función de pérdida MSE (Mean Squared Error).

- Early Stopping: Mecanismo de parada temprana para detener el entrenamiento cuando la pérdida en validación dejaba de mejorar, asegurando el mejor modelo posible (restore_best_weights).

---

### 5.6 Evaluación del modelo

El desempeño del modelo se evaluó utilizando métricas de regresión adecuadas para la estimación de valores continuos, tales como:

- Error absoluto medio (MAE)
- Raíz del error cuadrático medio (RMSE)

Además, se analizó el impacto del CLTV predicho en la clasificación de clientes.

---

## 6. Resultados

El modelo desarrollado permite estimar el CLTV de los clientes a 6 meses, facilitando:

- La identificación de clientes de alto valor esperado
- La mejora de la clasificación ABC de clientes
- Un soporte cuantitativo para la toma de decisiones de inversión en marketing

---

## 7. Conclusiones

Los resultados muestran que la incorporación de features temporales y un modelo basado en MLP permite capturar de forma efectiva el comportamiento futuro de los clientes.
El CLTV predicho aporta valor para la segmentación y la optimización del presupuesto, contribuyendo a decisiones más informadas y estratégicas.

---

## 8. Estructura del repositorio

- `data/`
  Datos utilizados en el proyecto

- `notebooks/`
  Notebooks de exploración, análisis y modelado

- `src/`
  Funciones y utilidades auxiliares

- `README.md`
  Documentación del proyecto

## 🔗 Links

[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://katherineoelsner.com/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/)
