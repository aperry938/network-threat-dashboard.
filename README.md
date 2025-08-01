# network-threat-dashboard.
graph TD
    subgraph "Data Ingestion & Storage"
        A[🌐 VPC Flow Logs] --> B[🔥 Amazon Kinesis Data Firehose];
        B -- "Raw Logs for Archival" --> C[🗄️ Amazon S3 Data Lake];
    end

    subgraph "Real-Time Processing & ML Inference"
        B -- "Real-time Stream" --> D[⚙️ AWS Lambda Function];
        D -- "Processed Data" --> E[🧠 Amazon SageMaker Endpoint];
        E -- "Anomaly Score" --> D;
    end

    subgraph "Alerting & Visualization"
        D -- "If Score > Threshold" --> F[🔔 Amazon SNS Topic];
        F --> G[👨‍💻 SOC Team <br/>via Email/PagerDuty];
        D -- "Time-Series Metrics" --> H[📊 Amazon Timestream];
        I[🖥️ React.js Dashboard <br/>Hosted on AWS Amplify] -- "Queries Data" --> H;
        I --> G;
    end
