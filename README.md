# Clasificación de Clientes de Tarjetas de Crédito a través de Algoritmos de Clustering

## 1. Introducción
Este proyecto tiene como objetivo segmentar clientes de tarjetas de crédito mediante algoritmos de clustering, con el fin de identificar grupos de comportamiento homogéneo. Se utilizó el algoritmo **KMeans**, que fue seleccionado como el mejor modelo basado en diversas métricas de evaluación. El análisis se realizó sobre un dataset que contiene el comportamiento de uso de aproximadamente 9,000 clientes activos.

## 2. Metodología

### 2.1 Análisis Exploratorio de Datos (EDA)
Se llevó a cabo un análisis exploratorio para evaluar la distribución de las variables numéricas y categóricas, identificando posibles valores atípicos y patrones clave.

### 2.2 Preprocesamiento de Datos
Los datos fueron preprocesados con las siguientes transformaciones:
- **Normalización:** Las variables numéricas se escalaron utilizando `StandardScaler` para garantizar su comparabilidad.
- **Manejo de datos faltantes:** Se imputaron valores faltantes con la mediana de cada variable.
- **Eliminación de outliers:** Se eliminaron valores atípicos detectados a través de boxplots.
- **Codificación de variables categóricas:** Si aplicaba.

### 2.3 Selección de Algoritmo de Clustering
Se evaluaron diversos algoritmos de clustering, entre ellos **KMeans**, **DBSCAN**, y **Agglomerative Clustering**. **KMeans** fue seleccionado como el mejor algoritmo, basándose en las siguientes métricas:
- **Silhouette Score:** Mide la cohesión dentro de los clusters.
- **Calinski-Harabasz Index:** Evalúa la relación entre la dispersión intra-cluster e inter-cluster.
- **Davies-Bouldin Index:** Mide la compactación de los clusters en relación con su separación.

## 3. Implementación Técnica

### 3.1 Algoritmo Seleccionado: KMeans
El modelo **KMeans** se entrenó con 3 clusters, que se determinaron como el número óptimo basado en las métricas mencionadas anteriormente.

### 3.2 Evaluación del Modelo
Se compararon los algoritmos según las siguientes métricas:
- **KMeans** obtuvo el mejor rendimiento en **Silhouette Score** y **Calinski-Harabasz Index**, lo que indica que formó clusters compactos y bien separados.
- **DBSCAN** sobresalió en el **Davies-Bouldin Index**, pero su desempeño en las demás métricas fue inferior.

Con base en estos resultados, **KMeans** fue elegido como el mejor modelo global.

## 4. Interpretación de Resultados

### 4.1 Visualización de los Clusters
Se generaron **boxplots** para analizar las distribuciones de las variables numéricas escaladas entre los tres clusters.

### 4.2 Insights Clave
A partir de las distribuciones de las variables, se identificaron los siguientes comportamientos:
- **BALANCE:** Los clientes del Cluster 1 tienden a tener balances más altos.
- **ONEOFF_PURCHASES:** El Cluster 1 realiza más compras puntuales.
- **CASH_ADVANCE:** El Cluster 2 muestra mayor uso de adelantos en efectivo.
- **CREDIT_LIMIT:** Los clientes del Cluster 1 tienen límites de crédito más altos, lo que sugiere menor riesgo percibido por la institución financiera.

### 4.3 Gráficos de Dispersión
Se generaron gráficos de dispersión para visualizar las relaciones entre pares de variables, coloreados por los clusters obtenidos.

### 4.4 Clasificación de Variables en Rangos
Las variables numéricas se clasificaron en rangos (bajo, intermedio, alto) según los cuartiles, facilitando una interpretación más intuitiva del comportamiento de los clientes.

## 5. Implementación en el Negocio
Los resultados de este análisis proporcionan las siguientes aplicaciones para la institución financiera:
- **Personalización de productos:** Ofrecer productos premium y límites de crédito más altos a los clientes del Cluster 1.
- **Gestión de riesgos:** Implementar estrategias para mitigar riesgos en clientes del Cluster 2, que tienden a usar más adelantos en efectivo.
- **Estrategias de retención:** Desarrollar estrategias de fidelización para los clientes del Cluster 0, que muestran un uso moderado de sus tarjetas de crédito.

## 6. Limitaciones del Análisis
- **Desbalance en los datos:** Algunos grupos de clientes pueden estar subrepresentados, lo que podría afectar los resultados.
- **Outliers:** Aunque se eliminaron algunos, podrían persistir valores atípicos que influyan en el modelo.

## 7. Conclusiones y Recomendaciones
El modelo **KMeans** identificó tres segmentos clave de clientes, cada uno con comportamientos de uso distintos. Estos insights pueden ser utilizados para desarrollar estrategias de marketing, mejorar la gestión del riesgo crediticio y aumentar la rentabilidad mediante ofertas personalizadas.

## 8. Trabajo Futuro
- Explorar otros algoritmos de clustering, como **Gaussian Mixture Models**, para mejorar la segmentación.
- Incorporar variables categóricas adicionales o datos demográficos para un análisis más completo.
- Desarrollar un sistema de recomendación basado en los clusters obtenidos.
