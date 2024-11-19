<p align="center">
  <a href="https://suajornadadedados.com.br/"><img src="https://github.com/lvgalvao/data-engineering-roadmap/raw/main/pics/logo.png" alt="Jornada de Dados"></a>
</p>
<p align="center">
    <em>Nossa missão é fornecer o melhor ensino em engenharia de dados</em>
</p>

Bem-vindo à **Jornada de Dados**

# ETL com Monitoramento e Integração de Dados Multiformato

Este projeto é um pipeline ETL completo que processa dados de diferentes fontes, incluindo planilhas Excel, APIs em tempo real (mercado financeiro) e dados batch provenientes de SQL Server. O objetivo é consolidar esses dados em um **Data Warehouse PostgreSQL**, utilizando **dbt** para transformações, com monitoramento robusto por **Sentry** e **OpenTelemetry**. Também inclui um dashboard para visualizar o uso e os cálculos de KPIs realizados.

---

## Arquitetura

```mermaid
flowchart TD
    Excel[Planilhas Excel (S3)] --> ETL[Pipeline ETL]
    API[API Mercado Financeiro (S3)] --> ETL
    Batch[Dados Batch SQL Server (S3)] --> ETL
    ETL --> DBT[Transformações dbt]
    DBT --> Postgres[PostgreSQL (Data Warehouse)]
    DBT --> Monitoramento[Observabilidade (Sentry e OpenTelemetry)]
    Monitoramento --> Alertas[Alertas e Logs]
    DBT --> Dashboard[Dashboard de KPIs]
```

---

## Ferramentas Utilizadas

1. **Airflow**: Orquestrador para ingestão e integração dos dados.  
2. **dbt**: Responsável por transformações SQL organizadas em camadas.  
3. **Amazon S3**: Armazena dados brutos das fontes de entrada.  
4. **PostgreSQL**: Banco de dados utilizado como Data Warehouse.  
5. **OpenTelemetry**: Rastreabilidade e métricas do pipeline.  
6. **Sentry**: Captura de erros e geração de alertas.  
7. **Superset (Apache)**: Para visualização de dashboards e métricas de uso.  

---

## Pré-requisitos

1. **Python 3.8+**: Certifique-se de ter o Python 3.8 ou superior instalado.  
2. **dbt CLI**: Instale o dbt para gerenciar transformações SQL.  
3. **Docker**: Utilize contêineres para gerenciar o ambiente.  
4. **Dependências**: Instale as bibliotecas listadas no arquivo `requirements.txt`.  

---

## Configuração

1. **Buckets S3**:
   - `raw-data`: Armazena os dados brutos das fontes (Excel, APIs, SQL Server).  

2. **Arquivo `.env`**:
   Crie um arquivo `.env` com as credenciais e variáveis de ambiente:  
   ```env
   AWS_ACCESS_KEY_ID=sua_chave
   AWS_SECRET_ACCESS_KEY=sua_secret
   POSTGRES_DB=nome_do_banco
   POSTGRES_USER=usuario
   POSTGRES_PASSWORD=senha
   POSTGRES_HOST=localhost
   POSTGRES_PORT=5432
   ```

3. **dbt Profiles**:
   Configure o arquivo `profiles.yml` do dbt para conectar ao PostgreSQL.

4. **Superset**:
   Instale e configure o **Superset** para criar o dashboard de KPIs.

---

## Dashboard: O que será monitorado?

O dashboard inclui as seguintes métricas e KPIs:

1. **Processos Executados**:
   - Quantidade de processos ETL realizados por tipo (Excel, APIs, Batch).  
   - Monitoramento de sucesso/falha em cada execução.  

2. **KPIs Calculados**:
   - Quantidade de KPIs gerados por dia, semana e mês.  
   - Análise dos cálculos de KPIs divididos por fonte de dados.  

3. **Uso do Dashboard**:
   - Número de usuários acessando o dashboard diariamente.  
   - Frequência de visualização de KPIs específicos.  

4. **Dados em Tempo Real**:
   - Atualizações de APIs em tempo real, com tempo médio de processamento.

---

## Como Visualizar o Dashboard?

### Configuração do Superset:
1. Instale o Superset:
   ```bash
   pip install apache-superset
   ```

2. Inicialize o Superset:
   ```bash
   superset db upgrade
   superset fab create-admin
   superset init
   ```

3. Inicie o servidor:
   ```bash
   superset run -p 8088 --with-threads --reload --debugger
   ```

4. Conecte o Superset ao PostgreSQL:
   - Configure uma conexão com o banco para acessar as tabelas criadas pelo dbt.  

5. Crie os Dashboards:
   - Utilize as tabelas de mart criadas pelo dbt para configurar os gráficos e KPIs.  

---

## Monitoramento e Alertas

1. **OpenTelemetry**:
   - Monitore o fluxo completo de tarefas e identifique gargalos.  
   - Integre com ferramentas como Grafana para visualizar traces.  

2. **Sentry**:
   - Receba alertas automáticos de falhas ou anomalias em tempo real.  

---

## Sobre o Workshop

Instrutores:
- **Luciano Vasconcelos**: Especialista em Engenharia de Dados.  
- **Fábio Melo**: Referência em pipelines e observabilidade.  

---

**⭐ Dê uma estrela neste repositório se você gostou do conteúdo!**