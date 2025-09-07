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
