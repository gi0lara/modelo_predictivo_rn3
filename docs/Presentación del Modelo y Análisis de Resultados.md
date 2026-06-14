## Modelo Predictivo de Visibilidad y Seguridad Vial en la RN3

## Entrega 3: Presentación del Modelo y Análisis de Resultados

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

La matriz de correlación general permite visualizar simultáneamente las relaciones existentes entre todas las variables meteorológicas registradas en las ciudades de Río Grande y Ushuaia. Los colores rojizos representan correlaciones positivas, mientras que los tonos azulados indican correlaciones negativas. Cuanto más intenso es el color, mayor es la fuerza de la relación.

Se observa una fuerte correlación positiva entre las temperaturas de ambas ciudades, lo que indica que los cambios térmicos suelen producirse de manera similar en toda la provincia. Del mismo modo, las variables relacionadas con el punto de rocío (dwpt) presentan correlaciones elevadas entre ambas localidades, reflejando patrones atmosféricos compartidos.
Las variables de velocidad y ráfaga de viento también muestran asociaciones positivas importantes tanto dentro de cada ciudad como entre ciudades, evidenciando que los eventos de viento intenso suelen afectar a la región de manera conjunta. En contraste, la humedad relativa presenta correlaciones negativas moderadas con la temperatura, indicando que los períodos más cálidos suelen estar asociados a una menor humedad relativa del aire.

Ademas que nos muestra que  la presión atmosférica mantiene correlaciones negativas débiles a moderadas con la temperatura y la velocidad del viento, sugiriendo que las condiciones de baja presión suelen estar asociadas con situaciones meteorológicas más dinámicas y ventosas.

<img width="1023" height="943" alt="image" src="https://github.com/user-attachments/assets/42ea05f2-9e05-40d0-a532-6af15e55fe73" />


## Matriz de correlaciones de la ciudad de rio grande

El análisis específico para Río Grande muestra que la temperatura presenta una correlación positiva con el punto de rocío (0,67), lo que indica que cuando aumenta la temperatura también tiende a incrementarse la cantidad de vapor de agua presente en la atmósfera.
Tambien se observa una correlación negativa considerable entre temperatura y humedad relativa (-0,66). Este comportamiento es esperable, ya que al aumentar la temperatura la capacidad del aire para contener vapor de agua se incrementa, reduciendo la humedad relativa si la cantidad de humedad disponible permanece constante.
La velocidad del viento presenta una correlación positiva moderada con la temperatura ( 0,50), sugiriendo que las jornadas más cálidas suelen estar acompañadas por vientos de mayor intensidad. Por otro lado, la humedad relativa y la velocidad del viento exhiben una correlación negativa relativamente fuerte (-0,62), indicando que las condiciones más secas suelen coincidir con velocidades de viento más elevadas.
La presión atmosférica muestra correlaciones negativas débiles con la temperatura (-0,20) y con la velocidad del viento (-0,34), mientras que la precipitación presenta relaciones muy bajas con el resto de las variables analizadas. Esto sugiere que las precipitaciones en Río Grande dependen de una combinación más compleja de factores meteorológicos y no de una única variable dominante.

<img width="634" height="542" alt="image" src="https://github.com/user-attachments/assets/e78a8efb-6deb-4e07-b299-c9309e3db5ea" />


## Matriz de correlaciones de la ciudad de Ushuaia

En el analisis puntualizado de  Ushuaia se observan patrones similares a los registrados en Río Grande. La relación más destacada corresponde a la temperatura y el punto de rocío, con una correlación positiva de 0,71, ligeramente superior a la observada en Río Grande. Esto indica una fuerte asociación entre el calentamiento del aire y el incremento del contenido de humedad atmosférica.
La temperatura también presenta una correlación negativa importante con la humedad relativa (-0,62), confirmando que las condiciones más cálidas suelen asociarse con menores niveles de humedad relativa. Sin embargo, a diferencia de Río Grande, la velocidad del viento muestra una relación prácticamente nula con la temperatura (0,07), lo que indica que ambas variables evolucionan de forma relativamente independiente en Ushuaia.
La presión atmosférica mantiene correlaciones negativas débiles tanto con la temperatura (-0,17) como con la precipitación (-0,20), mientras que las precipitaciones presentan relaciones muy bajas con la mayoría de las variables meteorológicas analizadas. Esto sugiere que los eventos de lluvia o nieve en Ushuaia están influenciados por múltiples factores atmosféricos y no pueden explicarse únicamente mediante las variables consideradas en este análisis.

<img width="612" height="521" alt="image" src="https://github.com/user-attachments/assets/498a9b4c-6b8c-4a00-af9b-21e91c50011a" />

## Distribución de condición meteorológica (coco) por ciudad

La distribución de los códigos COCO permite visualizar  las condiciones meteorológicas predominantes en Río Grande y Ushuaia durante el período analizado. En ambas localidades se observa un claro predominio de los códigos asociados a condiciones de cielo despejado, poco nuboso y nublado (códigos 1, 2 y 3), siendo este último el más frecuente en los dos casos. Este comportamiento indica que gran parte de las observaciones corresponden a situaciones atmosféricas estables, sin fenómenos meteorológicos severos.

En Río Grande destaca la elevada frecuencia del código 3 (nublado), lo que evidencia una marcada recurrencia de condiciones de cielo cubierto o mayormente nublado. Asimismo, la presencia relativamente importante del código 5 (niebla) sugiere que los episodios de niebla constituyen un fenómeno meteorológico recurrente en la zona. Por su parte, Ushuaia presenta una distribución más diversificada, con una mayor representación de códigos asociados a precipitaciones y fenómenos invernales, particularmente lluvia ligera (código 7), aguanieve intensa (código 13) y nevadas ligeras (código 14).

En un analisis comparativo , los resultados indican que Río Grande se caracteriza por una mayor concentración de observaciones en condiciones nubladas y de niebla, mientras que Ushuaia registra una mayor variedad de fenómenos asociados a la precipitación. Estas diferencias reflejan las particularidades climáticas de cada ciudad  y permiten identificar patrones meteorológicos distintivos a lo largo de los distintos sectores de la Ruta Nacional 3 en Tierra del Fuego.

<img width="1390" height="490" alt="image" src="https://github.com/user-attachments/assets/a56c5bbe-4a8d-495f-956c-26076136ebc7" />


## Humedad relativa: Río Grande vs Ushuaia
El grafico de la humedad relativa deja en evidencia la diferencia leve que hay  entre las condiciones atmosféricas de Río Grande y Ushuaia. Río Grande presenta una tendencia hacia valores de humedad ligeramente más elevados y una mayor concentración de registros en rangos altos, lo que sugiere una atmósfera más cercana a condiciones favorables para la saturación del aire. Por su parte, Ushuaia exhibe una distribución algo más dispersa y una mediana levemente inferior, reflejando una mayor variabilidad en los niveles de humedad. Aunque ambas localidades mantienen condiciones generalmente húmedas, los resultados indican que Río Grande podría presentar una mayor predisposición a alcanzar estados de saturación atmosférica, especialmente cuando estos niveles de humedad se combinan con descensos de temperatura. 

<img width="676" height="451" alt="image" src="https://github.com/user-attachments/assets/b173305a-65b9-41a6-bb7c-48d1d012b40d" />


## Diferencia entre Temperatura y Dew Point
La distribución de la diferencia entre la temperatura del aire y el punto de rocío muestra que Río Grande presenta, en general, valores ligeramente más bajos y una mayor concentración de registros próximos a la saturación atmosférica en comparación con Ushuaia. Esto sugiere que las condiciones favorables para la formación de niebla podrían ocurrir con mayor frecuencia en Río Grande. Por su parte, Ushuaia exhibe una distribución algo más desplazada hacia diferencias mayores, indicando una menor proximidad entre la temperatura ambiente y el punto de rocío.

<img width="667" height="451" alt="image" src="https://github.com/user-attachments/assets/f3abc33c-cedd-4046-b3d0-3c1bbe9d4afb" />

## Punto de rocio: Rio Grande vs Ushuaia

El gráfico comparativo del punto de rocío nos muestra que, pese a las diferencias geográficas entre ambas ciudades, existe una similitud notable en las condiciones de humedad atmosférica y en la tendencia del aire a alcanzar la saturación. Ushuaia presenta una mediana ligeramente más elevada y una mayor presencia de valores atípicos bajos, lo que sugiere episodios ocasionales de ingreso de aire más frío y seco provenientes de zonas montañosas, reduciendo temporalmente las probabilidades de condensación. En cambio, Río Grande muestra una distribución más uniforme y una concentración de datos dentro de valores positivos. Este comportamiento refleja una disponibilidad de humedad relativamente constante que, combinada con el enfriamiento radiativo característico de la estepa fueguina, favorece la estabilidad del punto de rocío y aumenta la ocurrencia de fenómenos que afectan la visibilidad, especialmente en el sector norte de la Ruta Nacional 3.

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

