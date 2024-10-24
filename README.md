#Clasificación de Clientes de Tarjetas de Crédito a través de Algoritmos de Clustering
1. Introducción
El objetivo de este proyecto es realizar una segmentación de clientes de tarjetas de crédito utilizando algoritmos de clustering. Para este fin, se empleó el algoritmo KMeans, el cual se seleccionó como el mejor modelo en función de varias métricas de evaluación de desempeño. El análisis está basado en un conjunto de datos que describe el comportamiento de uso de tarjetas de crédito de aproximadamente 9,000 clientes activos.
2. Metodología
2.1 Análisis Exploratorio de Datos (EDA)
Se realizó un análisis preliminar de las variables numéricas y categóricas presentes en el dataset, evaluando su distribución y posibles valores atípicos.
2.2 Preprocesamiento de Datos
Los datos fueron normalizados utilizando el método de escalado estándar (StandardScaler) para asegurar que todas las variables tengan una influencia similar en el proceso de clustering. Además, se realizaron las siguientes transformaciones:
•	Codificación de variables categóricas (si aplica).
•	Relleno de valores faltantes utilizando la mediana de cada variable.
•	Eliminación de outliers detectados mediante análisis de boxplots.
2.3 Selección de Algoritmo de Clustering
Se compararon varios algoritmos de clustering, incluyendo KMeans, DBSCAN y Agglomerative Clustering. KMeans fue seleccionado como el mejor algoritmo basado en las siguientes métricas de evaluación:
•	Silhouette Score: Mide qué tan similares son los puntos dentro de un mismo cluster.
•	Calinski-Harabasz Index: Evalúa la proporción entre la dispersión intra-cluster y la inter-cluster.
•	Davies-Bouldin Index: Mide la relación entre las distancias dentro de los clusters y las distancias entre los clusters.
3. Implementación Técnica
3.1 Algoritmo Seleccionado: KMeans
Se entrenó un modelo de clustering utilizando el algoritmo KMeans, con un número óptimo de 3 clusters basado en las métricas previamente mencionadas.
 

3.2 Evaluación del Modelo
Las métricas de desempeño utilizadas para evaluar los modelos fueron:
 
Conclusión:
•	KMeans obtuvo los mejores resultados en el Silhouette Score y el Calinski-Harabasz Index, lo que sugiere que forma los clusters más compactos y bien separados.
•	DBSCAN obtuvo el mejor resultado en el Davies-Bouldin Index, pero su desempeño en las otras métricas fue inferior.
Por lo tanto, el mejor modelo en general, considerando las tres métricas, es KMeans.
4. Interpretación de Resultados
4.1 Visualización de los Clusters
Se generaron visualizaciones de boxplots para las variables numéricas escaladas con el fin de analizar las distribuciones de estas variables entre los tres clusters.
 
4.2 Insights Clave de las Distribuciones
Al observar las distribuciones de las variables numéricas por cada cluster, se obtuvieron los siguientes insights clave:
•	BALANCE: Los clientes en el Cluster 1 tienden a tener balances más altos.
•	ONEOFF_PURCHASES: El Cluster 1 realiza más compras puntuales en comparación con los otros clusters.
•	CASH_ADVANCE: El Cluster 2 hace mayor uso de adelantos en efectivo.
•	CREDIT_LIMIT: Los clientes en el Cluster 1 tienen límites de crédito más altos, lo que sugiere un menor riesgo percibido por la institución financiera.
4.3 Visualización de Clusters con Gráficos de Dispersión
Se generaron gráficos de dispersión para observar la relación entre pares de variables, coloreados por los clusters obtenidos con KMeans.
 
4.4 Clasificación de Variables en Rangos
Se categorizó cada variable numérica en rangos (bajo, intermedio y alto) basados en sus cuartiles, lo que permitió una interpretación más intuitiva del comportamiento de los clientes.
  
5. Implementación en el Negocio
Los resultados de este análisis pueden ayudar a la institución financiera a:
•	Personalizar ofertas y productos: Enfocarse en los clientes del Cluster 1 con productos premium y límites de crédito más altos, ya que estos clientes demuestran un uso más intensivo de sus tarjetas.
•	Gestión de riesgo: Implementar estrategias para mitigar el riesgo de los clientes del Cluster 2, quienes tienden a usar más adelantos en efectivo.
•	Estrategias de retención: Desarrollar estrategias específicas para los clientes del Cluster 0, quienes hacen un uso más moderado de sus tarjetas de crédito, para aumentar su lealtad y frecuencia de uso.
6. Limitaciones del Análisis
•	Datos no balanceados: Algunos grupos de clientes pueden estar subrepresentados en los datos, lo que podría afectar los resultados.
•	Posibles outliers: A pesar de los esfuerzos de limpieza, podrían existir outliers que influyen en los resultados del modelo.
7. Conclusiones y Recomendaciones
El modelo KMeans fue capaz de identificar tres segmentos clave de clientes de tarjetas de crédito, cada uno con comportamientos de uso distintos. Estos segmentos pueden ser utilizados para desarrollar estrategias personalizadas, mejorar la gestión del riesgo crediticio y aumentar la rentabilidad a través de ofertas dirigidas.
8. Trabajo Futuro
•	Explorar otros algoritmos de clustering como Gaussian Mixture Models para mejorar la segmentación.
•	Incluir variables categóricas adicionales o datos demográficos para un análisis más detallado.
•	Implementar un sistema de recomendación basado en los clusters obtenidos.
