## Modelo Predictivo de Visibilidad y Seguridad Vial en la RN3

## Entrega 3: Presentación del Modelo y Análisis de Resultados

## Aprendizaje Automático

## Alumno; LARA, Giovanna Estefania

link Github; https://github.com/gi0lara/modelo_predictivo_rn3.git


## Introducción

## Descripción del problema
Este proyecto tiene como objetivo desarrollar un modelo de Aprendizaje Automático capaz de predecir condiciones de riesgo vial asociadas a la baja visibilidad en la Ruta Nacional N.º 3 de Tierra del Fuego. Utilizando datos meteorológicos históricos, se busca identificar situaciones que favorezcan la formación de niebla y otros fenómenos que dificultan la conducción, contribuyendo así a la generación de alertas tempranas para mejorar la seguridad vial.

## Objetivo General
Desarrollar un modelo de Aprendizaje Automático supervisado, utilizando la librería scikit-learn, que permita clasificar de manera temprana condiciones de riesgo vial por pérdida crítica de visibilidad en la Ruta Nacional N.º 3 a partir de variables meteorológicas locales, con el objetivo de emitir alertas tempranas sobre posibles escenarios de baja visibilidad y peligro para la circulación.



## Origen del dataset

Los datos meteorológicos utilizados en este proyecto fueron obtenidos de la plataforma Meteostat e incluyen registros históricos de las estaciones meteorológicas de Ushuaia y Río Grande correspondientes al período enero de 2023 - abril de 2026.
Debido a limitaciones en la descarga de grandes volúmenes de información, los datos fueron obtenidos en archivos semanales para garantizar la disponibilidad de todas las variables necesarias, especialmente la condición climática (Coco).
Posteriormente, los archivos de cada ciudad fueron integrados y consolidados en un único dataset, alineando los registros por fecha y hora. El conjunto de datos final fue almacenado en formato Excel (.xlsx) para su procesamiento y análisis en Python.
Los archivos originales descargados se encuentran disponibles en la carpeta data/raw, mientras que el dataset consolidado y listo para su utilización se encuentra en data/processed. Ambos pueden ser consultados y descargados desde este repositorio.

●​ link dataset Rio Grande: https://meteostat.net/es/station/87934?t=2026-05-19/2026-05-26


●​ link dataset Ushuaia: https://meteostat.net/es/station/87938?t=2026-05-19/2026-05-26


## Análisis exploratorio (conclusiones de análisis)

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

## Conclusiones del análisis 

El análisis exploratorio permitió identificar diferencias climáticas relevantes entre ambas ciudades. Río Grande presentó una mayor variabilidad térmica, niveles de humedad ligeramente superiores y una mayor frecuencia de eventos extremos, especialmente niebla y niebla helada. Ushuaia, en cambio, mostró un comportamiento más estable desde el punto de vista térmico y una mayor presencia de fenómenos asociados a precipitaciones y nevadas. Estas características resultan especialmente importantes para comprender cómo las condiciones meteorológicas pueden variar a lo largo de la provincia y afectar de manera diferente a la circulación vehicular.
Las matrices de correlación evidenciaron relaciones significativas entre variables como temperatura, humedad relativa y punto de rocío, confirmando patrones atmosféricos coherentes con la climatología fueguina. Asimismo, el análisis de la diferencia entre temperatura y punto de rocío permitió detectar una mayor predisposición a la formación de niebla en Río Grande, un fenómeno directamente relacionado con la reducción de visibilidad en rutas.
En conjunto, los resultados del análisis exploratorio permitieron comprender el comportamiento meteorológico de ambas localidades, identificar variables relevantes para el modelado predictivo y validar la calidad del dataset construido. 

## Modelo de aprendizaje automático

Descripción del Modelo de Aprendizaje Automático
Para el desarrollo del modelo predictivo de visibilidad y seguridad vial en la Ruta Nacional N.º 3 se utilizó un algoritmo de aprendizaje supervisado basado en Random Forest, una técnica de ensamble que combina múltiples árboles de decisión para mejorar la capacidad predictiva y reducir el riesgo de sobreajuste. Este modelo fue seleccionado debido a su buen desempeño en problemas de clasificación, su capacidad para manejar relaciones no lineales entre variables y su robustez frente a datos con valores atípicos o distribuciones complejas, características frecuentes en los fenómenos meteorológicos.
La construcción del modelo comenzó con la generación de una variable objetivo denominada target_visibilidad, diseñada para representar distintos niveles de riesgo vial asociados a las condiciones climáticas. Esta variable fue creada a partir de los códigos meteorológicos (coco) registrados en las ciudades de Río Grande y Ushuaia. Se definieron tres categorías de clasificación:

Clase 0( Riesgo Bajo)
Corresponde a situaciones meteorológicas con buena visibilidad y sin fenómenos que representen un riesgo para la circulación.
Códigos coco: [1, 2, 3, 4]
1: Despejado (Clear)
2: Parcialmente nublado o buen tiempo (Fair)
3: Nublado (Cloudy)
4: Cubierto (Overcast)

Clase 1(Riesgo Moderado)
Incluye fenómenos meteorológicos que reducen la visibilidad, pero que generalmente no representan condiciones extremas para la seguridad vial.
Códigos coco: [7, 8, 9, 14, 15, 17, 18]
7: Lluvia ligera (Light Rain)
8: Lluvia (Rain)
9: Lluvia intensa (Heavy Rain)
14: Nevada ligera (Light Snowfall)
15: Nevada (Snowfall)
17: Chubasco de lluvia (Rain Shower)
18: Chubasco intenso de lluvia (Heavy Rain Shower)

Clase 2 ( Riesgo Crítico)comprende fenómenos meteorológicos severos que pueden afectar gravemente la visibilidad y la seguridad vial, requiriendo una alerta temprana.
Códigos coco: [5, 6, 16, 22, 23, 24, 25, 26, 27]
5: Niebla (Fog)
6: Niebla helada (Freezing Fog)
16: Nevada intensa (Heavy Snowfall)
22: Chubasco intenso de nieve (Heavy Snow Shower)
23: Descargas eléctricas (Lightning)
24: Granizo (Hail)
25: Tormenta eléctrica (Thunderstorm)
26: Tormenta eléctrica intensa (Heavy Thunderstorm)
27: Tormenta (Storm)


Como variables predictoras se seleccionaron doce indicadores meteorológicos correspondientes a temperatura, punto de rocío, humedad relativa, precipitaciones, velocidad del viento y presión atmosférica registradas tanto en Río Grande como en Ushuaia. Estas variables fueron elegidas debido a su influencia directa sobre la formación de fenómenos que afectan la visibilidad y las condiciones de seguridad vial. Antes del entrenamiento, los valores faltantes fueron reemplazados utilizando la mediana de cada variable, permitiendo mantener la totalidad de las observaciones sin introducir sesgos significativos.
Para entrenar y evaluar el modelo, el conjunto de datos se dividió en dos subconjuntos mediante la función train_test_split de Scikit-Learn. El 80 % de las observaciones se destinó al entrenamiento y el 20 % restante a la evaluación. Además, se aplicó una partición estratificada (stratify = y) para conservar la proporción original de cada clase en ambos conjuntos, aspecto especialmente importante debido al desbalance existente entre las categorías de riesgo.
La arquitectura del modelo se basó en un bosque de 200 árboles de decisión (n_estimators = 200), permitiendo que cada árbol aprendiera diferentes patrones presentes en los datos y que la predicción final surgiera de la combinación de todas sus decisiones. Para evitar árboles excesivamente complejos y mejorar la capacidad de generalización, se estableció una profundidad máxima de 10 niveles (max_depth = 10). Asimismo, se utilizó el parámetro class_weight = 'balanced', que ajusta automáticamente el peso de cada clase en función de su frecuencia dentro del conjunto de entrenamiento. Esta configuración resulta especialmente útil porque la categoría Riesgo Crítico posee una cantidad considerablemente menor de observaciones respecto de las demás clases.
Finalmente, se fijó un random_state = 42 para garantizar la reproducibilidad de los resultados. Una vez entrenado, el modelo fue evaluado mediante métricas de clasificación como Accuracy, Precision, Recall y F1-Score, complementadas por un Classification Report y una matriz de confusión, herramientas que permitieron analizar en detalle el desempeño del modelo para cada categoría de riesgo. Los resultados obtenidos mostraron un desempeño satisfactorio, alcanzando una precisión  cercana al 80 % y una capacidad destacable para identificar situaciones de riesgo crítico, lo que demuestra el potencial del modelo como herramienta de apoyo para la predicción de condiciones meteorológicas adversas y la mejora de la seguridad vial en la Ruta Nacional N.º 3.


## Evaluación del modelo

El modelo obtuvo una Accuracy del 79,94%, las categorías Riesgo Bajo y Riesgo Moderado presentaron un desempeño sólido, con valores de F1-Score de 0,83 y 0,81 respectivamente, reflejando una buena capacidad de clasificación. Por otro lado, la categoría Riesgo Crítico mostró un comportamiento diferente. Si bien alcanzó un recall de 0,80, lo que significa que logró identificar el 80% de los casos críticos reales, su precisión fue de 0,34, indicando que una parte importante de los casos predichos como críticos pertenecían en realidad a otras categorías. Como resultado, el F1-Score para esta clase fue de 0,48, considerablemente menor al de las demás categorías. Este comportamiento puede estar relacionado con el desbalance presente en el conjunto de datos, ya que la clase Riesgo Crítico cuenta con solo 230 observaciones, frente a las 3358 de Riesgo Bajo y las 2249 de Riesgo Moderado. En términos generales, el modelo presenta un rendimiento satisfactorio, especialmente en las categorías de Riesgo Bajo y Moderado, manteniendo además una buena capacidad para detectar los casos críticos. 
<img width="460" height="244" alt="image" src="https://github.com/user-attachments/assets/513e3eb5-78df-4347-ad0d-9edfbcaf6025" />




La matriz de confusión obtenida deja en evidencia un desempeño satisfactorio en la tarea de clasificación, ya que la mayor parte de las predicciones se concentra sobre la diagonal principal, lo que representa clasificaciones correctas. Para la categoría Bajo, el modelo clasificó correctamente 2696 observaciones, aunque registró algunas confusiones con las categorías Moderado (343 casos) y Crítico (319 casos). En la categoría Moderado, se identificaron correctamente 1785 registros, mientras que 427 fueron clasificados como Bajo y 37 como Crítico. Respecto a la categoría Crítico, que presenta una menor cantidad de observaciones dentro del conjunto de datos, el modelo logró clasificar correctamente 185 casos, con errores reducidos hacia las categorías Bajo (36 casos) y Moderado (9 casos).
Considerando las métricas obtenidas, el modelo Random Forest alcanzó una precisión cercana al 80 %, lo que refleja un desempeño adecuado para el problema planteado. La elevada cantidad de aciertos observada en la matriz de confusión confirma su capacidad para identificar correctamente los distintos niveles de riesgo analizados. Asimismo, el buen comportamiento alcanzado en la categoría Crítico, pese a contar con una menor representación en los datos, demuestra la robustez del modelo frente al desbalance de clases. En consecuencia, Random Forest se presenta como una alternativa eficaz y confiable para la clasificación de los niveles de visibilidad y seguridad vial en la Ruta Nacional N.º 3.

<img width="661" height="490" alt="image" src="https://github.com/user-attachments/assets/66181575-f292-4eaf-8910-fb8d084a3cfa" />

## Conclusiones


En conclusión, este  proyecto permitió desarrollar y evaluar un modelo de aprendizaje automático orientado a la predicción de condiciones de riesgo vial asociadas a la pérdida de visibilidad en la Ruta Nacional N.º 3 de Tierra del Fuego. A partir del análisis de registros meteorológicos históricos de las ciudades de Río Grande y Ushuaia, fue posible identificar patrones climáticos relevantes relacionados con la formación de niebla, precipitaciones y otros fenómenos que afectan la seguridad de la circulación.
Los resultados obtenidos demuestran que el modelo Random Forest alcanzó un desempeño satisfactorio, con una precisión general cercana al 80 %, logrando una adecuada clasificación de los niveles de riesgo definidos. Además, mostró una capacidad destacable para detectar situaciones de Riesgo Crítico(Clase2), alcanzando un recall del 80 % para esta categoría, aspecto especialmente importante en aplicaciones de seguridad vial donde resulta prioritario minimizar la omisión de eventos potencialmente peligrosos.
El análisis exploratorio permitió confirmar diferencias meteorológicas significativas entre Río Grande y Ushuaia, destacándose una mayor frecuencia de niebla y eventos extremos en Río Grande, mientras que Ushuaia presentó una mayor presencia de precipitaciones y fenómenos invernales. Estas diferencias aportaron información valiosa para la construcción del modelo y evidenciaron la importancia de considerar datos de distintas zonas de la provincia para comprender mejor las condiciones atmosféricas que afectan la visibilidad.
Sin embargo, el proyecto presenta algunas limitaciones. La principal está relacionada con el desbalance de clases existente en el conjunto de datos, ya que los eventos clasificados como Riesgo Crítico(Clase 3) poseen una representación considerablemente menor respecto de las demás categorías. Asimismo, el modelo se basa únicamente en información meteorológica proveniente de dos estaciones ubicadas en los extremos de la provincia, lo que limita la representación de las condiciones presentes en los sectores intermedios de la Ruta Nacional N.º 3.
Como línea de mejora futura,propongo poder ampliar el dataset incorporando datos meteorológicos correspondientes a la ciudad de Tolhuin, lo que permitiría incluir información representativa de la zona central de la provincia y mejorar la caracterización de las condiciones climáticas a lo largo de todo el corredor vial. También sería conveniente incorporar nuevas variables, como datos de visibilidad observada, estado de la calzada, tránsito vehicular o información satelital, que puedan ampliar el proyecto a no solo la visibilidad, sino también a la seguridad vial en general del estado de la ruta.


## Video explicativo

link al video expositivo del proyecto de Aprendizaje Automatico:  Modelo Predictivo de Visibilidad y Seguridad Vial en la RN3

[https://drive.google.com/file/d/1ELO-cNZWddyH089FkBOnyDm9IvpkHCJR/view?usp=sharing](https://drive.google.com/file/d/1ELO-cNZWddyH089FkBOnyDm9IvpkHCJR/view?usp=sharing)https://drive.google.com/file/d/1ELO-cNZWddyH089FkBOnyDm9IvpkHCJR/view?usp=sharing
