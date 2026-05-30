# ABC Retails - E-Commerce Platform

ABC Retails is a comprehensive e-commerce platform consisting of two main applications:

1. **ABCRetails** - ASP.NET Core MVC Web Application
2. **ABCRetailsFunctions** - Azure Functions API Backend

## Project Overview

This project implements a complete retail management system with product catalog, shopping cart, order management, and cloud-based serverless backend functionality. The architecture follows a microservices pattern with a web interface and cloud-native processing capabilities.

### Technology Stack

- **Frontend/Web Application**: ASP.NET Core 9.0 MVC with C# (54.7% of repo)
- **Backend API**: Azure Functions (.NET 8.0)
- **Frontend UI**: HTML (38.3%) and CSS (4.5%)
- **Database**: SQL Server (T-SQL: 1.6%)
- **Cloud Platform**: Microsoft Azure
- **Additional**: JavaScript (0.9%)

### Key Technologies
- Entity Framework Core 9.0
- Azure Storage (Blobs, Tables, Queues, File Shares)
- Azure Functions Worker Runtime
- ASP.NET Core Authentication (Cookie-based)
- Dependency Injection & Configuration Management

---

## 1. ABCRetails - Web Application

### Overview
The primary web application providing the user interface and business logic for the e-commerce platform.

**Location**: `ABCRetails/ABCRetails/`  
**Framework**: ASP.NET Core 9.0  
**Pattern**: MVC (Model-View-Controller)

### Architecture

```
ABCRetails/
├── Controllers/          # Request handlers
├── Models/              # Data structures
├── Services/            # Business logic
├── Views/               # UI Templates
├── Data/                # Database context
├── Properties/          # Project settings
├── wwwroot/             # Static assets (CSS, JS, images)
└── Program.cs           # Application entry point
```

### Controllers

#### 1. **HomeController**
- **Endpoints**: Home page, error handling, dashboard
- **Responsibilities**: Main navigation, general UI rendering
- **Key Features**: Index page, error pages, accessibility features

#### 2. **LoginController**
- **Endpoints**: User authentication, login/logout
- **Responsibilities**: 
  - User credential validation
  - Authentication state management (Cookie-based)
  - Session management
  - User role assignment (Admin/Customer)
- **Login Path**: `/Login`
- **Logout Path**: `/Login/Logout`
- **Access Denied Path**: `/Home/AccessDenied`
- **Session Timeout**: 2 hours

#### 3. **ProductController**
- **Endpoints**: Product listing, product details, search
- **Responsibilities**:
  - Display available products
  - Handle product filtering and search
  - Product information retrieval
  - Category management

#### 4. **CartController**
- **Endpoints**: Add to cart, view cart, update quantities, remove items, checkout
- **Responsibilities**:
  - Shopping cart management
  - Item quantity management
  - Cart persistence
  - Checkout process initiation
- **Size**: 12,052 bytes (largest controller)

#### 5. **CustomerController**
- **Endpoints**: Customer profile, address management, order history, preferences
- **Responsibilities**:
  - Customer profile management
  - Address management
  - Customer information updates
  - Order history viewing
  - Preference settings

#### 6. **OrderController**
- **Endpoints**: Order creation, order tracking, order history, cancellation, returns
- **Responsibilities**:
  - Order processing
  - Payment processing coordination
  - Order status tracking
  - Order fulfillment management
  - Return/exchange handling
- **Size**: 13,921 bytes (largest controller)
- **Integration**: Communicates with Azure Functions for backend processing

#### 7. **UploadController**
- **Endpoints**: File upload, file management, document handling
- **Responsibilities**:
  - File upload handling
  - File validation
  - Azure Blob Storage integration
  - File retrieval and management

### Data Models

#### 1. **User**
```csharp
- UserId (PK)
- Username
- Email
- PasswordHash
- Role (Admin/Customer)
- CreatedAt
- UpdatedAt
```

#### 2. **Customer**
```csharp
- CustomerId (PK)
- UserId (FK)
- FirstName
- LastName
- PhoneNumber
- ShippingAddress
- BillingAddress
- CreatedAt
- UpdatedAt
```

#### 3. **Product**
```csharp
- ProductId (PK)
- ProductName
- Description
- Price
- StockQuantity
- Category
- ImageUrl
- CreatedAt
- UpdatedAt
```

#### 4. **Cart**
```csharp
- CartId (PK)
- CustomerId (FK)
- CreatedAt
- UpdatedAt
```

#### 5. **Order**
```csharp
- OrderId (PK)
- CustomerId (FK)
- OrderDate
- Status
- TotalAmount
- ShippingAddress
- PaymentMethod
- CreatedAt
- UpdatedAt
```

#### 6. **FileUploadModel**
```csharp
- FileId
- FileName
- FileType
- FileSize
- UploadedBy (FK to User)
- UploadDate
```

### Services

#### 1. **IFunctionsApiService**
- **Purpose**: Communication bridge with Azure Functions backend
- **Endpoints**:
  - Product operations (CRUD)
  - Order operations (CRUD)
  - Customer operations (CRUD)
  - Inventory management
  - Queue-based async operations
- **Configuration**: `FunctionsBaseUrl` from `appsettings.json`
- **Size**: 32,364 bytes (comprehensive API interface)

#### 2. **FunctionApiService**
- **Implementation** of `IFunctionsApiService`
- **HttpClient Configuration**:
  - Base URL: `https://abcretailsfunctions-g8h2g5b4fygxd3ad.southafricanorth-01.azurewebsites.net/api`
  - Default headers: Accept: application/json
- **Error Handling**: Comprehensive exception handling for API calls
- **Size**: 2,295 bytes

#### 3. **ICustomerSyncService**
- **Purpose**: Customer data synchronization
- **Responsibilities**:
  - Sync customer data with Azure Functions
  - Maintain data consistency
  - Handle customer-related business logic
- **Size**: 4,045 bytes

### Configuration

#### **appsettings.json**
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "FunctionsBaseUrl": "https://abcretailsfunctions-g8h2g5b4fygxd3ad.southafricanorth-01.azurewebsites.net/api",
  "ConnectionStrings": {
    "AuthDb": "[SQL Server Connection String]"
  }
}
```

#### **appsettings.Development.json**
- Development-specific logging and configuration

### Database Context

**DbContext**: `AuthDbContext`
- **Database**: SQL Server
- **Connection String**: `AuthDb` from configuration
- **Entities**:
  - Users
  - Customers
  - Products
  - Orders
  - Carts
  - Files

### Authentication & Authorization

- **Scheme**: Cookie Authentication
- **Configuration**:
  - Login path: `/Login`
  - Logout path: `/Login/Logout`
  - Access denied path: `/Home/AccessDenied`
  - Session timeout: 2 hours
- **Roles**: Admin, Customer
- **Middleware**: Authentication & Authorization middleware enabled

### Project Dependencies

- **Azure SDKs**:
  - `Azure.Data.Tables` (v12.11.0)
  - `Azure.Storage.Blobs` (v12.25.0)
  - `Azure.Storage.Files.Shares` (v12.23.0)
  - `Azure.Storage.Queues` (v12.23.0)

- **Entity Framework**:
  - `Microsoft.EntityFrameworkCore.SqlServer` (v9.0.3)
  - `Microsoft.EntityFrameworkCore.Tools` (v9.0.3)

- **ASP.NET Core**:
  - `Microsoft.AspNetCore.Authentication.Cookies` (v2.3.0)
  - `Microsoft.VisualStudio.Web.CodeGeneration.Design` (v9.0.0)

### Static Files

**Location**: `wwwroot/`

Contains:
- CSS stylesheets
- JavaScript files
- Images and assets
- Vendor libraries

### Database Initialization

On application startup:
1. Database is created if it doesn't exist
2. Default users are seeded:
   - **Admin User**: 
     - Username: `admin01`
     - Email: `admin@abcretail.com`
     - Role: Admin
   - **Customer User**:
     - Username: `customer1`
     - Email: `customer1@gmail.com`
     - Role: Customer

---

## 2. ABCRetailsFunctions - Azure Functions API

### Overview
Serverless backend API providing cloud-native processing for orders, products, customers, and file handling.

**Location**: `ABCRetails/ABCRetailsFunctions/`  
**Framework**: Azure Functions Worker Runtime v4  
**Language**: C# (.NET 8.0)

### Architecture

```
ABCRetailsFunctions/
├── Functions/           # Azure Function implementations
├── Entities/            # Data models
├── Models/              # Request/Response models
├── Helpers/             # Utility functions
├── Properties/          # Project metadata
├── Program.cs           # Function host configuration
└── host.json            # Function runtime configuration
```

### Azure Functions

#### 1. **Blobfunction.cs**
- **Purpose**: Azure Blob Storage operations
- **Responsibilities**:
  - File upload to blob storage
  - File download from blob storage
  - File deletion
  - Blob metadata management
- **Trigger**: HTTP triggers for file operations
- **Storage Integration**: Azure Blob Storage
- **Size**: 1,664 bytes

#### 2. **CustomersFunctions.cs**
- **Purpose**: Customer data management
- **Responsibilities**:
  - Create new customers
  - Retrieve customer information
  - Update customer details
  - Delete customers
  - List all customers
- **HTTP Triggers**: POST, GET, PUT, DELETE
- **Storage**: Azure Table Storage for customer data
- **Size**: 4,173 bytes

#### 3. **OrdersFunctions.cs**
- **Purpose**: Order processing and management
- **Responsibilities**:
  - Create new orders
  - Retrieve order details
  - Update order status
  - List customer orders
  - Order cancellation
  - Order fulfillment coordination
- **HTTP Triggers**: POST, GET, PUT, DELETE
- **Queue Integration**: Communicates with queue processor
- **Size**: 8,531 bytes (comprehensive order management)

#### 4. **ProductsFunctions.cs**
- **Purpose**: Product catalog management
- **Responsibilities**:
  - Add new products
  - Retrieve product catalog
  - Update product information
  - Delete products
  - Inventory management
  - Search and filter products
- **HTTP Triggers**: POST, GET, PUT, DELETE
- **Storage**: Azure Table Storage for products
- **Size**: 7,769 bytes

#### 5. **QueueProcessorFunctions.cs**
- **Purpose**: Asynchronous job processing
- **Responsibilities**:
  - Process order queues
  - Handle batch operations
  - Asynchronous notifications
  - Background task processing
- **Trigger**: Azure Storage Queue triggers
- **Use Cases**:
  - Order confirmation emails
  - Inventory updates
  - Batch data processing
- **Size**: 3,777 bytes

#### 6. **UploadsFunctions.cs**
- **Purpose**: File upload and processing
- **Responsibilities**:
  - Handle multipart file uploads
  - File validation and scanning
  - Generate file metadata
  - Store in Azure Blob Storage
  - Generate download links
  - File cleanup/deletion
- **HTTP Trigger**: Multipart form data
- **Storage**: Azure Blob Storage, Azure Tables
- **Queue Integration**: May queue files for further processing
- **Size**: 10,080 bytes (largest function)

### Configuration

#### **host.json**
```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "samplingSettings": {
        "isEnabled": true,
        "maxTelemetryItemsPerSecond": 20
      }
    }
  }
}
```

### Models & Entities

**Entities Folder**: Data transfer objects and entity definitions
- Customer entities
- Order entities
- Product entities
- Upload entities
- Queue message models

**Models Folder**: Request/Response models
- Request DTOs
- Response DTOs
- API contracts

### Helpers

**Helpers Folder**: Utility functions
- Validation helpers
- Serialization utilities
- Error handling helpers
- Logging utilities

### Azure Resources Integration

#### **Azure Table Storage**
- Customer data storage
- Product catalog
- Order records
- Metadata storage

#### **Azure Blob Storage**
- File uploads
- Product images
- Customer documents
- Backup storage

#### **Azure Storage Queues**
- Asynchronous job queue
- Order processing queue
- Notification queue
- Background task queue

#### **Azure Application Insights**
- Performance monitoring
- Application telemetry
- Error tracking
- Logging

### Project Dependencies

- **Azure Functions**:
  - `Microsoft.Azure.Functions.Worker` (v1.22.0)
  - `Microsoft.Azure.Functions.Worker.Sdk` (v1.17.0)
  - `Microsoft.Azure.Functions.Worker.Extensions.Http` (v3.1.0)

- **Storage Extensions**:
  - `Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs` (v6.2.0)
  - `Microsoft.Azure.Functions.Worker.Extensions.Tables` (v1.2.1)
  - `Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues` (v5.2.0)

- **Azure SDKs**:
  - `Azure.Data.Tables` (v12.8.3)
  - `Azure.Storage.Blobs` (v12.23.0)
  - `Azure.Storage.Queues` (v12.19.1)

- **ASP.NET Core**:
  - `Microsoft.AspNetCore.WebUtilities` (v2.2.0)
  - `Microsoft.AspNetCore.Http.Features` (v2.2.0)

---

## Integration Between Applications

### Communication Flow

1. **Web Application** → **Azure Functions**
   - HTTP requests via `FunctionsApiService`
   - Base URL: `https://abcretailsfunctions-g8h2g5b4fygxd3ad.southafricanorth-01.azurewebsites.net/api`

2. **Azure Functions** → **Azure Storage**
   - Direct access to Table Storage, Blob Storage, Queues

3. **Azure Functions** → **Queue Processing**
   - Asynchronous background job execution
   - Order confirmations and notifications

### Data Flow

```
User (Web Browser)
    ↓
ASP.NET Core MVC Web App
    ↓
Controllers & Services
    ↓
FunctionsApiService (HTTP)
    ↓
Azure Functions API
    ↓
Azure Storage Services
    ↓
Database / Blob / Tables
```

---

## Deployment

### Web Application
- **Platform**: Azure App Service
- **Runtime**: .NET 9.0
- **Location**: South Africa North

### Azure Functions
- **Hosting**: Azure Functions (Serverless)
- **Runtime**: .NET 8.0 Isolated Worker
- **Version**: Azure Functions v4
- **Location**: South Africa North
- **URL**: `abcretailsfunctions-g8h2g5b4fygxd3ad.southafricanorth-01.azurewebsites.net`

### Database
- **SQL Server**: Azure SQL Database
- **Server**: `st104057abcretailsdb.database.windows.net`
- **Database**: `ABCRetailsDB`
- **User**: `St10450570`

---

## Getting Started

### Prerequisites
- .NET 9.0 SDK (for Web Application)
- .NET 8.0 SDK (for Azure Functions)
- Visual Studio 2022 or VS Code
- Azure CLI
- Git

### Setup Instructions

#### 1. Clone Repository
```bash
git clone https://github.com/Chuma-Makhathini/Projects.git
cd Projects/ABCRetails
```

#### 2. Web Application Setup
```bash
cd ABCRetails
# Restore dependencies
dotnet restore

# Update database
dotnet ef database update

# Run application
dotnet run
```

#### 3. Azure Functions Setup
```bash
cd ../ABCRetailsFunctions
# Restore dependencies
dotnet restore

# Run functions locally
func start
```

### Configuration

Update `appsettings.json`:
```json
{
  "FunctionsBaseUrl": "http://localhost:7071/api",
  "ConnectionStrings": {
    "AuthDb": "Server=YOUR_SERVER;Initial Catalog=YOUR_DB;User ID=YOUR_USER;Password=YOUR_PASSWORD;"
  }
}
```

---

## Development Guidelines

### Code Organization
- **Controllers**: Handle HTTP requests and coordinate responses
- **Models**: Represent data structures
- **Services**: Contain business logic
- **Data**: Database context and migrations

### Authentication
- Users must be authenticated before accessing most features
- Admin roles have access to management functions
- Customer roles have access to shopping features

### Error Handling
- Proper HTTP status codes
- Meaningful error messages
- Logging of exceptions
- User-friendly error pages

### Security
- SQL injection prevention (Entity Framework)
- Cross-site scripting (XSS) protection
- CSRF token validation
- Secure password hashing
- HTTPS enforcement

---

## Testing

### Unit Tests
- Create test projects for each layer
- Test service methods
- Test controller logic
- Mock external dependencies

### Integration Tests
- Test database interactions
- Test Azure Functions
- Test API endpoints
- Test authentication flow

---

## Troubleshooting

### Common Issues

**Connection String Error**
- Verify SQL Server connection string in `appsettings.json`
- Check database credentials
- Ensure database server is accessible

**Azure Functions Not Responding**
- Verify Azure Functions is running
- Check `FunctionsBaseUrl` configuration
- Review Application Insights logs

**Authentication Issues**
- Clear browser cookies
- Check user roles in database
- Verify login credentials

---

## Support & Contact

For questions or issues:
- Review existing documentation
- Check GitHub Issues
- Contact project maintainer: Chuma-Makhathini

---

## License

This project is provided as-is for educational and commercial purposes.

**Course**: CLDV6212 - Part 3  
**Student ID**: ST10450570

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-05-30 | Initial release with ABCRetails web app and Azure Functions backend |
