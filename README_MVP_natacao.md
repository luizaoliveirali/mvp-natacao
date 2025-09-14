# MVP — Classificação de Medalhistas em Natação Olímpica (1912–2020)

**Autora:** Luiza Oliveira Lima  
**Objetivo:** Prever se um(a) atleta conquistará medalha (ouro/prata/bronze) em provas olímpicas de natação.

## Como executar (Colab — recomendado)
1. Abra o Google Colab.
2. Faça upload do notebook `MVP_1_final.ipynb` ou abra direto do seu GitHub.
3. Execute **Todas as Células** (Runtime > Run all).  
   - O dataset é carregado via URL pública (RAW GitHub).

## Como executar localmente (Python 3.10+)
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -U pip
pip install numpy pandas scikit-learn xgboost matplotlib
jupyter notebook
```
Abra o arquivo `MVP_1_final.ipynb` e rode as células.

## Dataset
- **Fonte:** Olympic Swimming History 1912–2020 (público)
- **URL RAW:** https://raw.githubusercontent.com/datasciencedonut/Olympic-Swimming-History-1912-to-2020-/main/Olympic_Swimming.csv

## Pipeline (resumo)
- Engenharia: `Medalha` (Rank ≤ 3), `Distance_value` (inclui revezamentos 4x100 → 400).
- Pré-processamento: One‑Hot (`Stroke`, `Gender`, `Team`) + StandardScaler (numéricas).
- Modelos: Logistic Regression (baseline), Random Forest, XGBoost.
- Tuning: RandomizedSearchCV (CV=5).
- Decisão: **threshold = 0.40** (prioriza recall de medalhistas).
- Métricas: accuracy, precision/recall/F1 (classe 1), ROC‑AUC.

## Resultados (resumo)
- **Modelo final:** XGBoost + threshold 0.40.
- **Insights:** `Team` (país) é preditor dominante; `Relay?`, `Stroke`, `Distance_value` e `Year` também são relevantes.
- **Robustez:** retirar `Team` derruba as métricas; agrupar em Top‑N + OTHER melhora robustez, mas reduz performance.

## Estrutura do repositório sugerida
```
├─ MVP_1_final.ipynb        # Notebook final (entrega)
├─ README_MVP_natacao.md    # Este arquivo
└─ (opcional) figures/      # Imagens exportadas dos gráficos
```

## Licença
Uso acadêmico/educacional. Cite as fontes do dataset.
