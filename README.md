# 💳 Projeto de Detecção de Fraude em Cartões de Crédito

[![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)]()
[![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)](https://www.python.org/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conecte--se-blue?logo=linkedin)](https://www.linkedin.com/in/eltonjorgee)

---

## 🧠 Sobre o Projeto

Com o crescimento exponencial das transações financeiras digitais, a detecção de fraudes tornou-se uma área crítica para a segurança de instituições financeiras e clientes. Este projeto foi desenvolvido para construir um modelo de _machine learning_ capaz de identificar transações de cartão de crédito fraudulentas com alta precisão.

O desafio central deste projeto é lidar com um _dataset_ altamente desbalanceado, onde as fraudes representam apenas 0,17% do total de transações. O objetivo é criar um modelo que não apenas minimize as perdas financeiras, mas também garanta a confiança e a integridade do sistema financeiro.

> 🗂️ A análise preditiva é uma ferramenta essencial para criar sistemas de detecção proativos e eficientes. Este trabalho explora desde a análise exploratória e o pré-processamento de dados até a comparação de múltiplos algoritmos de classificação, avaliando-os tanto por métricas estatísticas quanto por seu impacto financeiro.

---

## 🗂️ Sumário

1.  📖 [Instalação e Importação de Bibliotecas](#bibliotecas)
2.  📌 [Extração de Dados](#extracao-de-dados)
3.  🧹 [Tratamento de Dados](#tratamento-de-dados)
4.  📈 [Análise Exploratória de Dados (EDA)](#analise-exploratoria)
5.  ⚙️ [Pré-processamento e Engenharia de Features](#pre-processamento)
6.  🤖 [Modelagem e Treinamento](#modelagem)
    * 📊 Avaliação de Desempenho dos Modelos
    * 💰 Análise de Impacto Financeiro
7.  📑 [Considerações Finais](#consideracoes-finais)

---

### <a id="bibliotecas"> 1. Instalação e Importação de Bibliotecas </a>

Nesta etapa, foram instalados e importados todos os pacotes necessários para manipulação(__Pandas__,__numpy__), visualização(__Seaborn__,__matplotlib__), análise estatística(__statsmodels__), modelagem dos dados(__imblearn__) e modelos de machine learning(__XGboost__ e __scikit-learn__).

### <a id="extracao-de-dados"> 2. Extração de Dados </a>

O _dataset_ utilizado foi o **Credit Card Fraud Detection** do Kaggle, contendo 284.807 transações. As _features_ `V1` a `V28` são componentes principais (PCA) para proteger a privacidade dos dados, enquanto `Time` e `Amount` são as únicas variáveis originais.

### <a id="tratamento-de-dados"> 3. Tratamento de Dados </a>

Foi realizada a verificação de dados nulos e duplicados. Os registros duplicados da classe majoritária (não fraude) foram removidos para limpar a base, enquanto os da classe minoritária (fraude) foram mantidos para preservar o máximo de informação sobre esses eventos raros.

### <a id="analise-exploratoria"> 4. Análise Exploratória de Dados (EDA) </a>

A EDA revelou o forte desbalanceamento do _dataset_: apenas **0,17%** das transações são fraudulentas. A análise mostrou que as fraudes tendem a se concentrar em horários específicos e em faixas de valores mais baixas, embora o risco relativo também aumente para transações de valores muito altos.

### <a id="pre-processamento"> 5. Pré-processamento e Engenharia de Features </a>

* **Engenharia de Features:** Foram criadas novas colunas, como `Hour` e `Day_of_week`, a partir da variável `Time` para capturar padrões temporais.
* **Escalonamento:** A variável `Amount` foi normalizada utilizando `RobustScaler` para mitigar o efeito de _outliers_.
* **Balanceamento de Classes:** Foi aplicada a técnica **SMOTE (_Synthetic Minority Over-sampling Technique_)** para criar amostras sintéticas da classe minoritária, balanceando o _dataset_ de treino.

### <a id="modelagem"> 6. Modelagem e Treinamento </a>

Foram testados e comparados diversos algoritmos de classificação, incluindo:
* Regressão Logística
* Random Forest
* Gradient Boosting
* XGBoost
* Voting & Stacking Classifiers
* Isolation Forest (não supervisionado)

A avaliação dos modelos considerou métricas estatísticas (com foco em **PR-AUC**) e uma análise de impacto financeiro, simulando o custo de fraudes e o custo de verificação de falsos positivos.

<details>
<summary><b>Resultados dos Modelos</b></summary>

| Modelo                     | Acurácia | ROC AUC | PR AUC  | Precision | Recall | F1-Score |
|----------------------------|----------|---------|---------|-----------|--------|----------|
| Regressão Logística        | 0.9755   | 0.9741  | 0.7506  | 0.06      | 0.91   | 0.11     |
| Logistic Regression        | 0.9734   | 0.9669  | 0.7510  | 0.06      | 0.90   | 0.10     |
| Regressão Logística Otimizada | 0.9755 | 0.9741  | 0.7509  | 0.06      | 0.91   | 0.11     |
| Random Forest              | 0.9956   | 0.9709  | 0.6813  | 0.26      | 0.88   | 0.41     |
| Random Forest Otimizado    | 0.9978   | 0.9666  | 0.4640  | 0.43      | 0.87   | 0.57     |
| Gradient Boosting          | 0.9988   | 0.9511  | 0.8307  | 0.60      | 0.85   | 0.70     |
| XGBoost                    | 0.9988   | 0.9685  | 0.8648  | 0.61      | 0.88   | 0.72     |
| Voting Classifier          | 0.9985   | 0.9693  | 0.8561  | 0.54      | 0.87   | 0.67     |
| Stacking Classifier        | 0.9964   | 0.9698  | 0.7479  | 0.31      | 0.87   | 0.45     |
| Isolation Forest           | 0.9975   | 0.9421  | 0.1441  | 0.27      | 0.26   | 0.26     |

</details>


### <a id="consideracoes-finais"> 7. Considerações Finais </a>

O modelo **XGBoost** apresentou o melhor equilíbrio entre desempenho técnico e impacto financeiro, com um **PR-AUC de 0.9685** e um **ROI estimado de 4,6x**. Sua implementação pode gerar uma economia significativa, evitando perdas financeiras e fortalecendo a segurança das transações.

---

## 🛠️ Ferramentas Utilizadas

- [![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)](https://www.python.org/)
- [![Pandas](https://img.shields.io/badge/Pandas-Data%20Manipulation-%23150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
- [![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-%23F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
- [![Seaborn](https://img.shields.io/badge/Seaborn-Statistical-%2300CED1?logo=seaborn&logoColor=white)](https://seaborn.pydata.org/)
- [![Plotly](https://img.shields.io/badge/Plotly-Interactive-%2300498B?logo=plotly&logoColor=white)](https://plotly.com/python/)
- [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
- [![Quarto](https://img.shields.io/badge/Quarto-Reporting-%2300599C?logo=quarto&logoColor=white)](https://quarto.org/)

---

## 🤝 Conecte-se comigo

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conecte--se-blue?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/eltonjorgee)
[![Email](https://img.shields.io/badge/Email-eltonoliveirajorge@hotmail.com-red?style=flat&logo=gmail&logoColor=white)](mailto:eltonoliveirajorge@hotmail.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-+5521964523066-green?style=flat&logo=whatsapp&logoColor=white)](https://wa.me/5521964523066)
