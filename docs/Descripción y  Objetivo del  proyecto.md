
## Modelo Predictivo de Visibilidad y Seguridad Vial en la RN3

## Entrega 1: Descripción y Formulación del Objetivo

## Aprendizaje Automático

## Alumno; LARA, Giovanna Estefania

link Github; https://github.com/gi0lara/modelo_predictivo_rn3.git



## Introducción

La Ruta Nacional N.º 3 es la principal conexión terrestre dentro de la Isla Grande de Tierra del Fuego y resulta fundamental para unir ciudades, transportar mercadería y permitir el traslado diario de muchas personas. Sin embargo, quienes transitamos habitualmente esta ruta sabemos que las condiciones climáticas representan un problema constante, especialmente en sectores como el Paso Garibaldi, donde el relieve montañoso y el clima fueguino generan situaciones muy peligrosas para conducir.

En muchas ocasiones, al trasladarme dentro de la isla, pude observar cómo la niebla densa, la niebla de hielo y el viento blanco reducen la visibilidad de forma repentina, convirtiendo la conducción en una situación de alto riesgo. En cuestión de minutos, la ruta puede quedar cubierta por una especie de “pared” de niebla o nieve en suspensión que dificulta la orientación de los conductores y aumenta     considerablemente las probabilidades de accidentes. Esta problemática se vio reflejada en los últimos años con numerosos despistes y situaciones de emergencia en distintos sectores de la Ruta Nacional N.º 3, involucrando vehículos particulares, camiones y transportes de pasajeros afectados por las condiciones climáticas adversas.

 A partir de esta problemática surge la importancia de este proyecto, que busca utilizar datos meteorológicos históricos para desarrollar una herramienta predictiva capaz de anticipar escenarios de baja visibilidad. Contar con un modelo de este tipo permitiría mejorar la toma de decisiones sobre la transitabilidad de la ruta, emitir alertas tempranas y contribuir a una mayor seguridad para todas las personas que circulan por este corredor tan importante de la provincia.



## Objetivos

### Objetivo General 

Desarrollar un modelo de Aprendizaje Automático supervisado, utilizando la librería scikit-learn, que permita clasificar de manera temprana condiciones de riesgo vial por pérdida crítica de visibilidad en la Ruta Nacional N.º 3 a partir de variables meteorológicas locales, con el objetivo de emitir alertas tempranas sobre posibles escenarios de baja visibilidad y peligro para la circulación.


## Objetivos Específicos


●​ Analizar la relación de dependencia y correlación entre la temperatura del aire, la humedad relativa y la temperatura del punto de rocío (dew point) para modelar matemáticamente la saturación del aire que genera la niebla.

●​ Estructurar y preprocesar un conjunto de datos histórico de dominio público, tratando los valores nulos mediante la columna de condición climática (Coco) para construir una variable objetivo robusta.

●​ Entrenar y evaluar algoritmos de clasificación aprendidos en el curso, seleccionando aquel que minimice los falsos negativos en la Matriz de Confusión mediante el análisis riguroso de las métricas de Precisión, Recall (Sensibilidad) y F1-Score.



## Definición de problema

El problema planteado corresponde a un problema de clasificación, ya que el objetivo del modelo es identificar y asignar cada situación meteorológica a una categoría determinada según el nivel de riesgo vial presente en la Ruta Nacional N.º 3.


 El modelo trabajará con tres clases previamente definidas asociadas a diferentes niveles de riesgo por pérdida de visibilidad y transitabilidad. El algoritmo será entrenado utilizando datos meteorológicos históricos etiquetados, permitiendo reconocer patrones climáticos capaces de anticipar escenarios específicos para la circulación. Para ello, la variable objetivo (target) se construirá utilizando el Código de Condición Climática (coco) proporcionado por el dataset, agrupando las observaciones en tres categorías principales:


●​ Clase 1 (Riesgo Bajo / Visibilidad Óptima): representa escenarios meteorológicos donde la visibilidad es adecuada y superior a 10 km, no existiendo un riesgo para la seguridad vial. Incluye condiciones de cielo despejado, buen tiempo o nubosidad estándar en general (códigos de coco bajos como 1, 2 o 3).

●​ Clase 2 (Riesgo Moderado / Visibilidad Reducida): registra situaciones intermedias donde la visibilidad se encuentra parcialmente comprometida (entre 1 km y 10 km) debido a fenómenos de menor intensidad como lluvias moderadas o neblinas ligeras.

●​ Clase 3 (Riesgo Crítico / Peligro Extremo): incluye escenarios severos donde la visibilidad se encuentra críticamente comprometida, generalmente por debajo de los 500 metros. Esta categoría contempla eventos extremos característicos de la isla como niebla densa (Código 7), niebla de hielo (Código 8) o episodios de nevadas intensas combinadas con fuertes ráfagas de viento (viento blanco).



## Posibles modelos

Debido a que el problema planteado corresponde a una clasificación supervisada, podrían utilizarse distintos modelos de clasificación para predecir situaciones de riesgo vial asociadas a la pérdida de visibilidad en la Ruta Nacional N.º 3 a partir de variables meteorológicas. Entre los principales modelos que podrían implementarse se encuentran:


●​ Regresión Logística: podría utilizarse como modelo base, ya que permite analizar la relación entre las variables meteorológicas y las clases de riesgo mediante una frontera de decisión lineal.

●​ Árboles de Decisión: este modelo podría emplearse para identificar relaciones no lineales entre variables como humedad, temperatura, viento o precipitaciones, además de permitir una interpretación clara de las decisiones tomadas por el algoritmo.

●​ Random Forest: también podría utilizarse debido a su capacidad para combinar múltiples árboles de decisión y mejorar la precisión de las predicciones, reduciendo el riesgo de sobreajuste y adaptándose mejor a la complejidad de las condiciones climáticas de la región.



