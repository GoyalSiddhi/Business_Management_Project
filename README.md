# 🏢 Business Management System

A comprehensive Spring Boot application for managing business operations including purchasing, supplier management, inventory control, and user authentication.

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This Business Management System is designed to streamline core business operations through a modern web-based interface. The application provides comprehensive modules for purchasing workflows, supplier relationship management, inventory tracking, and secure user authentication.

## 🏗️ Architecture

### 1. High-Level Interaction Diagram (Upstream / Downstream)

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#f8fafc',
    'primaryTextColor': '#1e293b',
    'primaryBorderColor': '#64748b',
    'lineColor': '#94a3b8'
  }
}}%%

flowchart LR
    %% Upstream Systems
    subgraph "🔼 Upstream Systems"
        ERP[🏢 ERP System<br/>Master Data]:::upstream
        VENDOR[🏪 Vendor Portal<br/>Catalogs & Pricing]:::upstream
        AUTH[🔐 LDAP/AD<br/>User Authentication]:::upstream
    end

    %% Core Business System
    subgraph "🎯 Business Management System"
        PURCHASE[📦 Purchase Management]:::core
        SUPPLIER[🤝 Supplier Management]:::core
        INVENTORY[📊 Inventory Control]:::core
        USER[👤 User Management]:::core
    end

    %% Downstream Systems
    subgraph "🔽 Downstream Systems"
        FINANCE[💰 Financial System<br/>AP/GL Integration]:::downstream
        WMS[📦 Warehouse System<br/>Fulfillment]:::downstream
        REPORT[📈 BI/Reporting<br/>Analytics]:::downstream
        NOTIF[📧 Notification Service<br/>Alerts & Updates]:::downstream
    end

    %% Upstream Flows
    ERP -->|Master Data Sync| PURCHASE
    ERP -->|Product Catalog| INVENTORY
    VENDOR -->|Price Updates| SUPPLIER
    VENDOR -->|Availability| INVENTORY
    AUTH -->|User Validation| USER

    %% Downstream Flows
    PURCHASE -->|PO Data| FINANCE
    PURCHASE -->|Fulfillment Orders| WMS
    INVENTORY -->|Stock Levels| REPORT
    SUPPLIER -->|Performance Data| REPORT
    USER -->|Activity Logs| NOTIF

    %% Styling
    classDef upstream fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
    classDef core fill:#fff3e0,stroke:#ef6c00,stroke-width:2px,color:#bf360c
    classDef downstream fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px,color:#1b5e20

```

### 2. Context Diagram

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#f8fafc',
    'primaryTextColor': '#1e293b',
    'primaryBorderColor': '#64748b',
    'lineColor': '#94a3b8'
  }
}}%%

flowchart TD
    %% External Entities
    BUYER[👤 Purchase Manager<br/>Creates & Manages Orders]:::actor
    ADMIN[👨‍💼 System Admin<br/>User & Config Management]:::actor
    SUPPLIER_USER[🏪 Supplier<br/>External Vendor]:::external
    FINANCE_USER[💰 Finance Team<br/>Budget & Approval]:::actor

    %% Central System
    BMS[🏢 Business Management System<br/>Core Application]:::system

    %% External Systems
    EMAIL_SYS[📧 Email System]:::external
    PAYMENT_SYS[💳 Payment Gateway]:::external
    ERP_SYS[🏢 Enterprise System]:::external

    %% User Interactions
    BUYER -->|Create Purchase Orders| BMS
    BUYER -->|Track Order Status| BMS
    ADMIN -->|Manage Users & Suppliers| BMS
    FINANCE_USER -->|Approve & Budget Control| BMS

    %% System Interactions
    BMS -->|Order Notifications| EMAIL_SYS
    BMS -->|Payment Processing| PAYMENT_SYS
    BMS -->|Data Synchronization| ERP_SYS
    SUPPLIER_USER -->|Catalog & Pricing Updates| BMS

    %% Response Flows
    EMAIL_SYS -.->|Delivery Confirmations| BMS
    PAYMENT_SYS -.->|Transaction Status| BMS
    ERP_SYS -.->|Master Data Updates| BMS

    %% Styling
    classDef actor fill:#e8f5e8,stroke:#388e3c,stroke-width:2px,color:#1b5e20
    classDef system fill:#fff3e0,stroke:#f57c00,stroke-width:3px,color:#e65100
    classDef external fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#4a148c

```

### 3. Data Flow Diagram

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#f8fafc',
    'primaryTextColor': '#1e293b',
    'primaryBorderColor': '#64748b',
    'lineColor': '#94a3b8'
  }
}}%%

flowchart TD
    %% External Entities
    USER[👤 User]:::entity
    VENDOR[🏪 Vendor]:::entity
    FINANCE[💰 Finance Dept]:::entity

    %% Processes
    P1[📝 1.0<br/>Create Purchase Request]:::process
    P2[✅ 2.0<br/>Approve Purchase Order]:::process
    P3[📦 3.0<br/>Manage Inventory]:::process
    P4[📊 4.0<br/>Generate Reports]:::process

    %% Data Stores
    DS1[(🗄️ D1: Purchase Orders)]:::datastore
    DS2[(🗄️ D2: Suppliers)]:::datastore
    DS3[(🗄️ D3: Inventory)]:::datastore
    DS4[(🗄️ D4: Users)]:::datastore

    %% Data Flows
    USER -->|Purchase Request| P1
    P1 -->|PO Details| DS1
    DS1 -->|Pending POs| P2
    P2 -->|Approved PO| DS1
    DS1 -->|Order Info| VENDOR
    VENDOR -->|Delivery Confirmation| P3
    P3 -->|Stock Updates| DS3
    DS3 -->|Stock Levels| P1
    DS2 -->|Supplier Info| P1
    DS4 -->|User Permissions| P2
    P2 -->|Approval Status| FINANCE
    DS1 -->|Order Data| P4
    DS3 -->|Inventory Data| P4
    P4 -->|Reports| USER
    P4 -->|Analytics| FINANCE

    %% Styling
    classDef entity fill:#e0f2fe,stroke:#0277bd,stroke-width:2px,color:#01579b
    classDef process fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#e65100
    classDef datastore fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#4a148c
```

### 4. Deployment Diagram

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#f8fafc',
    'primaryTextColor': '#1e293b',
    'primaryBorderColor': '#64748b',
    'lineColor': '#94a3b8'
  }
}}%%

flowchart TB
    %% Client Tier
    subgraph "🖥️ Client Tier"
        BROWSER[🌐 Web Browser<br/>Chrome/Firefox/Safari]:::client
        MOBILE[📱 Mobile Browser<br/>Responsive UI]:::client
    end

    %% Load Balancer
    LB[⚖️ Load Balancer<br/>Nginx/Apache]:::infrastructure

    %% Application Tier
    subgraph "🏗️ Application Tier"
        subgraph "🖥️ App Server 1"
            APP1[☕ Spring Boot App<br/>Primary Instance<br/>Port: 8080]:::application
        end
        subgraph "🖥️ App Server 2"
            APP2[☕ Spring Boot App<br/>Secondary Instance<br/>Port: 8081]:::application
        end
    end

    %% Database Tier
    subgraph "🗄️ Database Tier"
        DB_PRIMARY[(💽 MySQL Primary<br/>Read/Write<br/>Port: 3306)]:::database
        DB_REPLICA[(📖 MySQL Replica<br/>Read Only<br/>Port: 3307)]:::database
    end

    %% External Services
    subgraph "🌐 External Services"
        EMAIL_SVC[📧 SMTP Server<br/>Email Service<br/>Port: 587]:::external
        PAYMENT_SVC[💳 Payment API<br/>HTTPS Gateway<br/>Port: 443]:::external
    end

    %% Monitoring & Logging
    subgraph "📊 Monitoring Tier"
        MONITOR[📈 Application Monitoring<br/>Actuator Endpoints]:::monitoring
        LOGS[📝 Log Aggregation<br/>Centralized Logging]:::monitoring
    end

    %% Connections
    BROWSER --> LB
    MOBILE --> LB
    LB --> APP1
    LB --> APP2
    APP1 --> DB_PRIMARY
    APP2 --> DB_PRIMARY
    APP1 --> DB_REPLICA
    APP2 --> DB_REPLICA
    DB_PRIMARY -.->|Replication| DB_REPLICA
    APP1 --> EMAIL_SVC
    APP2 --> EMAIL_SVC
    APP1 --> PAYMENT_SVC
    APP2 --> PAYMENT_SVC
    APP1 --> MONITOR
    APP2 --> MONITOR
    APP1 --> LOGS
    APP2 --> LOGS

    %% Deployment Annotations
    LB -.->|HTTP/HTTPS<br/>Port 80/443| APP1
    APP1 -.->|JDBC<br/>Port 3306| DB_PRIMARY

    %% Styling
    classDef client fill:#e8f5e8,stroke:#388e3c,stroke-width:2px,color:#1b5e20
    classDef infrastructure fill:#e0f2fe,stroke:#0277bd,stroke-width:2px,color:#01579b
    classDef application fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#e65100
    classDef database fill:#ffebee,stroke:#d32f2f,stroke-width:2px,color:#b71c1c
    classDef external fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#4a148c
    classDef monitoring fill:#f5f5f5,stroke:#616161,stroke-width:2px,color:#424242
```

