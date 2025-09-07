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

### System Architecture Diagram

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#f8fafc',
    'primaryTextColor': '#1e293b',
    'primaryBorderColor': '#64748b',
    'lineColor': '#94a3b8',
    'secondaryColor': '#f1f5f9',
    'tertiaryColor': '#e2e8f0'
  }
}}%%

flowchart TD
    %% User Layer
    subgraph "👥 Presentation Layer"
        UI[🖥️ Web Interface<br/>Thymeleaf Templates]:::frontend
        API[🔌 REST API<br/>Spring Controllers]:::api
    end

    %% Service Layer
    subgraph "⚙️ Business Service Layer"
        PS[📦 Purchase Service<br/>Order Processing]:::service
        SS[🏪 Supplier Service<br/>Vendor Management]:::service
        IS[📊 Inventory Service<br/>Stock Control]:::service
        US[👤 User Service<br/>Authentication]:::service
    end

    %% Data Access Layer
    subgraph "💾 Data Access Layer"
        PR[📁 Purchase Repository<br/>JPA/Hibernate]:::repository
        SR[📁 Supplier Repository<br/>JPA/Hibernate]:::repository
        IR[📁 Inventory Repository<br/>JPA/Hibernate]:::repository
        UR[📁 User Repository<br/>JPA/Hibernate]:::repository
    end

    %% Database Layer
    subgraph "🗄️ Persistence Layer"
        DB[(💽 MySQL Database<br/>Primary Storage)]:::database
    end

    %% External Systems
    subgraph "🌐 External Services"
        EMAIL[📧 Email Service<br/>Notifications]:::external
        PAYMENT[💳 Payment Gateway<br/>Processing]:::external
        VENDOR[🏭 Vendor APIs<br/>Integration]:::external
    end

    %% Message Infrastructure
    subgraph "📨 Messaging Layer"
        QUEUE[📬 Message Queue<br/>Async Processing]:::messaging
    end

    %% Primary Flow
    UI --> API
    API --> PS
    API --> SS
    API --> IS
    API --> US

    %% Service to Repository
    PS --> PR
    SS --> SR
    IS --> IR
    US --> UR

    %% Repository to Database
    PR --> DB
    SR --> DB
    IR --> DB
    UR --> DB

    %% External Integrations
    PS --> EMAIL
    PS --> PAYMENT
    SS --> VENDOR
    PS --> QUEUE
    QUEUE --> EMAIL

    %% Inter-service Communication
    PS -.->|"Stock Check"| IS
    PS -.->|"Supplier Info"| SS
    PS -.->|"User Validation"| US
    SS -.->|"Inventory Update"| IS

    %% Styling Classes - Subtle Professional Colors
    classDef frontend fill:#e0f2fe,stroke:#0277bd,stroke-width:2px,color:#01579b
    classDef api fill:#e8f5e8,stroke:#388e3c,stroke-width:2px,color:#1b5e20
    classDef service fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#e65100
    classDef repository fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#4a148c
    classDef database fill:#ffebee,stroke:#d32f2f,stroke-width:2px,color:#b71c1c
    classDef external fill:#f5f5f5,stroke:#616161,stroke-width:2px,color:#424242
    classDef messaging fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#01579b
