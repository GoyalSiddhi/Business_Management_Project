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
    'primaryColor': '#4f46e5',
    'primaryTextColor': '#ffffff',
    'primaryBorderColor': '#3730a3',
    'lineColor': '#6b7280',
    'secondaryColor': '#059669',
    'tertiaryColor': '#dc2626',
    'background': '#ffffff',
    'mainBkg': '#f8fafc',
    'secondBkg': '#e2e8f0',
    'tertiaryBkg': '#fef2f2'
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

    %% Styling Classes
    classDef frontend fill:#4f46e5,stroke:#3730a3,stroke-width:2px,color:#ffffff
    classDef api fill:#059669,stroke:#047857,stroke-width:2px,color:#ffffff
    classDef service fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#ffffff
    classDef repository fill:#7c3aed,stroke:#6d28d9,stroke-width:2px,color:#ffffff
    classDef database fill:#dc2626,stroke:#b91c1c,stroke-width:2px,color:#ffffff
    classDef external fill:#6b7280,stroke:#4b5563,stroke-width:2px,color:#ffffff
    classDef messaging fill:#ea580c,stroke:#c2410c,stroke-width:2px,color:#ffffff
