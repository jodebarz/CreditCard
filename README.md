# README: Clasificación de Clientes de Tarjetas de Crédito a través de Algoritmos de Clustering

# 1. Introducción
## 1.1. El Problema

Las entidades financieras enfrentan el desafío de comprender y gestionar eficazmente el comportamiento de los titulares de tarjetas de crédito. Con aproximadamente 9,000 clientes activos, es esencial identificar patrones en su uso a lo largo de los últimos seis meses para optimizar las estrategias de marketing y mejorar la gestión del riesgo. La falta de segmentación adecuada puede llevar a decisiones subóptimas, afectando tanto la satisfacción del cliente como la rentabilidad de las instituciones. La comprensión de las dinámicas de uso de las tarjetas de crédito se convierte en una oportunidad de negocio crucial para personalizar ofertas y maximizar el retorno de inversión en campañas.

## 1.2. La Solución

Para abordar este problema, proponemos una solución basada en la segmentación de clientes utilizando algoritmos de clustering. Esta técnica permitirá identificar grupos de comportamiento homogéneo entre los titulares de tarjetas, facilitando la personalización de ofertas y mejorando la gestión del riesgo. Aunque en esta fase de la presentación no profundizaremos en detalles técnicos, es importante destacar que existen soluciones similares en el ámbito del machine learning, que han demostrado ser efectivas en la segmentación de clientes y en la optimización de estrategias de marketing. Al aplicar estas metodologías, buscamos no solo entender el comportamiento de nuestros clientes, sino también transformar esos insights en oportunidades de negocio que beneficien tanto a las entidades financieras como a sus clientes.


# 2. Metodología

### 2.1 Análisis Exploratorio

En esta sección, se describe el conjunto de datos utilizado para el análisis de segmentación de clientes. El conjunto de datos contiene 8950 registros y 18 columnas, de las cuales las más relevantes para nuestro análisis son las que están relacionadas con el comportamiento financiero de los titulares de tarjetas de crédito.

#### Descripción del Conjunto de Datos

El conjunto de datos incluye las siguientes columnas:

- **CUST_ID**: Identificador único del cliente.
- **BALANCE**: Saldo actual de la cuenta.
- **BALANCE_FREQUENCY**: Frecuencia con la que se revisa el saldo.
- **PURCHASES**: Total de compras realizadas.
- **ONEOFF_PURCHASES**: Compras únicas realizadas.
- **INSTALLMENTS_PURCHASES**: Compras realizadas a plazos.
- **CASH_ADVANCE**: Adelantos en efectivo.
- **PURCHASES_FREQUENCY**: Frecuencia de compras.
- **CREDIT_LIMIT**: Límite de crédito del cliente.
- **PAYMENTS**: Total de pagos realizados.
- **MINIMUM_PAYMENTS**: Pagos mínimos que se deben realizar.
- **TENURE**: Número de meses que el cliente ha tenido la tarjeta.

#### Estadísticas Descriptivas

Los datos muestran un resumen estadístico revelador:

- El saldo promedio (**BALANCE**) es de $1564.47, con una alta desviación estándar (**STD**: $2081.53), lo que sugiere una gran variabilidad en los saldos.
- La mayoría de los usuarios realiza un número limitado de **PURCHASES** (promedio: $1003.20), pero algunas transacciones alcanzan cifras significativamente más altas (máximo: $49039.57).
- Se observa que el **CREDIT_LIMIT** promedio es de $4494.45, lo que indica que muchos clientes operan con límites de crédito relativamente bajos.

#### Visualización de Datos

Se realizaron histogramas y boxplots para visualizar la distribución de las variables numéricas:

- **Distribución de Variables**: Las gráficas revelan que la mayoría de los usuarios tienden a mantener balances bajos y realizan pocos adelantos en efectivo. Sin embargo, un pequeño porcentaje muestra balances significativamente más altos, indicando la presencia de clientes premium o de alto riesgo.
- **Frecuencia de Compras**: Aunque la frecuencia de revisiones de balances y compras es alta, las actividades como adelantos en efectivo y compras a plazos son menos comunes, lo que podría sugerir una oportunidad para fomentar el uso de estas opciones entre los clientes.

#### Correlaciones entre Variables

Se realizó un análisis de correlación para identificar relaciones entre variables. La matriz de correlación revela:

- **Correlaciones Positivas Fuertes**:
  - **PURCHASES** y **ONEOFF_PURCHASES** (0.92): Indica que los clientes que realizan muchas compras tienden a hacer compras no recurrentes.
  - **PURCHASES_INSTALLMENTS_FREQUENCY** y **PURCHASES_FREQUENCY** (0.86): Los clientes que realizan compras a plazos también hacen compras más frecuentes.
  - **CREDIT_LIMIT** y **BALANCE** (0.53): Los clientes con mayores límites de crédito tienden a tener balances más altos.
  
- **Correlaciones Negativas**:
  - **PRC_FULL_PAYMENT** y **BALANCE** (-0.32): Los clientes que suelen pagar el total de su deuda tienen saldos más bajos, lo que puede reflejar un comportamiento financiero más responsable.

#### Limpieza de Datos

Antes de proceder con el modelado, se llevó a cabo un proceso de limpieza de datos:

- **Duplicados**: Se verificó que no existan registros duplicados.
- **Valores Nulos**: Se identificaron algunas columnas con valores nulos, como **CREDIT_LIMIT** y **MINIMUM_PAYMENTS**. Los nulos en **CREDIT_LIMIT** fueron reemplazados por la mediana de la columna debido a la presencia de valores atípicos. En el caso de **MINIMUM_PAYMENTS**, se aplicó la misma estrategia.
- **Verificación Final**: Se revisó que no quedaran nulos después de los reemplazos, asegurando así la integridad de los datos para el análisis posterior.

## 2.2. Procesamiento de Datos

El procesamiento de datos se centró en la normalización de variables numéricas, asegurando que todas contribuyan equitativamente al rendimiento del modelo. Para ello, se utilizó **StandardScaler**, que ajusta las variables para que tengan una media de cero y una desviación estándar de uno, lo cual es crucial para algoritmos sensibles a la escala.

Adicionalmente, se eliminaron variables irrelevantes y se realizaron técnicas de **feature engineering** para crear nuevas características basadas en los datos existentes. Entre las características avanzadas generadas, se incluyeron:

### Características de Comportamiento de Pago:
- **Frecuencia de pagos**: Calculada como el total de pagos dividido entre el número de compras, permite evaluar con qué frecuencia un cliente paga sus deudas.
- **Porcentaje de pagos mínimos realizados**: Relaciona los pagos mínimos con el total de pagos, lo que ayuda a comprender la tendencia de pago del cliente.

### Características de Comportamiento de Compra:
- **Porcentaje de compras a crédito**: Proporción de las compras realizadas a crédito en comparación con el total, útil para evaluar el comportamiento de compra del cliente.
- **Compras totales respecto al límite de crédito**: Mide qué tan cerca está el cliente de utilizar su límite de crédito, proporcionando información valiosa sobre su utilización.

### Características Derivadas de Transacciones:
- **Frecuencia de transacciones**: Indica cuántas transacciones realiza un cliente en un periodo determinado.
- **Promedio de adelantos en efectivo por transacción**: Proporciona datos sobre la dependencia del cliente de los adelantos en efectivo.

Para comprender mejor la distribución de estas nuevas características y detectar posibles outliers, se generaron histogramas y boxplots.

Cabe mencionar que, dado que el conjunto de datos solo contiene variables numéricas, no fue necesario realizar un paso de **encoding** (transformación de variables categóricas a formato numérico). Además, se eliminaron variables redundantes como `PURCHASES`, `PURCHASES_FREQUENCY`, y `CASH_ADVANCE_TRX`, enfocándose en aquellas características que realmente aportan valor al análisis.


## 2.3. Entrenamiento y ajuste de hiperparámetros

Se adoptó un enfoque iterativo para entrenar el modelo KMeans, implementando una búsqueda de hiperparámetros mediante el método del codo y la validación cruzada para determinar el número óptimo de clusters, seleccionando finalmente 3 clusters por su simplicidad y efectividad en la segmentación de datos bien definidos.

Se evaluaron diferentes algoritmos de clustering, incluidos DBSCAN y Agglomerative Clustering, destacando a KMeans como el mejor algoritmo basado en métricas como el Silhouette Score, el Calinski-Harabasz Index, y el Davies-Bouldin Index. KMeans logró clusters compactos y bien separados, mientras que DBSCAN presentó un rendimiento inferior en las métricas de cohesión y dispersión.

Estos resultados justifican la elección de KMeans como el modelo más adecuado para la clasificación.


## 2.4. Interpretación de los Clusters

Se realizaron visualizaciones, como gráficos de dispersión y diagramas de caja, para analizar la distribución de las variables en los clusters generados mediante K-means, lo que permitió identificar características distintivas y patrones de gasto de los clientes. 

El análisis reveló tres clusters:

- **Cluster 1**: Clientes de alto poder adquisitivo y bajo riesgo, que mostraron alta actividad en el uso de tarjetas.
- **Cluster 2**: Con un enfoque cauteloso hacia el gasto, evidenció limitaciones en compras en efectivo.
- **Cluster 3**: Aunque con buenos balances, prefirió mantener liquidez inmediata.

## 3. Implementación en el negocio

Para llevar a cabo la implementación del modelo, se recomienda integrar la segmentación de clientes en el sistema de CRM de la empresa. Esta integración no solo facilitará la personalización de las ofertas según el comportamiento específico de cada cliente, sino que también permitirá una comunicación más efectiva. Diversas organizaciones han experimentado mejoras significativas en la retención y la satisfacción del cliente a través de enfoques similares, lo que resalta la importancia de adoptar una estrategia basada en datos.

- **Ofertas Personalizadas:** Diseñar campañas de marketing específicas para cada clúster, optimizando así la efectividad de las comunicaciones y promociones.

- **Gestión del Riesgo:** Utilizar la información recopilada sobre los comportamientos de cada clúster para ajustar las políticas de crédito, minimizando así el riesgo de impagos.

- **Monitoreo Continuo:** Establecer un sistema de seguimiento que permita adaptar las estrategias de manera proactiva en función de los cambios en el comportamiento del cliente, asegurando que la empresa se mantenga alineada con las necesidades y expectativas del mercado.

## 4. Limitaciones

El análisis se basa en datos históricos, lo que puede no reflejar cambios en el comportamiento del consumidor a futuro. Entre las limitaciones identificadas, destaca la **falta de información sobre el historial crediticio** de los clientes, un factor que podría influir en su comportamiento al utilizar las tarjetas. Además, la **selección de características** puede ser limitada; podría ser útil explorar otras variables no incluidas en el análisis.

Otra limitación importante es el **poder computacional limitado**, que puede haber restringido la capacidad para experimentar con modelos más complejos. Estas limitaciones podrían afectar la **precisión de los clusters generados** y, por lo tanto, los resultados del análisis.


## 5. Conclusiones y recomendaciones
El proyecto ha logrado segmentar exitosamente a los clientes de tarjetas de crédito, proporcionando **insights valiosos** sobre sus comportamientos. Se recomienda a otros analistas considerar la inclusión de datos adicionales, como el historial crediticio, para mejorar la capacidad de discriminación de los clusters. Para optimizar aún más la personalización de las ofertas, se sugiere registrar información adicional sobre las interacciones de los clientes con el servicio.

Se recomienda:

1. **Ofertas Personalizadas**: Diseñar campañas de marketing dirigidas a cada cluster para maximizar la efectividad.
2. **Gestión del Riesgo**: Utilizar la información sobre los comportamientos de cada cluster para ajustar políticas de crédito.
3. **Monitoreo Continuo**: Establecer un sistema de seguimiento para adaptar estrategias basadas en cambios en el comportamiento del cliente.

Se puede concluir que:

El análisis y la segmentación de clientes de tarjetas de crédito ofrecen oportunidades significativas para mejorar la gestión del riesgo y la personalización de servicios financieros. Implementar un enfoque basado en datos permitirá a las instituciones financieras optimizar sus operaciones y ofrecer un mejor servicio a sus clientes.


## 6. Trabajo Futuro

En futuras iteraciones del proyecto, se podrían explorar técnicas de clustering más avanzadas, como DBSCAN o Gaussian Mixture Models, con el objetivo de mejorar la segmentación. Además, sería beneficioso incorporar un análisis temporal para observar cómo evolucionan los patrones de comportamiento a lo largo del tiempo, lo que permitiría una segmentación más dinámica y adaptativa.

### Acciones a Considerar

- Investigar la incorporación de datos adicionales (por ejemplo, datos demográficos) para enriquecer la segmentación.
- Evaluar la efectividad de las recomendaciones implementadas a lo largo del tiempo.

