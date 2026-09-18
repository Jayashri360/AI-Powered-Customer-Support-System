# AI-Powered Customer Support System

A backend-focused **Customer Support System** built with **ASP.NET Core Web API, .NET 10, Entity Framework Core, and SQL Server**, following **Clean Architecture** principles.

The project is designed as a real-world enterprise application that starts with traditional customer-support functionality and can later be extended with Generative AI, Semantic Search, RAG, AI Agents, Tool Calling, and other AI capabilities.

## 🎯 Project Overview

The system provides a centralized platform where customers can raise and track support requests related to products or services.

Support teams can review, assign, investigate, communicate, and resolve tickets while maintaining the complete history of each support request.

The application supports three primary user roles:

* **Customer**
* **Support Executive**
* **Administrator**

## ✨ Core Features

### Customer

Customers can:

* Register and authenticate
* View available products or services
* Create support tickets
* Select the related product or service
* Add ticket subject and description
* Upload screenshots or supporting documents
* View their own tickets
* Add comments
* View responses from the support team
* Track ticket status and history

### Support Executive

Support executives can:

* View assigned tickets
* Review ticket details and customer comments
* Access uploaded attachments
* Respond to customers
* Update ticket status
* Update ticket priority where permitted
* Resolve tickets
* Search Knowledge Base articles
* Review previous ticket history

### Administrator

Administrators can:

* Manage users
* Manage products and services
* Manage ticket categories
* Manage priorities and statuses
* Manage Knowledge Base articles
* Manage FAQs
* View support tickets
* Monitor support activity
* Review audit information

## 🎫 Ticket Management

Support tickets are the central business entity of the application.

A ticket can contain:

* Ticket Number
* Customer
* Product or Service
* Subject
* Description
* Category
* Priority
* Status
* Assigned Support Executive
* Created Date
* Updated Date
* Comments
* Attachments
* Assignment History
* Status History
* Audit Information

### Ticket Lifecycle

A simplified ticket workflow is:

```text
Open / Reopen
      ↓
   Assigned
      ↓
 In Progress
      ↓
   Resolved
      ↓
    Closed
```

The system maintains ticket history so changes and important actions can be tracked throughout the ticket lifecycle.

## 🛠️ Technology Stack

| Technology            | Purpose                           |
| --------------------- | --------------------------------- |
| .NET 10               | Application platform              |
| ASP.NET Core Web API  | REST API                          |
| C#                    | Primary programming language      |
| SQL Server            | Relational database               |
| Entity Framework Core | ORM                               |
| EF Core Code First    | Database modelling and migrations |
| Swagger / OpenAPI     | API documentation and testing     |
| JWT                   | Authentication                    |
| Visual Studio 2026    | Development environment           |

## 🏗️ Architecture

The solution follows **Clean Architecture** to separate business logic from frameworks and infrastructure concerns.

```text
CustomerSupportSystem
│
├── CustomerSupport.Domain
│
├── CustomerSupport.Application
│
├── CustomerSupport.Infrastructure
│
├── CustomerSupport.API
│
└── CustomerSupport.Tests
```

### Domain

The innermost layer containing the core business concepts and rules.

Typical components include:

```text
Entities
Enums
Constants
Domain Rules
Domain Exceptions
```

Example entities:

```text
User
Product
SupportTicket
TicketCategory
TicketPriority
TicketStatus
TicketComment
TicketAssignment
TicketAttachment
TicketHistory
KnowledgeBaseArticle
FAQ
RefreshToken
```

The Domain layer does not depend on ASP.NET Core, Entity Framework Core, SQL Server, Swagger, JWT libraries, or AI providers.

### Application

Contains application use cases and business workflows.

Typical components include:

```text
DTOs
Service Interfaces
Services
Repository Interfaces
Validators
Mappings
Application Exceptions
Pagination Models
Search / Filter Models
External Service Abstractions
```

Example use cases include:

* Register customer
* Authenticate user
* Create and update tickets
* Assign tickets
* Change ticket status
* Add comments
* Search and filter tickets
* Manage Knowledge Base articles
* Manage FAQs

The Application layer depends on the **Domain layer**, but remains independent of infrastructure technologies.

### Infrastructure

Provides implementations for interfaces and abstractions required by the Application layer.

Typical components include:

```text
DbContext
EF Core Configurations
Repository Implementations
SQL Server Integration
Database Migrations
Seed Data
File Storage
JWT Implementation
Password Hashing
External Service Implementations
```

The Infrastructure layer can depend on both the **Application** and **Domain** layers.

### API

The entry point and presentation layer of the application.

Typical components include:

```text
Controllers
Program.cs
Middleware
Global Exception Handling
Swagger / OpenAPI
Authentication
Authorization
CORS
Health Checks
Dependency Injection
```

Controllers receive HTTP requests and delegate business operations to the Application layer.

## 🔗 Dependency Flow

Clean Architecture dependency rules:

```text
                  ┌─────────────────────┐
                  │        API          │
                  └──────────┬──────────┘
                             │
                  ┌──────────▼──────────┐
                  │   Infrastructure    │
                  └──────────┬──────────┘
                             │
                  ┌──────────▼──────────┐
                  │    Application      │
                  └──────────┬──────────┘
                             │
                  ┌──────────▼──────────┐
                  │       Domain        │
                  └─────────────────────┘
```

The core principle is:

> Business logic should remain independent of databases, frameworks, APIs, user interfaces, and external services.

## 🔐 Authentication & Authorization

The application is designed to support:

* User registration
* Login
* JWT authentication
* Refresh tokens
* Role-Based Authorization
* Customer data isolation
* Protected API endpoints

A customer must only be able to access their own private support tickets.

## 📚 Knowledge Base & FAQs

The application contains a Knowledge Base for storing information about products, services, troubleshooting procedures, and common issues.

Frequently Asked Questions can also be maintained and searched.

These components will later provide trusted business knowledge for AI capabilities such as Semantic Search and RAG.

## 🤖 AI Roadmap

AI is intentionally introduced **after the core business application is established**.

Planned AI capabilities include:

### Ticket Summarization

Generate concise summaries of long tickets and conversations.

### Category Suggestions

Analyse ticket descriptions and suggest categories such as:

```text
Payment Issue
Login Issue
Billing Issue
Technical Issue
```

### Priority Suggestions

Analyse ticket content and recommend an appropriate priority.

### Suggested Responses

Generate response drafts that Support Executives can review before sending.

### Sentiment Analysis

Identify whether customer messages appear:

```text
Positive
Neutral
Frustrated
```

### Semantic Search

Search Knowledge Base content based on meaning rather than only exact keywords.

### Retrieval-Augmented Generation (RAG)

Answer support questions using trusted information retrieved from the application's Knowledge Base.

### Multimodal AI

Analyse uploaded content such as:

* Screenshots
* PDFs
* Documents

### Tool Calling

AI functionality can interact with approved application services rather than receiving unrestricted database access.

For example:

```text
User:
"What is the current status of ticket 1025?"

AI
 ↓
Approved Application Service
 ↓
Ticket Service
 ↓
Repository
 ↓
Database
```

### AI Agents

Future AI agents can perform controlled multi-step support workflows through existing application services.

## 🧠 Design Philosophy

The project deliberately separates **deterministic business logic** from **AI-assisted functionality**.

Operations such as:

* Authentication
* Authorization
* Database transactions
* Ticket creation
* Permission validation
* Business-rule enforcement
* Token generation
* File validation

remain normal application functionality.

AI is used where understanding, generation, semantic retrieval, or intelligent assistance provides additional value.

## 🗄️ Database

SQL Server stores business information including:

```text
Users
Products
Tickets
Categories
Priorities
Statuses
Comments
Attachments
Ticket History
Knowledge Base Articles
FAQs
Refresh Tokens
```

The database is managed through **Entity Framework Core Code First** and EF Core migrations.

## 🚀 Getting Started

### Prerequisites

Install:

* .NET 10 SDK
* SQL Server
* Visual Studio 2026 or another compatible IDE
* Git

### Clone the Repository

```bash
git clone <repository-url>
cd <repository-name>
```

### Restore Dependencies

```bash
dotnet restore
```

### Configure Database

Update the SQL Server connection string in the appropriate application configuration file.

Do not commit production credentials or secrets to the repository.

### Apply Database Migrations

```bash
dotnet ef database update
```

### Run the Application

```bash
dotnet run --project CustomerSupport.API
```

Open Swagger using the URL displayed by the application after startup.

## 🧪 API Testing

The APIs can initially be tested using:

* Swagger UI
* Postman

Swagger can be used to test request/response payloads, authentication, and protected endpoints without requiring a separate frontend application.

## 🗺️ Development Roadmap

```text
Project Architecture
        ↓
Domain Entities
        ↓
EF Core Configuration
        ↓
Database & Migrations
        ↓
Repository Layer
        ↓
Application Services
        ↓
DTOs & Validation
        ↓
REST APIs
        ↓
Authentication & Authorization
        ↓
Ticket Management
        ↓
Comments & Attachments
        ↓
Knowledge Base & FAQs
        ↓
Logging & Auditing
        ↓
Testing
        ↓
Semantic Search
        ↓
RAG
        ↓
Generative AI
        ↓
Tool Calling
        ↓
AI Agents
```

## 📌 Project Status

🚧 **Under Active Development**

The initial development focuses on building the traditional Customer Support System and establishing strong Clean Architecture boundaries.

AI functionality will be introduced progressively after the core application functionality is established.

## 📄 License

Add the appropriate license for this repository before public distribution.

---

**AI-Powered Customer Support System**
Built with **ASP.NET Core • .NET 10 • EF Core • SQL Server • Clean Architecture**
