```mermaid
flowchart LR

    subgraph Client_Layer
        UI[Web Frontend (React / Next.js)]
    end

    subgraph API_Layer
        API[Go Backend API (Gin/Echo)]
        Auth[Auth & RBAC (JWT + Refresh Tokens)]
        Validator[Validation Layer]
        Logger[Logging & Error Handling]
    end

    subgraph Application_Core
        Visits[Visits Service]
        Prescriptions[Prescription Service]
        Patients[Patient Service]
        Doctors[Doctor Service]
        Cache[Redis Cache (Token Lookup, Rate Limiting)]
    end

    subgraph DB_Layer
        DB[(PostgreSQL - RDS / Local)]
    end

    subgraph Cloud_and_Infra
        ECR[(AWS ECR - Container Registry)]
        ECS[(AWS ECS or EC2 - Container Runtime)]
        S3[(AWS S3 - File Storage)]
        CW[(CloudWatch - Logs & Metrics)]
        LB[(Application Load Balancer)]
        CI[GitHub Actions - CI/CD Pipeline]
    end

    UI -->|HTTPS| LB
    LB --> API

    API --> Auth
    API --> Validator
    API --> Logger

    API --> Visits
    API --> Prescriptions
    API --> Patients
    API --> Doctors

    Visits --> DB
    Prescriptions --> DB
    Patients --> DB
    Doctors --> DB

    Prescriptions --> Cache
    API --> Cache

    API --> S3
    ECS --> CW
    ECS --> DB
    ECS --> S3

    CI --> ECR
    ECR --> ECS
```
