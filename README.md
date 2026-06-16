# Modelo Predictivo RN3
==============================

## Descripción del Proyecto

Este proyecto tiene como objetivo desarrollar un modelo de Aprendizaje Automático capaz de predecir condiciones de riesgo vial asociadas a la baja visibilidad en la Ruta Nacional N.º 3 de Tierra del Fuego. Utilizando datos meteorológicos históricos, se busca identificar situaciones que favorezcan la formación de niebla y otros fenómenos que dificultan la conducción, contribuyendo así a la generación de alertas tempranas para mejorar la seguridad vial.

## Objetivo General
Desarrollar un modelo de Aprendizaje Automático supervisado, utilizando la librería scikit-learn, que permita clasificar de manera temprana condiciones de riesgo vial por pérdida crítica de visibilidad en la Ruta Nacional N.º 3 a partir de variables meteorológicas locales, con el objetivo de emitir alertas tempranas sobre posibles escenarios de baja visibilidad y peligro para la circulación. 

## Origen e Integración del Dataset

Los datos meteorológicos utilizados en este proyecto fueron obtenidos de la plataforma Meteostat e incluyen registros históricos de las estaciones meteorológicas de Ushuaia y Río Grande correspondientes al período enero de 2023 - abril de 2026.

Debido a limitaciones en la descarga de grandes volúmenes de información, los datos fueron obtenidos en archivos semanales para garantizar la disponibilidad de todas las variables necesarias, especialmente la condición climática (Coco).

Posteriormente, los archivos de cada ciudad fueron integrados y consolidados en un único dataset, alineando los registros por fecha y hora. El conjunto de datos final fue almacenado en formato Excel (.xlsx) para su procesamiento y análisis en Python.

Los archivos originales descargados se encuentran disponibles en la carpeta **data/raw**, mientras que el dataset consolidado y listo para su utilización se encuentra en **data/processed**. Ambos pueden ser consultados y descargados desde este repositorio.



Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
