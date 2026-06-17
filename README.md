# Modelo Predictivo Ruta Nacional N°3
### Autor: LARA, Giovanna Estefania 
> Estudiante de Ciencia de Datos e IA
Politécnico Malvinas Argentinas, Tierra del Fuego, Argentina 🇦🇷

## Descripción del Proyecto

Este proyecto tiene como objetivo desarrollar un modelo de Aprendizaje Automático capaz de predecir condiciones de riesgo vial asociadas a la baja visibilidad en la Ruta Nacional N.º 3 de Tierra del Fuego. Utilizando datos meteorológicos históricos, se busca identificar situaciones que favorezcan la formación de niebla y otros fenómenos que dificultan la conducción, contribuyendo así a la generación de alertas tempranas para mejorar la seguridad vial.

## Objetivo General
Desarrollar un modelo de Aprendizaje Automático supervisado, utilizando la librería scikit-learn, que permita clasificar de manera temprana condiciones de riesgo vial por pérdida crítica de visibilidad en la Ruta Nacional N.º 3 a partir de variables meteorológicas locales, con el objetivo de emitir alertas tempranas sobre posibles escenarios de baja visibilidad y peligro para la circulación. 

## Origen e Integración del Dataset

Los datos meteorológicos utilizados en este proyecto fueron obtenidos de la plataforma Meteostat e incluyen registros históricos de las estaciones meteorológicas de Ushuaia y Río Grande correspondientes al período enero de 2023 - abril de 2026.

Debido a limitaciones en la descarga de grandes volúmenes de información, los datos fueron obtenidos en archivos semanales para garantizar la disponibilidad de todas las variables necesarias, especialmente la condición climática (Coco).

Posteriormente, los archivos de cada ciudad fueron integrados y consolidados en un único dataset, alineando los registros por fecha y hora. El conjunto de datos final fue almacenado en formato Excel (.xlsx) para su procesamiento y análisis en Python.

Los archivos originales descargados se encuentran disponibles en la carpeta **data/raw**, mientras que el dataset consolidado y listo para su utilización se encuentra en **data/processed**. Ambos pueden ser consultados y descargados desde este repositorio.

●​ link dataset Rio Grande: https://meteostat.net/es/station/87934?t=

●​ link dataset Ushuaia: https://meteostat.net/es/station/87938?t=

### Variables utilizadas

- Temperatura
- Punto de rocío
- Humedad relativa
- Precipitaciones
- Presión atmosférica
- Dirección del viento
- Velocidad del viento
- Ráfagas máximas
- Condición meteorológica (COCO)

##  Tecnologías Utilizadas
- [x] Python
- [x] Pandas
- [x] NumPy
- [x] Matplotlib
- [x] Seaborn
- [x] Scikit-Learn
- [x] Meteostat

##  Modelo de Machine Learning

### Algoritmo seleccionado

Se utilizó un modelo de **Random Forest Classifier** debido a:

- Su capacidad para modelar relaciones no lineales.
- Su robustez frente a ruido y valores atípicos.
- Su buen desempeño en problemas de clasificación multiclase.

### Variable objetivo

Se construyó una variable denominada:

**target_visibilidad**

Con tres niveles de riesgo:

| Clase | Nivel de Riesgo |
|---------|----------------|
| 1 | Riesgo Bajo |
| 2 | Riesgo Moderado |
| 3 | Riesgo Crítico |

## 📈 Resultados



<img width="460" height="244" alt="image" src="https://github.com/user-attachments/assets/4561f5d1-9a4a-4f35-9e5d-41c11461953f" />

<img width="661" height="490" alt="image" src="https://github.com/user-attachments/assets/f51d9a7c-a09b-4511-aeae-53b83a9d872f" />

### Hallazgos destacados

- Excelente desempeño en Riesgo Bajo y Moderado.
- Buena capacidad de detección de eventos críticos.
- El modelo identifica correctamente el 80 % de los casos de Riesgo Crítico.
- El desbalance de clases afecta principalmente la precisión de la categoría crítica.

# Video 
En este video se explica el desarrollo completo del proyecto, desde la obtención y análisis de los datos meteorológicos hasta la construcción y evaluación del modelo Random Forest utilizado para predecir niveles de riesgo vial en la Ruta Nacional N.º 3.

https://drive.google.com/file/d/1ELO-cNZWddyH089FkBOnyDm9IvpkHCJR/view?usp=sharing

Project Organization
------------

    ├── LICENSE
    ├── Makefile          
    ├── README.md          <- Documentación inicial del proyecto
    ├── data
    │   ├── interim        <- data set de la ciudades individuales
    │   ├── processed      <- dataset final 
    │   └── raw            <- datasets originales (semanales, archivos zip)
    │
    ├── docs               <-documentacion referida al proyecto 
    │
    ├── models             
    │
    ├── notebooks          <- Jupyter notebooks. (analisis exploratorio, Modelo predrictivo de seguridad vial y visibilidad la RN3)
    │                         
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- PowerPoint del proyecto
    │   └── figures        <- Graficos 
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── video              <- video exxplicativo del modelo predictivo  
    ├── setup.py          
    ├── src               
    │   ├── __init__.py    
    │   │
    │   ├── data         
    │   │   └── make_dataset.py
    │   │
    │   ├── features       
    │   │   └── build_features.py
    │   │
    │   ├── models       
    │   │   │                
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  
    │       └── visualize.py
    │
    └── tox.ini           


--------

## Mejoras Futuras

- Incorporar datos meteorológicos de Tolhuin.
- Incluir variables de visibilidad observada.
- Incorporar información del estado de la calzada.
- Integrar datos de tránsito vehicular.
- Implementar un sistema de alertas en tiempo real.
## Licencia
<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>



Este proyecto fue desarrollado con fines académicos y educativos.
