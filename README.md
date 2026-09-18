# 🚗 Etapa 1: ETL do Dataset (PRF)

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-ETL-150458.svg)
![PostgreSQL](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E.svg)
![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento-orange.svg)

## 📌 Visão Geral do Projeto

Este projeto consiste no desenvolvimento de uma pipeline de **ETL (Extract, Transform, Load)** aplicada à base histórica de acidentes em rodovias federais brasileiras, disponibilizada pela **Polícia Rodoviária Federal (PRF)**. Nesta etapa inicial, o foco foi voltado integralmente para a **Engenharia de Dados**, priorizando a qualidade, a integridade e a eficiência do processamento antes da realização de qualquer análise.

Ao longo da pipeline, foram implementadas diversas etapas de tratamento e padronização dos dados, garantindo uma base confiável e preparada para análises posteriores. Entre as principais atividades desenvolvidas, destacam-se:

* **Tratamento e sanitização dos dados:** correção de inconsistências, remoção de ruídos e padronização textual, incluindo a eliminação de acentos e caracteres especiais por meio da biblioteca `unicodedata`, reduzindo problemas de *encoding* e incompatibilidades entre sistemas.
* **Otimização de armazenamento e desempenho:** adequação dos tipos de dados utilizando técnicas de *downcasting* para colunas numéricas e categóricas, reduzindo significativamente o consumo de memória e aumentando a eficiência das operações de processamento e consulta.
* **Modelagem e integridade relacional:** padronização da nomenclatura das colunas, reorganização do esquema de dados e criação de uma chave primária sequencial, assegurando consistência e facilitando a integração com o **Supabase (PostgreSQL)**.

Como resultado, foi construída uma base de dados totalmente higienizada, padronizada e otimizada, pronta para suportar as próximas fases do projeto. As etapas seguintes contemplam a realização da **Análise Exploratória de Dados (EDA)**, com foco na investigação dos acidentes relacionados à **fadiga e ao sono**, **desatenção do condutor** e outros, permitindo extrair padrões, identificar fatores de risco e gerar insights que apoiem futuras análises e modelos preditivos.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **Linguagem:** Python
* **Manipulação e Tratamento:** Pandas, NumPy e unicodedata
*  **Ambiente de Desenvolvimento:** Jupyter Notebook

---

# 🧠 Etapa 2: Introdução de Machine Learning no Projeto

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange) ![imbalanced-learn](https://img.shields.io/badge/imbalanced--learn-SMOTE-red) ![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)

### 📌 Visão Geral da Etapa

Com a base de dados já tratada, esta etapa expande o projeto incorporando dados de telemetria de um aplicativo próprio de monitoramento de condutor, que capta métricas de câmera (fechamento dos olhos, piscadas, bocejos e posição da cabeça) durante as viagens.

O objetivo passou a ser **estimar a probabilidade de risco** (fadiga ou desatenção) de um condutor a partir desses sinais brutos, utilizando técnicas de **Machine Learning**. Para isso, foi utilizada a biblioteca `scikit-learn`, com o algoritmo **RandomForestClassifier**, treinado para classificar cada leitura de sensor como situação de risco ou normalidade.

Ao longo do desenvolvimento do modelo, surgiram desafios importantes que guiaram as decisões metodológicas:

- **Desbalanceamento de classes**: os registros de risco (`WARNING`/`FATIGUED`) representam menos de 1% da base, o que exigiu tratamento específico para evitar um modelo enviesado.
- **Balanceamento com SMOTE**: aplicação da técnica de superamostragem sintética (biblioteca `imbalanced-learn`) para equilibrar as classes no conjunto de treino, sem comprometer a integridade do conjunto de teste.
- **Ajuste do limiar de decisão**: em vez de utilizar o padrão de 50%, o limiar de classificação foi ajustado priorizando o *recall* da classe de risco — no contexto de segurança veicular, é mais custoso deixar passar um caso real de fadiga do que gerar um alerta desnecessário.
- **Interpretação do modelo**: análise de *feature importance* para identificar quais sinais (PERCLOS, taxa de piscadas, bocejo, inclinação da cabeça) mais contribuem para a detecção de risco.
- **Validação contextual**: cruzamento dos horários de maior risco identificados pelo modelo com os horários de maior incidência de acidentes comportamentais na base da PRF (Etapa 1), como forma de contextualizar — não validar causalmente — os resultados.

### 🎯 Resultados

| Métrica | Antes do balanceamento | Depois do balanceamento (SMOTE) |
|---|---|---|
| Recall (classe risco) | 14% | 38% |
| Acurácia geral | 98,7% | 96,07% |

> ⚠️ A acurácia geral não foi utilizada como métrica principal de avaliação, pois se mostrou enganosa dado o forte desbalanceamento das classes. O foco da análise foi o *recall* da classe de risco.

### 📂 Notebooks desta etapa

- [`ML.ipynb`](./ML.ipynb) — modelagem, balanceamento, avaliação e interpretação do modelo
- [`tratando.ipynb`](./tratando.ipynb) — tratamento e preparação dos dados de telemetria

### ⚠️ Limitações

- Poucos exemplos reais de risco na base (apenas 308 em ~59 mil leituras), o que limita a capacidade de generalização do modelo.
- O cruzamento com os dados da PRF é contextual (por horário), não havendo vínculo direto entre os usuários do aplicativo e os acidentes registrados — portanto, não implica causalidade.

---

### 🛠️ Tecnologias e Ferramentas Utilizadas

* **Linguagem:** Python
* **Machine Learning:** Scikit-learn (RandomForestClassifier) e Imbalanced-learn (SMOTE)
* **Visualização:** Matplotlib e Seaborn
* **Banco de Dados:** Supabase (PostgreSQL)
* **Ambiente de Desenvolvimento:** Jupyter Notebook

---
## 🚀 Como Executar o Projeto

```bash
# 1. Clone o repositório
git clone https://github.com/Raimundo2004/ETL-Acidentes.git

# 2. Acesse a pasta do projeto
cd nome-do-repositorio

# 3. Instale as dependências necessárias
pip install -r requirements.txt

# 4. Execute os notebooks na ordem
jupyter notebook

# Depois abra e execute, em ordem:
# - tratando.ipynb (Etapa 1: ETL da base da PRF e da telemetria)
# - ML.ipynb (Etapa 2: modelagem e avaliação)

