```mermaid
flowchart LR

    %% External
    Customer((Customer)) -->|HTTP/HTTPS| LB[Load Balancer/API Gateway]

    %% Microservices
    LB --> MS1[Order Service]
    LB --> MS2[Inventory Service]
    LB --> MS3[Payment Service]
    LB --> MS4[Shipping Service]
    LB --> MS5[User Service]
    LB --> MS6[Notifications Service]

    %% Kafka for async
    MS1 -->|Publish/Consume| KAFKA((Kafka Cluster))
    MS2 -->|Publish/Consume| KAFKA
    MS3 -->|Publish/Consume| KAFKA
    MS4 -->|Publish/Consume| KAFKA
    MS5 -->|Publish/Consume| KAFKA
    MS6 -->|Publish/Consume| KAFKA

    %% Databases
    MS1 -->|SQL Reads/Writes| RDBMS[(Relational DB)]
    MS1 -->|Cache| CACHE[(Redis)]
    MS2 -->|NoSQL Reads/Writes| NOSQL[(NoSQL DB)]
    MS3 -->|SQL Reads/Writes| RDBMS
    MS4 -->|SQL Reads/Writes| RDBMS
    MS5 -->|SQL Reads/Writes| RDBMS
    MS6 -->|SQL Reads/Writes| RDBMS

    %% Observability
    MS1 --> MONITORING[Prometheus/Grafana]
    MS2 --> MONITORING
    MS3 --> MONITORING
    MS4 --> MONITORING
    MS5 --> MONITORING
    MS6 --> MONITORING

    MS1 --> LOGGING[ELK/EFK Stack]
    MS2 --> LOGGING
    MS3 --> LOGGING
    MS4 --> LOGGING
    MS5 --> LOGGING
    MS6 --> LOGGING

    %% Service Mesh
    subgraph Service Mesh
        MS1SM(Service Mesh Sidecar) -- Intercepts traffic --> MS2SM(Service Mesh Sidecar)
        MS2SM -- Intercepts traffic --> MS3SM(Service Mesh Sidecar)
        MS3SM -- Intercepts traffic --> MS4SM(Service Mesh Sidecar)
        MS4SM -- Intercepts traffic --> MS5SM(Service Mesh Sidecar)
        MS5SM -- Intercepts traffic --> MS6SM(Service Mesh Sidecar)
    end
