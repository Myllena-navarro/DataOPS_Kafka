# 🚀 Data Streaming Pipeline — Kafka, Parquet, Iceberg (Bronze, Silver, Gold)

## 📊 Descrição

Este projeto implementa um pipeline de dados em streaming local utilizando Kafka, com processamento em micro-batches e arquitetura em camadas (Bronze, Silver e Gold).

O objetivo é simular um fluxo real de dados chegando continuamente, sendo processados e organizados para análise.

---

## 🧠 Arquitetura do Pipeline

O fluxo de dados segue as seguintes etapas:

1. **Producer**

   * Lê dataset de aeroportos (OpenFlights)
   * Envia dados em pequenos blocos (chunks) para o Kafka

2. **Kafka**

   * Armazena os eventos no tópico `airports_raw`

3. **Consumer (Bronze)**

   * Consome dados em micro-batches (30 segundos)
   * Persiste os dados brutos em formato Parquet

4. **Silver**

   * Processa os dados com PySpark
   * Aplica tipagem, limpeza e deduplicação
   * Armazena em formato Iceberg

5. **Gold**

   * Filtra dados relevantes (aeroportos do Brasil)
   * Cria tabela analítica final

---

## 🏗️ Arquitetura

```text
Dataset → Producer → Kafka → Consumer → Bronze (Parquet)
                                    ↓
                                 Silver (Iceberg)
                                    ↓
                                  Gold
```

---

## 🛠️ Tecnologias utilizadas

* Python 3.12
* Kafka (via Docker)
* pandas
* PySpark
* Apache Iceberg
* Parquet
* kafka-python

---

## 📁 Estrutura do projeto

```text
workshop_streaming/
├── docker-compose.yml
├── requirements.txt
├── producer.py
├── consumer_bronze.py
├── silver_iceberg.py
├── gold_brazil.py
├── data/
│   ├── bronze/
│   └── warehouse/
└── README.md
```

---

## ⚙️ Pré-requisitos

* Python 3.10+
* Docker e Docker Compose
* Java 17+
* Ambiente virtual (venv)

---

## 🚀 Configuração do ambiente

### 1. Criar ambiente virtual

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

### 2. Instalar dependências

```bash
pip install -r requirements.txt
```

---

### 3. Subir Kafka

```bash
docker compose up -d
```

Verifique:

```bash
docker ps
```

---

## ▶️ Execução do pipeline

### 1. Rodar Producer

```bash
python producer.py
```

👉 Envia dados em chunks para o Kafka

---

### 2. Rodar Consumer (Bronze)

```bash
python consumer_bronze.py
```

👉 Gera arquivos Parquet em:

```text
data/bronze/airports/
```

---

### 3. Gerar camada Silver

```bash
python silver_iceberg.py
```

👉 Cria tabela:

```text
local.silver.airports
```

---

### 4. Gerar camada Gold

```bash
python gold_brazil.py
```

👉 Cria tabela:

```text
local.gold.airports_br
```

---

## 📊 Conceitos aplicados

* Streaming de dados
* Producer / Consumer
* Kafka topics e offsets
* Micro-batch processing
* Arquitetura Bronze, Silver e Gold
* Data Lake com Parquet
* Data Lakehouse com Iceberg

---

## 📦 Camadas de dados

| Camada | Descrição                     |
| ------ | ----------------------------- |
| Bronze | Dados brutos em Parquet       |
| Silver | Dados tratados e padronizados |
| Gold   | Dados filtrados para análise  |

---

## 🎯 Objetivos alcançados

* Implementação de pipeline de streaming local
* Simulação de ingestão contínua de dados
* Persistência em múltiplas camadas
* Transformação com PySpark
* Uso de arquitetura moderna de dados

---

## ⚠️ Limitações

* Execução local (não distribuída)
* Sem orquestração (ex: Airflow)
* Sem monitoramento avançado
* Sem controle de schema evolutivo

---

## 🔄 Melhorias futuras

* Orquestração com Airflow
* Monitoramento com logs estruturados
* Deploy em cloud (AWS / GCP)
* Integração com Data Lake real
* Schema evolution com Iceberg

---

## 👩‍💻 Autora

Projeto desenvolvido por Myllena Navarro Lins como prática de Engenharia de Dados / DataOps.

---
