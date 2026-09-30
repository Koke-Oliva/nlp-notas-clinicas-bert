# Dataset sintético

`dataset_clinico_simulado_200.csv` contiene 200 registros sintéticos usados en la evaluación formativa del Módulo 8.

Columnas:

- `texto_clinico`
- `edad`
- `genero`
- `afeccion`
- `gravedad`

## Uso en este repositorio

El archivo se publica para reproducibilidad del proyecto. No contiene nombres, identificadores personales ni historias clínicas reales.

La versión profesionalizada del análisis detecta que el dataset incluye:

- textos exactos repetidos;
- nueve familias de plantillas sintéticas;
- asociación determinista entre familia de plantilla y clase;
- asociación determinista entre `afeccion` y `gravedad`.

Por ese motivo, las métricas perfectas de una partición aleatoria no se interpretan como evidencia de generalización clínica.
