## Modelo Predictivo de Visibilidad y Seguridad Vial en la RN3

## Entrega 2: Descripción del Dataset y Origen

## Aprendizaje Automático

## Alumno; LARA, Giovanna Estefania

link Github; https://github.com/gi0lara/modelo_predictivo_rn3.git


## Introducción


## Origen del dataset

 Los datos meteorológicos utilizados en este proyecto fueron obtenidos de Meteostat, una plataforma de acceso abierto que brinda información climática histórica de distintas partes del mundo. Para el análisis se seleccionaron las estaciones meteorológicas oficiales de las dos principales ciudades de la provincia de Tierra del Fuego: Ushuaia (representativa de la zona sur y cordillerana) y Río Grande (representativa de la zona norte y esteparia).

Durante la recopilación de los datos surgió una dificultad importante. Al descargar grandes períodos de tiempo de manera automática, algunas variables relevantes no se incluían correctamente, especialmente la columna coco (Código de Condición Climática), que resulta fundamental para el entrenamiento supervisado de los modelos utilizados en este trabajo.

Para solucionar este problema, se optó por realizar las descargas en períodos más pequeños, organizados de forma semanal para cada ciudad. De esta manera se logró obtener la información completa y garantizar la presencia de todas las variables necesarias. El período analizado abarca desde enero de 2023 hasta abril de 2026.


●​ link dataset Rio Grande: https://meteostat.net/es/station/87934?t=2026-05-19/2026-05-26


●​ link dataset Ushuaia: https://meteostat.net/es/station/87938?t=2026-05-19/2026-05-26


## Integración y Consolidación del Dataset


Una vez descargados los archivos semanales de las estaciones meteorológicas de Ushuaia y Río Grande, se realizó el proceso de integración de los datos utilizando la herramienta de Excel. En primer lugar, se unieron todos los archivos correspondientes a cada ciudad para formar una única base de datos histórica continua. De esta manera se obtuvieron dos conjuntos de datos completos, uno para Ushuaia y otro para Río Grande, con información recopilada durante más de tres años.

Luego, ambas bases fueron combinadas en una sola hoja de trabajo. Para ello, los registros se alinearon según la fecha y hora de cada medición, asegurandoque cada fila contuviera información correspondiente al mismo momento temporal en ambas ciudades. Finalmente, el archivo consolidado fue guardado en formato .xlsx para su posterior importación y procesamiento en Python.


## Descripción del dataset

 El dataset final utilizado para el proyecto está compuesto por 29.184 registros y 19 variables. La información corresponde a observaciones meteorológicas de las ciudades de Río Grande y Ushuaia, organizadas en función de una variable temporal (time) almacenada en formato fecha y hora. Las restantes 18 variables son de tipo numérico (float64) e incluyen mediciones relacionadas con temperatura (temp), punto de rocío (dwpt), humedad relativa (rhum), precipitaciones (prcp), presión atmosférica (pres), dirección del viento (wdir), velocidad del viento (wspd), ráfagas máximas de viento (wpgt) y condición meteorológica (coco) para ambas ciudades. El conjunto de datos presenta algunos valores faltantes, principalmente en las variables de ráfagas máximas de viento (wpgt_Rio Grande y wpgt_Ushuaia), mientras que el resto de las variables cuenta con una cobertura superior al 97% de los registros. El tamaño total del dataset en memoria es de aproximadamente 4,2 MB.


El análisis descriptivo de las principales variables meteorológicas muestra que las temperaturas medias registradas fueron de 6,20 °C en Río Grande y 6,40 °C en Ushuaia, con valores que oscilaron entre -12,6 °C y 25 °C en Río Grande, y entre -6°C y 25 °C en Ushuaia. La humedad relativa presentó promedios elevados en ambas ciudades, alcanzando 74,31 % en Río Grande y 73,24 % en Ushuaia, lo que refleja las características climáticas predominantes de la región. Respecto a las precipitaciones, se observó una media de 0,055 mm en Río Grande y 0,119 mm en Ushuaia, aunque la mediana fue de 0 mm en ambos casos, indicando que la mayoría de los registros no presentan precipitaciones y que los eventos de lluvia se concentran en determinados períodos. Asimismo, las precipitaciones máximas alcanzaron 8,2 mm en Río Grande y 7,5 mm en Ushuaia, evidenciando la ocurrencia ocasional de eventos de mayor intensidad. En general, las distribuciones muestran una importante variabilidad térmica y niveles de humedad elevados, características propias del clima fueguino.

## Matriz de correlacion de las variables meteorologicas de ambas ciudades

<img width="1023" height="943" alt="image" src="https://github.com/user-attachments/assets/42ea05f2-9e05-40d0-a532-6af15e55fe73" />


## Matriz de correlaciones de la ciudad de rio grande

<img width="634" height="542" alt="image" src="https://github.com/user-attachments/assets/e78a8efb-6deb-4e07-b299-c9309e3db5ea" />


## Matriz de correlaciones de la ciudad de Ushuaia

<img width="612" height="521" alt="image" src="https://github.com/user-attachments/assets/498a9b4c-6b8c-4a00-af9b-21e91c50011a" />

## Distribución de coco por ciudad

<img width="1390" height="490" alt="image" src="https://github.com/user-attachments/assets/a56c5bbe-4a8d-495f-956c-26076136ebc7" />


## Humedad relativa: Río Grande vs Ushuaia
<img width="676" height="451" alt="image" src="https://github.com/user-attachments/assets/b173305a-65b9-41a6-bb7c-48d1d012b40d" />


## Diferencia entre Temperatura y Dew Point
<img width="667" height="451" alt="image" src="https://github.com/user-attachments/assets/f3abc33c-cedd-4046-b3d0-3c1bbe9d4afb" />

## Punto de rocio: Rio Grande vs Ushuaia
<img width="678" height="451" alt="image" src="https://github.com/user-attachments/assets/8ef654f0-e6e3-4a40-b265-bcb9f53b5bfe" />


## Distribución de Temperaturas (Ushuaia vs Río Grande)

El gráfico de densidad permite observar las diferencias en el comportamiento de las temperaturas entre Río Grande y Ushuaia. En Río Grande, la distribución es más amplia, lo que indica una mayor variación térmica a lo largo del tiempo, registrándose tanto temperaturas muy bajas como valores más elevados durante los meses cálidos. En cambio, Ushuaia presenta una distribución más concentrada, con temperaturas que tienden a mantenerse dentro de un rango más estable. Esto puede explicarse teniendo en cuenta la influencia marítima del Canal Beagle, que contribuye a moderar las variaciones extremas de temperatura.

Desde el punto de vista del modelo, estas diferencias resultan relevantes ya que permiten identificar patrones climáticos distintos entre ambas ciudades. La combinación de temperaturas registradas en cada localidad puede aportar información útil para detectar la probabilidad de congelamiento diferencial en los tramos intermedios de la calzada

<img width="989" height="490" alt="image" src="https://github.com/user-attachments/assets/98729aa4-643f-4fae-b765-7d84e2f3802e" />


## Relación de Humedad Relativa entre ambas ciudades (Scatter Plot)

El gráfico de dispersión muestra que la mayor parte de las observaciones se concentra en valores altos de humedad relativa para ambas ciudades. Esto indica que la humedad es una característica frecuente en la región. Sin embargo, también se observan diferencias entre los valores    registrados   en   cada localidad, lo que demuestra que las condiciones atmosféricas no siempre evolucionan de la misma manera.

Para el modelo, esta situación es beneficiosa porque ambas variables aportan información complementaria. Analizar simultáneamente la humedad de Río Grande y Ushuaia puede ayudar a identificar distintos escenarios climáticos que podrían afectar las condiciones de circulación en la Ruta Nacional Nº 3.

<img width="790" height="590" alt="image" src="https://github.com/user-attachments/assets/d40210e5-b278-4031-9c7d-d25f6a779278" />



## Comportamiento de las Precipitaciones por ciudad


 Los diagramas de caja muestran que la mayoría de los registros presentan precipitaciones nulas o muy bajas, algo esperable considerando que gran parte de los días no se registran eventos significativos de lluvia o nieve. No obstante, también aparecen valores extremos que representan episodios de precipitaciones más intensas.

Estos valores no fueron considerados errores ni eliminados durante el proceso de limpieza, ya que corresponden a fenómenos meteorológicos reales. Además, resultan especialmente importantes para el proyecto porque pueden estar asociados a situaciones de mayor riesgo para la circulación vehicular. Los modelos seleccionados, como Árboles de Decisión y Random Forest, pueden trabajar adecuadamente con este tipo de valores extremos y utilizarlos para mejorar la identificación de escenarios críticos.


<img width="1189" height="495" alt="image" src="https://github.com/user-attachments/assets/04b85168-87ba-485f-811a-d7bafd048f6a" />



## Frecuencia de eventos extremos

El gráfico muestra la frecuencia de eventos extremos(niebla, niebla helada, lluvia intensa, nevadas y nevadas intensas, chubascos intensos de lluvia y nieve, chubascos de nieve, tormentas eléctricas y temporales severos, correspondientes a los códigos meteorológicos 5, 6, 9, 15, 16, 18, 21, 22, 25 y 27.) registrada en las dos localidades analizadas. Se observa que Río Grande presenta una proporción ligeramente mayor de eventos extremos, alcanzando un 5,51 % del total de observaciones, mientras que Ushuaia registra apenas un 1,08 %. Esto indica que los eventos extremos son aproximadamente cinco veces más frecuentes en Río Grande que en Ushuaia, evidenciando una mayor variabilidad o exposición a condiciones extremas en la primera localidad durante el período estudiado.
<img width="531" height="374" alt="image" src="https://github.com/user-attachments/assets/746e3436-3165-4f77-9fd0-69ae82002aad" />


## Documentacion de meteosat: https://dev.meteostat.net/formats.html#meteorological-parameters

