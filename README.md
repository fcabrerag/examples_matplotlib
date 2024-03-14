# pro_investigacion

Como opinión personal, considero que una imagen vale más que mil palabras. Esto también se puede apreciar en los proyectos de Machine Learning y en todo el apoyo que las visualizaciones nos pueden aportar al momento de tomar decisiones. A través de este cuaderno, deseo mostrar de manera general y entendible mi trabajo en esta área. 

Mi trabajo de tesis trata sobre un tema partícular del ámbito de transporte público llamado bus bunching. 

El “bus bunching” (agrupamiento de buses) es el principal problema para la regularidad de los buses urbanos. El agrupamiento de buses se define como el intervalo de tiempo en que un bus transita al menos junto a otro bus del mismo servicio, separados por un headway menor a una cierta fracción del headway programado. El headway es la diferencia de tiempo que existe entre dos buses que recorren la misma ruta al llegar al mismo punto del recorrido, entendiéndose también como un desfase de sus tiempos de viaje.

Para ello , solicité al ministerio de transporte de mi país un dataset de registros GPS de un servicio de bus específico , que consta de registros de buses GPS para cada bus con una frecuencia de muestreo de 30 segundos.

A continuación, les presento las gráficas construídas como apoyo para este proyecto de investigación:

## 1.- Análisis exploratorio de datos:
### 1.1.- Gráficos distancia acumulada /tiempo de buses de un servicio de bus:
Permiten observar la distancia recorrida por un bus(de un servicio de bus específico) a lo largo del tiempo(hr). Además, es posible realizar zoom en intervalos de distancia y tiempo específicos, buscando patrones para viajes de buses. Mi trabajo de investigación de tesis de magíster trata el problema de  bus bunching, por lo que se desea encontrar características comunes para los viajes de buses que se encuentren viajando cercanamente o viajes de buses(representados por una línea) que se intersecten entre ellos , lo que inmediatamente indicaría presencia del fenómeno. En la imagen se visualizan los viajes de buses(representados cada uno por una serie) en el intervalo comprendido entre las 09:30 horas y las 13:30 horas para los cuatro lunes del mes de Agosto de 2018.
![](https://github.com/fcabrerag/pro_investigacion/blob/main/imagenes/fig_4.1_2.png)

El lenguaje de programación utilizado es Python. Para el tratamiento de datos es usada la librería pandas y en la visualización de resultados la librería Matplotlib.

### 1.2.- Gráficos de contabilización de casos de bunching para un período de tiempo:
Contabilización de casos para dos períodos de tiempo determinados (meses de Julio y Agosto). Para ambos meses, se determinan los paraderos que poseen mayor cantidad de casos positivos de bunching, durante cada uno de los meses presentando casos positivos vs negativos (al situarlos en la misma barra, con efecto de comparación). El valor 1 (color anaranjado) indica existencia de bunching y el valor 0 (color azul) que no existe bunching para ese muestreo de GPS.

![](https://github.com/fcabrerag/pro_investigacion/blob/main/imagenes/fig_3.3.png)

El lenguaje de programación utilizado es Python. Para el tratamiento de datos es usada la librería pandas y en la visualización de resultados la librería Seaborn.

## 2.- Data cleaning and processing of missing data:
### 2.1 Location Validation in GPS Bus Data:

How can I validate a location on a bus trip? Consider that I have a dataset with GPS bus data, and I would like to determine if certain conditions defined by my initial problem are met.
For example, determining if any trip occurs within the predefined geographical area stated in the problem statement or if a GPS coordinate point falls within the boundaries of a city or country.

There are different approaches to solving this problem.In particular, I would like to share a specific solution using the Geopandas library in Python.

One of the defined operations in Geopandas is "within" ,through which we can validate if a GPS point is located within a polygon (the polygon must be loaded beforehand). After performing this spatial join operation, we can exclude data that does not meet the specified condition.

On the following image, we can see the results obtained after performing the spatial join operation. As a result, the incorrect bus trips have been removed from the dataset.

![](https://github.com/fcabrerag/pro_investigacion/blob/main/imagenes/Rows_GPS_20180803.png)


### 2.2.- Linear interpolation of missing data:

The data sampling does not have the same regularity interval for all bus trips. There are times when data values have intervals exceeding 30 seconds (which is the defined time interval between each GPS row). An algorithm was applied to generate new GPS data rows with the correct regular interval. The new latitude and longitude variables were completed using linear interpolation, which calculates intermediate values between two data points with minimal error. The following image shows a comparison between the initial condition and the condition after being corrected by the algorithm.

![](https://github.com/fcabrerag/pro_investigacion/blob/main/imagenes/data_interpolation.png)

El lenguaje de programación utilizado es Python. Para el tratamiento de datos es usada la librería pandas y en la visualización de resultados la librería Matplotlib.

## 3.- Visualización de predicciones de una red neuronal LSTM:
Posterior a la construcción de una red neuronal LSTM (de arquitectura Many-to-One),a través de loops se generan predicciones de los viajes de un bus, en un intervalo de una hora, para los días que fueron seleccionados como el conjunto de test del dataset. Estas predicciones se guardan en archivos de textos , los cuales son leídos a través de un script en Python que se encarga de cargar estos datos y generar las imágenes las cuales son guardadas en un directorio especifico(es un proceso masivo). En la figura se muestran las predicciones para un día puntual en un intervalo de una hora, comparando las predicciones de la red (imagen izquierda) contra los datos reales(imagen derecha).

![](https://github.com/fcabrerag/pro_investigacion/blob/main/imagenes/resultados_red_mo.png)

El lenguaje de programación utilizado es Python. Para el tratamiento de datos es usada la librería pandas y en la visualización de resultados la librería Matplotlib.




