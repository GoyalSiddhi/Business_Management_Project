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
