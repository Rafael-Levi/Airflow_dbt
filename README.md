```mermaid
flowchart TD

    %% --- DEV Environments ---
    subgraph DEV1 [Ambiente DEV 1]
        U1[User] --> L1[localhost <br> dbt]
        L1 --> D1[(Database)]
    end

    subgraph DEV2 [Ambiente DEV 2]
        U2[User] --> L2[localhost <br> dbt]
        L2 --> D2[(Database)]
    end

    %% --- GitHub ---
    GH[(GitHub)]

    L1 --> GH
    L2 --> GH

    %% --- PROD Environment ---
    subgraph PROD [Ambiente PROD]
        VM[Stateless VM <br> dbt] --> DP[(Database)]
        DP --> C[(Cloud)]
        DW[Execução periódica <br> DAG DW] --> VM
    end

    %% --- Airflow + Cosmos ---
    subgraph AIRFLOW [Airflow + Cosmos]
        LOC[localhost ou Cloud] --> DBTA[dbt Cosmos]
        DBTA --> AF[Apache Airflow]
    end

    %% --- Connections from GitHub ---
    GH -->|Merge na branch principal<br/>deploy em PROD| VM
    GH -->|Merge na branch principal<br/>atualiza Airflow| DBTA


```

Project Contents
================

Your Astro project contains the following files and folders:

- dags: This folder contains the Python files for your Airflow DAGs. By default, this directory includes one example DAG:
    - `example_astronauts`: This DAG shows a simple ETL pipeline example that queries the list of astronauts currently in space from the Open Notify API and prints a statement for each astronaut. The DAG uses the TaskFlow API to define tasks in Python, and dynamic task mapping to dynamically print a statement for each astronaut. For more on how this DAG works, see our [Getting started tutorial](https://www.astronomer.io/docs/learn/get-started-with-airflow).
- Dockerfile: This file contains a versioned Astro Runtime Docker image that provides a differentiated Airflow experience. If you want to execute other commands or overrides at runtime, specify them here.
- include: This folder contains any additional files that you want to include as part of your project. It is empty by default.
- packages.txt: Install OS-level packages needed for your project by adding them to this file. It is empty by default.
- requirements.txt: Install Python packages needed for your project by adding them to this file. It is empty by default.
- plugins: Add custom or community plugins for your project to this file. It is empty by default.
- airflow_settings.yaml: Use this local-only file to specify Airflow Connections, Variables, and Pools instead of entering them in the Airflow UI as you develop DAGs in this project.

