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
graph TD
    User[Web Browser] --> Controller[Spring MVC Controllers]
    
    Controller --> HomeController[Home Controller]
    Controller --> UserController[User Controller]
    Controller --> AdminController[Admin Controller]
    Controller --> ProductController[Product Controller]
    Controller --> OrderController[Order Controller]
    
    HomeController --> ThymeleafEngine[Thymeleaf Template Engine]
    UserController --> UserService[User Service]
    AdminController --> AdminService[Admin Service]
    ProductController --> ProductService[Product Service]
    OrderController --> OrderService[Order Service]
    
    UserService --> UserRepository[User Repository]
    AdminService --> AdminRepository[Admin Repository]
    ProductService --> ProductRepository[Product Repository]
    OrderService --> OrderRepository[Order Repository]
    
    UserRepository --> MySQL[(MySQL Database)]
    AdminRepository --> MySQL
    ProductRepository --> MySQL
    OrderRepository --> MySQL
    
    ThymeleafEngine --> Templates[HTML Templates]
    Templates --> StaticResources[Static Resources]
    
    UserEntity[User Entity] -.-> UserRepository
    AdminEntity[Admin Entity] -.-> AdminRepository
    ProductEntity[Product Entity] -.-> ProductRepository
    OrderEntity[Order Entity] -.-> OrderRepository
    
    ExceptionHandler[Global Exception Handler] --> ErrorPages[Error Templates]
