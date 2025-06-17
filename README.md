# 📊 (GE) Engenharia de Dados - Pipeline ETL com 1 Bilhão de Linhas

## 🎯 Objetivo

Este projeto tem como objetivo desenvolver um pipeline completo de Engenharia de Dados, processando um dataset com 1 bilhão de linhas. O pipeline seguirá todas as etapas de um processo profissional de ETL (Extração, Transformação e Carga), utilizando ferramentas **open source** amplamente utilizadas no mercado.

---

## 📌 Contexto dos Dados

O dataset será gerado sinteticamente. O tema pode ser escolhido entre os seguintes exemplos:

- **Financeiro:** Transações de cartões de crédito
- **E-commerce:** Histórico de compras de usuários
- **Mobilidade:** Corridas de aplicativos de transporte
- **IoT:** Leituras de sensores em tempo real

O formato final dos dados será `.csv` ou `.parquet`.

---

## 🛠️ Ferramentas do Pipeline

| Etapa | Ferramenta | Descrição |
|-----|------|----|
| Geração de Dados | Python (Faker, Pandas, Polars) | Criação de dados sintéticos |
| Armazenamento | MinIO | Data Lake para os arquivos brutos |
| Exploração Local | DuckDB | Análises exploratórias e validação |
| Consulta Distribuída | Trino (Presto) | Query engine distribuído conectado ao MinIO |
| Transformações | DBT | Modelagem de dados com camadas staging, intermediate e mart |
| Orquestração | Apache Airflow | Agendamento e execução dos pipelines |
| (Opcional) Visualização | Apache Superset ou Metabase | Criação de dashboards |

---

## 📍 Fases do Projeto

### Fase 1 – Geração de Dados

- Desenvolver um script em Python para gerar um arquivo com 1 bilhão de linhas.
- Exemplos de colunas (tema financeiro):
  - `transaction_id`
  - `customer_id`
  - `transaction_amount`
  - `transaction_date`
  - `merchant_category`
  - `payment_method`
- Formato de saída: `.csv` ou `.parquet`.

---

### Fase 2 – Upload para o MinIO

- Subir os arquivos para o bucket `landing-zone` no MinIO.
- Configurar o MinIO localmente via Docker.

---

### Fase 3 – Exploração de Dados com DuckDB

- Conectar ao arquivo local ou ao MinIO.
- Realizar análises básicas:
  - Contagem de linhas
  - Validação de tipos
  - Estatísticas descritivas

---

### Fase 4 – Query Distribuída com Trino

- Instalar e configurar o Trino (ou Presto).
- Criar catálogo apontando para o MinIO.
- Executar queries SQL distribuídas.

Exemplos de queries:
- `SELECT COUNT(*)`
- Agregações por categoria
- Filtragem por intervalo de datas

---

### Fase 5 – Transformações com DBT

- Estruturar o projeto DBT.
- Criar as seguintes camadas:

| Camada | Finalidade |
|----|----|
| Staging | Tratamento inicial e padronização de dados |
| Intermediate | Limpeza, enriquecimento e junções |
| Mart | Tabelas finais analíticas |

- Executar os modelos DBT com Trino como backend.

---

### Fase 6 – Orquestração com Airflow

- Criar um DAG no Airflow com as seguintes tasks:

1. **Geração de dados**
2. **Upload para MinIO**
3. **Validação com DuckDB**
4. **Consultas com Trino**
5. **Execução de modelos DBT**
6. **(Opcional) Geração de dashboard**

---

## ✅ Tecnologias

- **Python**
- **MinIO**
- **DuckDB**
- **Trino (Presto)**
- **DBT**
- **Apache Airflow**
- **(Opcional) Apache Superset ou Metabase**

---

## 💬 Observações

- Todas as ferramentas utilizadas devem ser **open source** e de uso livre.
- A complexidade e o nível de detalhamento são graduais: o foco é o aprendizado.
- A escolha do contexto dos dados fica livre para o grupo.

---

**Bons estudos! 🚀**
