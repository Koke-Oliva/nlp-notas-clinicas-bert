# 🧠 Clasificación de Notas Clínicas con BERT (NLP - Español)

Modelo de procesamiento de lenguaje natural aplicado a **notas clínicas médicas** en español, con enfoque en clasificación de severidad (*leve*, *moderado*, *severo*) usando **BERT**.  
El proyecto aborda limpieza textual, tokenización, fine-tuning y evaluación estratificada con foco en **sesgos**.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Koke-Oliva/nlp-notas-clinicas-bert/blob/main/nlp-notas-clinicas-bert.ipynb)

---

## 📋 Resumen

- **Objetivo:** Clasificar la severidad de notas clínicas médicas escritas en español.  
- **Dataset:** Conjunto de textos clínicos preprocesados y anonimizados.  
- **Modelo:** *BETO* (versión española de BERT), fine-tuning sobre capas finales.  
- **Evaluación:** Estratificada por clase y por grupos demográficos (edad/género).  
- **Métricas:** Accuracy, F1 (macro), Recall, ROC-AUC.  
- **Enfoque ético:** Identificación y mitigación de posibles sesgos de representación.  
- **Resultados:** F1 Macro ≈ **0.84**, buena capacidad general de clasificación, sesgos moderados detectados.

---

## ⚙️ Stack (PyData + Transformers)

**Frameworks y librerías principales:**
- 🐍 Python  
- 📓 Jupyter  
- 🤗 Transformers (Hugging Face)  
- 🔥 PyTorch  
- 🧩 Scikit-learn  
- 📊 Matplotlib / Seaborn / WordCloud

**Principales módulos usados:**
```python
from transformers import BertTokenizerFast, BertForSequenceClassification, Trainer, TrainingArguments
from sklearn.metrics import classification_report, confusion_matrix
from datasets import Dataset

```
---

## 🧩 Reproducibilidad

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/Koke-Oliva/nlp-notas-clinicas-bert.git
   cd nlp-notas-clinicas-bert
   ```
   ```bash
   pip install -r requirements.txt
   ``` 
   ```bash
   nlp-notas-clinicas-bert.ipynb
   ```



