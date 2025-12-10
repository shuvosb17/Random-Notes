flowchart LR
    subgraph Client Layer
        UI[Web Frontend<br>(React / Next.js)]
    end

    subgraph API Layer
        API[Go Backend API<br>(Gin/Echo)]
        Auth[Auth & RBAC<br>(JWT + Refresh Tokens)]
        Validator[Validation Layer]
        Logger[Logging & Error Handling]
    end

    subgraph Application Core
        Visits[Visits Service]
        Prescriptions[Prescription Service]
        Patients[Patient Service]
        Doctors[Doctor Service]
        Cache[Redis Cache<br>(Token Lookup, Rate Limiting)]
    end

    subgraph DB Layer
        DB[(PostgreSQL<br>(RDS/Local))]
    end

    subgraph Cloud & Infra
        ECR[(AWS ECR<br>Container Registry)]
        ECS[(AWS ECS or EC2<br>Container Runtime)]
        S3[(AWS S3<br>File Storage)]
        CW[(CloudWatch<br>Logs & Metrics)]
        LB[(Application Load Balancer)]
        CI[GitHub Actions<br>CI/CD Pipeline]
    end

    UI -->|HTTPS Requests| LB
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
