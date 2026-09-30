# Dataset

`dataset_clinico_simulado_200.csv` contiene **200 notas clínicas simuladas** utilizadas en la evaluación académica del Módulo 8 de la Especialización en Machine Learning (IT Academy / Kibernum).

## Columnas

- `texto_clinico`: nota clínica sintética.
- `edad`: edad simulada.
- `genero`: género simulado (F/M).
- `afeccion`: afección asociada.
- `gravedad`: etiqueta objetivo (`leve`, `moderado`, `severo`).

## Advertencias metodológicas

Este corpus es **sintético** y pequeño. No contiene historias clínicas reales ni datos identificatorios de pacientes. El análisis del proyecto demuestra que existen plantillas lingüísticas repetidas y variables que actúan como proxies muy fuertes de la etiqueta, por lo que los resultados obtenidos con particiones aleatorias pueden sobreestimar la generalización.

La versión profesionalizada del notebook audita explícitamente estos shortcuts y utiliza una evaluación con familias de plantillas no vistas.

## Reutilización

El archivo proviene del material complementario utilizado para la evaluación académica. La licencia MIT del código del repositorio **no debe interpretarse automáticamente como licencia del dataset**.
