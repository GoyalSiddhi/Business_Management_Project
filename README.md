# Business Management Project

## 💡 Overview
A comprehensive business management web application built with Spring Boot and Thymeleaf. This system provides role-based access control for admins and users, featuring product management, order processing, user administration, and a complete web interface for business operations management.

## 🛠️ Tech Stack
- **Language(s):** Java 17
- **Framework(s):** Spring Boot 3.1.3, Spring MVC, Spring Data JPA, Thymeleaf
- **Infrastructure/Orchestration:** Maven, MySQL Database
- **Dependencies:** Spring Boot Starter Web, Spring Boot Starter Data JPA, Spring Boot Starter Thymeleaf, Spring Boot Starter Validation, MySQL Connector, Spring Boot DevTools

## 🧩 Functional Components
- **User Management**: Complete CRUD operations for user registration, authentication, and profile management
- **Admin Panel**: Administrative interface for managing users, products, and orders with full CRUD capabilities
- **Product Catalog**: Product management system with add, update, delete, and view functionalities
- **Order Processing**: Order creation, tracking, and management system with success notifications
- **Authentication System**: Role-based access control distinguishing between admin and regular users
- **Web Interface**: Responsive HTML templates with navigation, forms, and data display pages
- **Exception Handling**: Custom exception handling with user-friendly error pages

## 🔗 Integrations
- **Database**: MySQL database for persistent data storage
- **ORM**: Hibernate/JPA for database abstraction and mapping
- **Template Engine**: Thymeleaf for server-side rendering of HTML pages
- **Validation**: Spring Boot Validation for form input validation
- **Development Tools**: Spring Boot DevTools for hot reloading during development

## 🚀 Execution/Deployment
- **Local Development**: Run via `mvn spring-boot:run` or execute the main class `BusinessProjectApplication`
- **Build**: Maven build system with `mvn clean package`
- **Database Setup**: MySQL server required with database `businessproject`
- **Port Configuration**: Application runs on port 2330
- **Environment**: Configured for development with auto-restart capabilities

## 🧪 Testing
- **Testing Tools**: Spring Boot Starter Test (includes JUnit, Mockito, Spring Test)
- **Types of Tests**: Unit tests for service layer, integration tests for controllers
- **Test Structure**: Organized under `src/test/java` following standard Maven structure

## 📈 Metrics/Monitoring
- **Development Monitoring**: Spring Boot DevTools for development-time monitoring
- **Database Monitoring**: Hibernate SQL logging enabled
- **Application Health**: Spring Boot Actuator endpoints available
- **Error Handling**: Custom exception handling with dedicated error pages

## 🏗️ Architecture Diagram

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#2563eb',
    'primaryTextColor': '#ffffff',
    'primaryBorderColor': '#1d4ed8',
    'lineColor': '#374151',
    'secondaryColor': '#10b981',
    'tertiaryColor': '#f59e0b',
    'background': '#f8fafc',
    'mainBkg': '#ffffff',
    'secondBkg': '#e5e7eb',
    'tertiaryBkg': '#fef3c7'
  }
}}%%

flowchart TD
    %% User Layer
    subgraph "👥 User Interface Layer"
        UI[🖥️ Web Interface<br/>Thymeleaf Templates]:::frontend
        API[🔌 REST API<br/>Controllers]:::api
    end

    %% Service Layer
    subgraph "🏗️ Business Logic Layer"
        PS[📦 Purchase Service<br/>Business Logic]:::service
        SS[📦 Supplier Service<br/>Vendor Management]:::service
        IS[📦 Inventory Service<br/>Stock Management]:::service
        US[📦 User Service<br/>Authentication]:::service
    end

    %% Data Access Layer
    subgraph "💾 Data Access Layer"
        PR[🗂️ Purchase Repository<br/>JPA/Hibernate]:::repository
        SR[🗂️ Supplier Repository<br/>JPA/Hibernate]:::repository
        IR[🗂️ Inventory Repository<br/>JPA/Hibernate]:::repository
        UR[🗂️ User Repository<br/>JPA/Hibernate]:::repository
    end

    %% Database Layer
    subgraph "🗃️ Data Persistence Layer"
        DB[(🗄️ MySQL Database<br/>Primary Storage)]:::database
    end

    %% External Systems
    subgraph "🌐 External Integrations"
        EMAIL[📧 Email Service<br/>Notifications]:::external
        PAYMENT[💳 Payment Gateway<br/>Transactions]:::external
        SUPPLIER_API[🏪 Supplier APIs<br/>External Vendors]:::external
    end

    %% Message Queue (if implemented)
    subgraph "📨 Messaging Infrastructure"
        QUEUE[📬 Message Queue<br/>Async Processing]:::queue
    end

    %% User Interactions
    UI --> API
    API --> PS
    API --> SS
    API --> IS
    API --> US

    %% Service Interactions
    PS --> PR
    PS --> SR
    PS --> IR
    SS --> SR
    IS --> IR
    US --> UR

    %% Database Connections
    PR --> DB
    SR --> DB
    IR --> DB
    UR --> DB

    %% External Service Calls
    PS --> EMAIL
    PS --> PAYMENT
    SS --> SUPPLIER_API
    PS --> QUEUE
    QUEUE --> EMAIL

    %% Cross-Service Dependencies
    PS -.-> SS
    PS -.-> IS
    PS -.-> US

    %% Styling Classes
    classDef frontend fill:#3b82f6,stroke:#1d4ed8,stroke-width:2px,color:#ffffff
    classDef api fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef service fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef repository fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef database fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef external fill:#6b7280,stroke:#4b5563,stroke-width:2px,color:#ffffff
    classDef queue fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    %% Data Flow Annotations
    PS -.->|"Purchase Orders"| QUEUE
    QUEUE -.->|"Order Confirmations"| EMAIL
    PS -.->|"Inventory Updates"| IS
    SS -.->|"Supplier Data"| PS
