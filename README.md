# Crop Recommendation — Mineração de Dados

Projeto de classificação que recomenda a cultura agrícola mais adequada com base em atributos de solo e clima, comparando três algoritmos de aprendizado de máquina.

**Dataset:** [Crop Recommendation Dataset — Kaggle](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset) · 2 200 amostras · 22 culturas · 7 atributos

---

## Resultados

| Modelo | Acurácia | Precisão (W) | Recall (W) | F1 (W) |
|---|---|---|---|---|
| Decision Tree (depth=8) | 87,05% | 85,73% | 87,05% | 85,21% |
| KNN (k=3) | 98,18% | 98,25% | 98,18% | 98,17% |
| **Random Forest** | **99,32%** | **99,33%** | **99,32%** | **99,32%** |

Validação cruzada (5-fold estratificado) confirmou a robustez do Random Forest sem sinais de overfitting.

---

## Atributos do dataset

| Coluna | Descrição | Unidade |
|---|---|---|
| `N` | Nitrogênio no solo | mg/kg |
| `P` | Fósforo no solo | mg/kg |
| `K` | Potássio no solo | mg/kg |
| `temperature` | Temperatura média | °C |
| `humidity` | Umidade relativa | % |
| `ph` | pH do solo | — |
| `rainfall` | Precipitação anual | mm |
| `label` | Cultura recomendada | — |

---

## Pipeline

```
Dataset (CSV)
    └─ EDA: distribuição de classes, histogramas, correlação, boxplots
    └─ Pré-processamento: detecção de outliers (IQR), clipping, LabelEncoder, StandardScaler
    └─ Modelos: Decision Tree · Random Forest · KNN
    └─ Avaliação: accuracy, precision, recall, F1, matriz de confusão, validação cruzada
    └─ Visualização: superfície de decisão via PCA 2D, importância dos atributos
```

---

## Como executar

### 1. Clone o repositório
```bash
git clone https://github.com/jota6k/crop-recommendation.git
cd crop-recommendation
```

### 2. Instale as dependências
```bash
pip install -r requirements.txt
```

### 3. Baixe o dataset
Acesse [kaggle.com/datasets/atharvaingle/crop-recommendation-dataset](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset), baixe o arquivo `Crop_recommendation.csv` e coloque-o na pasta `data/`.

### 4. Execute o notebook
```bash
jupyter notebook crop_recommendation.ipynb
```

---

## Tecnologias

Python · Pandas · NumPy · Scikit-learn · Matplotlib · Seaborn

---

## Principais conclusões

- O dataset é **perfeitamente balanceado** (100 amostras por classe), o que elimina viés na avaliação.
- Os atributos mais discriminativos no Random Forest são **rainfall**, **humidity** e **K** (potássio).
- O **KNN** exige padronização dos dados — sem `StandardScaler` a acurácia cai significativamente.
- A superfície de decisão via PCA captura apenas 43% da variância total, o que explica as sobreposições visuais mesmo com alta acurácia no espaço original.
