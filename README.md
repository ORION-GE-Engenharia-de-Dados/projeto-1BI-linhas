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

O formato final dos dados será `.parquet`.

---

## 🛠️ Ferramentas do Pipeline

| Etapa | Ferramenta | Descrição |
|-----|------|----|
| Geração de Dados | Python (Faker, Pandas, Polars) | Criação de dados sintéticos |
| Armazenamento | MinIO | Data Lake com camadas Bronze, Silver e Gold |
| Metastore de Metadados | Hive Metastore | Registro de schemas e tabelas para leitura via Trino |
| Exploração Local | DuckDB | Análises exploratórias e validação rápida local |
| Consulta Distribuída | Trino (Presto) | Query engine distribuído conectado ao MinIO e ao Hive Metastore |
| Transformações | DBT | Modelagem de dados com camadas staging, intermediate e mart |
| Orquestração | Apache Airflow | Agendamento e execução dos pipelines |
| (Opcional) Visualização | Apache Superset ou Metabase | Criação de dashboards |

---

## 📍 Estrutura de Camadas do Data Lake (MinIO)

Seguindo a arquitetura em camadas (medallion architecture), o Data Lake será organizado da seguinte forma:

| Camada | Nome | Finalidade |
|---|---|---|
| **Bronze (Raw / Bruto)** | `landing-zone` | Armazena os dados exatamente como gerados, sem nenhum tratamento |
| **Silver (Processed / Limpo)** | `silver` | Dados tratados, com tipos corrigidos, dados inválidos removidos e enriquecimentos básicos aplicados |
| **Gold (Curated / Business Ready)** | `gold` | Dados prontos para análises de negócio, com agregações, métricas e modelos de dados finais |

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
- Formato de saída: `.parquet`.
- Upload inicial dos dados na camada **Bronze (landing-zone)** no MinIO.
- Usar a imagem: `quay.io/minio/minio:RELEASE.2025-02-03T21-03-04Z-cpuv1`

---

### Fase 2 – Exploração de Dados com DuckDB

- Conectar ao arquivo localmente ou via S3 API com MinIO.
- Realizar análises básicas:
  - Contagem de linhas
  - Validação de tipos
  - Estatísticas descritivas
- Tudo será feito diretamente sobre os dados da camada **Bronze**.

---

### Fase 3 – Registro de Metadados com Hive Metastore

- Instalar e configurar o **Hive Metastore**.
- Criar as tabelas externas correspondentes aos datasets armazenados no MinIO.
- Exemplo: criar tabelas externas apontando para o bucket `landing-zone`.

---

### Fase 4 – Consulta Distribuída com Trino

- Instalar e configurar o Trino.
- Conectar o Trino ao **Hive Metastore**.
- Criar catálogo S3 apontando para os buckets do MinIO.
- Executar queries SQL sobre os dados na **Bronze** e depois sobre as camadas transformadas (**Silver/Gold**).

---

### Fase 5 – Transformações com DBT

- Estruturar o projeto DBT com três camadas de modelagem:

| Camada | Finalidade |
|----|----|
| **Staging** | Leitura da camada Bronze, ajustes de tipos e padronizações iniciais |
| **Intermediate** | Limpeza, enriquecimento, remoção de duplicatas e filtros de qualidade |
| **Mart** | Criação de tabelas finais para consumo de negócio (ex: fatos e dimensões) |

- As saídas das transformações da **Staging** vão para a camada **Silver**, e os modelos finais do **Mart** vão para a camada **Gold** no MinIO.

- DBT se conectará ao Trino, que por sua vez usa o Hive Metastore para interpretar os dados.

---

### Fase 6 – Orquestração com Airflow

- Criar um DAG no Airflow com as seguintes tasks:

1. **Geração de dados**
2. **Upload para MinIO (Bronze)**
3. **Validação com DuckDB**
4. **Registro de metadados no Hive**
5. **Consultas exploratórias com Trino**
6. **Execução dos modelos DBT (gerando Silver e Gold)**
7. **(Opcional) Geração de dashboards no Superset ou Metabase**

---

## ✅ Tecnologias Finais

- **Python**
- **MinIO (Data Lake com camadas Bronze, Silver e Gold)**
- **Hive Metastore**
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

**Bons estudos e bom projeto! 🚀**
