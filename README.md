# Clasificación de Notas Clínicas con BETO

Proyecto de **NLP en español** sobre notas clínicas **simuladas**, profesionalizado con foco en validación robusta, detección de shortcuts, explicabilidad y análisis ético.

[![Notebook CI](https://github.com/Koke-Oliva/nlp-notas-clinicas-bert/actions/workflows/notebook-ci.yml/badge.svg?branch=main)](https://github.com/Koke-Oliva/nlp-notas-clinicas-bert/actions/workflows/notebook-ci.yml)
[![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Transformers](https://img.shields.io/badge/Hugging%20Face-Transformers-FFD21E)](https://huggingface.co/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Koke-Oliva/nlp-notas-clinicas-bert/blob/main/nlp-notas-clinicas-bert.ipynb)
[![nbviewer](https://img.shields.io/badge/nbviewer-open-orange)](https://nbviewer.org/github/Koke-Oliva/nlp-notas-clinicas-bert/blob/main/nlp-notas-clinicas-bert.ipynb)

## Vista rápida

- **Problema:** clasificación multiclase de gravedad clínica simulada: `leve`, `moderado`, `severo`.
- **Modelos:** TF-IDF + Multinomial Naive Bayes, Word2Vec + Random Forest y BETO.
- **Hallazgo clave:** las métricas perfectas del experimento original estaban fuertemente favorecidas por textos repetidos, proxies del target y plantillas sintéticas.
- **Validación robusta:** comparación entre CV aleatoria y CV con **familias completas de plantillas no vistas**.
- **Ética y fairness:** género y edad se reservan para auditoría; no se usan como predictores principales.
- **Explicabilidad:** LIME sobre una predicción de BETO.
- **Reproducibilidad:** dataset, dependencias, notebook y GitHub Actions incluidos.

> **Proyecto demostrativo de portafolio.** El dataset es sintético y este repositorio no representa un sistema clínico ni debe utilizarse para decisiones sobre pacientes.

## Dataset

El repositorio incluye `data/dataset_clinico_simulado_200.csv`:

- 200 registros;
- 5 variables;
- 115 textos clínicos únicos;
- 85 filas repiten un texto ya observado;
- 3 clases de gravedad;
- edad y género simulados;
- afección asociada.

La auditoría detectó además dos riesgos de shortcut:

1. **Afección → gravedad:** las afecciones del corpus aparecen asociadas a una sola clase.
2. **Plantilla → gravedad:** se identifican nueve familias de redacción y cada familia está asociada a una sola clase.

En la reproducción del split aleatorio original, **23 de 40 textos del test (57,5%)** ya aparecen exactamente en entrenamiento.

## Por qué no se presenta el 100% como resultado principal

La entrega académica original obtuvo métricas perfectas con Word2Vec + Random Forest y BETO. En lugar de utilizar ese `1.00` como evidencia de generalización, la versión profesionalizada investiga por qué aparece.

El objetivo pasa de:

> “obtener la mayor accuracy”

a:

> **“medir cuánto del rendimiento proviene de patrones sintéticos y cuánto se sostiene ante estructuras lingüísticas no vistas”.**

## Metodología

1. EDA visual y control de calidad.
2. Auditoría de duplicados exactos.
3. Auditoría de `afeccion` como proxy del target.
4. Identificación de familias de plantillas.
5. Preprocesamiento con spaCy: tokenización, lematización y stopwords.
6. **TF-IDF + Multinomial Naive Bayes**.
7. **Word2Vec + Random Forest**.
8. **BETO** (`dccuchile/bert-base-spanish-wwm-uncased`).
9. CV aleatoria estratificada vs. tres folds agrupados por plantilla, con una familia completa de cada clase retenida por fold.
10. Holdout robusto compartido entre modelos.
11. Train / validation / test separados para BETO.
12. Matrices de confusión y curvas Precision–Recall.
13. Análisis de errores, con foco en falsos negativos de `severo`.
14. Auditoría por género y edad.
15. Explicabilidad local con LIME.
16. Comparación de desempeño y costo computacional.

### Prevención de leakage

- BETO ya **no utiliza el test como validation** para EarlyStopping.
- El test robusto contiene familias de plantillas que no aparecen en desarrollo.
- Train y validation de BETO se separan evitando textos exactamente repetidos entre ambos.
- Word2Vec se entrena desde cero dentro de cada fold.
- `afeccion`, género y edad no forman parte de las features de los modelos principales.

## Resultados

Las métricas definitivas de la versión profesionalizada se generan desde una ejecución completa del notebook y se incorporarán aquí únicamente después de validar el workflow. El notebook ejecutado es la fuente de verdad para evitar inconsistencias entre texto y resultados.

## Explicabilidad y análisis ético

LIME se aplica directamente a BETO para mostrar qué tokens favorecen una predicción individual. Si existen errores en el holdout robusto, se prioriza explicar uno de ellos.

El análisis por subgrupos reporta:

- soporte;
- F1 macro;
- recall de `severo`;
- falsos negativos de `severo`.

Dado que el corpus es sintético y pequeño, estas métricas **no permiten concluir ausencia o presencia de sesgo clínico real**.

## Estructura

```text
.
├── .github/
│   └── workflows/
│       └── notebook-ci.yml
├── data/
│   ├── README.md
│   └── dataset_clinico_simulado_200.csv
├── figures/
│   └── README.md
├── nlp-notas-clinicas-bert.ipynb
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Reproducibilidad

```bash
git clone https://github.com/Koke-Oliva/nlp-notas-clinicas-bert.git
cd nlp-notas-clinicas-bert

python -m venv .venv

# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1

pip install -r requirements.txt
python -m spacy download es_core_news_sm

jupyter notebook nlp-notas-clinicas-bert.ipynb
```

BETO descarga pesos públicos desde Hugging Face durante la ejecución.

## Limitaciones

- Solo 200 observaciones simuladas.
- Plantillas de texto y afecciones fuertemente asociadas a la etiqueta.
- La validación por plantillas es más exigente, pero no sustituye un corpus clínico externo.
- El análisis de subgrupos tiene poco soporte estadístico.
- LIME es una explicación local aproximada y no implica causalidad.
- Antes de una aplicación clínica real serían necesarios validación externa/temporal, revisión médica, privacidad, calibración, monitoreo y gobernanza.

## Contexto académico

Proyecto desarrollado inicialmente en el **Módulo 8 — Procesamiento del Lenguaje Natural** de la Especialización en Machine Learning de IT Academy / Kibernum. La versión actual conserva el objetivo formativo original y refuerza validación, reproducibilidad, explicabilidad y análisis crítico.
