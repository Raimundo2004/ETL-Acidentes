# 🚗 Análise de Acidentes de Trânsito no Brasil: O Fator Fadiga

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

Como resultado, foi construída uma base de dados totalmente higienizada, padronizada e otimizada, pronta para suportar as próximas fases do projeto. As etapas seguintes contemplam a realização da **Análise Exploratória de Dados (EDA)** e o desenvolvimento de técnicas de **Feature Engineering**, com foco na investigação dos acidentes relacionados à **fadiga e ao sono**, permitindo extrair padrões, identificar fatores de risco e gerar insights que apoiem futuras análises e modelos preditivos.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **Linguagem:** Python
* **Manipulação e Tratamento:** Pandas, NumPy e unicodedata

---

## 🚀 Como Executar o Projeto

```bash
# 1. Clone o repositório
git clone [https://github.com/seu-usuario/nome-do-repositorio.git](https://github.com/seu-usuario/nome-do-repositorio.git)

# 2. Acesse a pasta do projeto
cd nome-do-repositorio

# 3. Instale as dependências necessárias
pip install -r requirements.txt

# 4. Execute o script de ETL
python etl_pipeline.py
