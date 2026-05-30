# Contract Monthly Claim System

## Overview

A fully automated, production-ready enterprise application for managing contract-based monthly claims with comprehensive role-based access control, advanced reporting, and secure document handling. This system streamlines the entire claims lifecycle from submission through approval to payment processing.

## Architecture & Technical Stack

### 1. Database Integration & Entity Framework Core
- Full SQL Server database integration with Entity Framework Core
- `ApplicationDbContext.cs` with proper entity configurations and migrations
- Comprehensive database seeding via `DbInitializer.cs`
- Stored procedures and views for advanced reporting:
  - `vw_ClaimsSummary` - Comprehensive claims overview
  - `vw_ApprovedClaimsForPayment` - Payment processing view
  - `vw_MonthlyClaimsByDepartment` - Departmental analytics
  - `sp_GetLecturerPerformanceReport` - Performance metrics

### 2. Authentication & Authorization
- BCrypt.NET for secure password hashing with salt
- `IAuthenticationService` with robust password verification
- `UserSessionService` integrated with database context
- Comprehensive authorization checks across all controllers
- `CheckAuthorization()` helper methods in controllers
- Dedicated `AccessDenied` view for unauthorized access attempts

### 3. HR Management Module
Complete HR administration capabilities:

**User Management:**
- Full CRUD operations via `HRController.cs`
- Role-specific user creation and editing forms
- Automatic hourly rate management
- User activation/deactivation functionality
- Hard delete option for permanent user removal
- Email uniqueness validation

**HR Views:**
- `HR/Dashboard.cshtml` - HR overview with statistics
- `HR/Users.cshtml` - User management interface
- `HR/CreateUser.cshtml` - User creation form
- `HR/EditUser.cshtml` - User editing form
- `HR/Reports.cshtml` - Approved claims for payment processing
- `HR/AllClaims.cshtml` - Complete claims overview
- `HR/LecturerPerformance.cshtml` - Performance analytics

### 4. Automated Claim Processing
Fully automated system eliminating manual rate entry:

**Submission Automation:**
- Hourly rates automatically pulled from user profiles (configured by HR)
- Real-time total amount calculation: `TotalAmount = HoursWorked × HourlyRate`
- Validation prevents claims if hourly rate not set
- Maximum 180 hours per month validation
- Auto-calculation in both Create and Edit views

**Approval Workflow Automation:**
- Automated claim verification workflow
- Built-in approval/rejection logic with mandatory reviewer comments
- Claims escalation: Coordinator → Manager → Approved
- Real-time status tracking and updates
- Comprehensive reviewer comments system for audit trail

### 5. Advanced Reporting & PDF Generation
Professional report generation using QuestPDF:

**Report Types:**
- **Approved Claims Report (CSV/PDF):** Payment-ready claims with full details and approval information
- **All Claims Report (CSV/PDF):** Complete system overview with status breakdown and statistics
- **Contractor Performance Report (CSV/PDF):** Individual and aggregate performance metrics with success rates, total claims, hours, and amounts per contractor

**Professional Features:**
- Landscape/portrait layout options
- Color-coded headers and sections
- Comprehensive data tables with summaries
- South African Rand (ZAR) currency formatting
- Date-stamped file names for compliance

### 6. Enhanced User Interface & Experience

**Dashboard Features:**
- Real-time statistics via AJAX calls
- Dynamic dashboard cards with smooth animations
- Recent claims table with live updates
- Role-specific navigation and quick actions

**Claims Management:**
- Quick action buttons on Details page for Coordinators and Managers
- Modal dialogs for all reviewer actions (Verify, Approve, Reject, Return)
- Enhanced status tracking with color-coded badges
- Comprehensive error handling and user feedback
- Document encryption/decryption for secure file handling

**Visual Design:**
- Modern glassmorphism design with dark mode support
- 3D card effects and smooth transitions
- Gradient backgrounds and accent colors
- Fully responsive layout for all screen sizes
- Fixed header and footer with proper z-index management

### 7. Supporting Documents Management

**Flexible Document Handling:**
- Optional supporting document uploads during claim submission
- Clear indication of optional fields in the interface
- Enhanced user guidance throughout the application
- Secure document storage with encryption

**Claims Details Enhancement:**
- Coordinators can Verify, Return, or Reject claims directly from details page
- Managers can Approve or Reject claims from the details view
- Consistent modal-based workflow for all reviewer actions
- Reduced navigation requirements improving user efficiency

### 8. Service Layer Architecture

**Core Services:**
- `IUserService` / `UserService.cs` - User management operations
- `IClaimService` / `ClaimService.cs` - Claims processing and reporting
- `IFileEncryptionService` / `FileEncryptionService.cs` - Document security

**Key Operations:**
- `GetAllUsersAsync()` - User listing
- `GetContractorsAsync()` - Contractor-specific queries
- `CreateUserAsync()` / `UpdateUserAsync()` - User CRUD operations
- `GetApprovedClaimsAsync()` - Payment processing queries
- `GetAllClaimsAsync()` - Complete claims overview
- Performance metric calculations

### 9. Data Models & ViewModels

**ViewModels:**
- `UserCreateViewModel.cs` - User creation with validation
- `UserEditViewModel.cs` - User editing with optional password updates
- `PerformanceViewModel.cs` - Performance metrics display

**Data Models:**
- `ApplicationUser.cs` with computed properties
- Full navigation properties for all relationships
- Proper cascade delete behaviors
- Comprehensive data validation attributes

## Technical Highlights

### Code Quality
- Dependency injection throughout the application
- Comprehensive error handling with try-catch blocks
- Consistent async/await patterns
- SOLID principles in service design
- Repository pattern implementation via Entity Framework

### Security
- BCrypt password hashing with cryptographic salt
- AES-256 encryption for sensitive documents
- SQL injection protection via parameterized queries
- CSRF protection with anti-forgery tokens
- Session security with HttpOnly and Secure flags

### Performance Optimization
- Eager loading with `.Include()` to prevent N+1 queries
- Indexed database columns for faster searches
- Efficient AJAX calls for dashboard updates
- Optimized SQL queries with proper join strategies

### Validation & Testing
- Comprehensive model-level validation
- Client-side and server-side validation
- Business rule enforcement (hours, rates, file sizes)
- Role-based access control verification

## Project Structure

**Controllers:**
- `HRController.cs` - HR administration
- `ClaimsController.cs` - Claims management

**Views:**
- `HR/` folder with complete HR interface
- `Claims/` folder with claims management views
- `Shared/_StatusLabel.cshtml` - Reusable components

**Services:**
- `UserService.cs`
- `ClaimService.cs`
- `AuthenticationService.cs`
- `FileEncryptionService.cs`

**Database:**
- `ApplicationDbContext.cs`
- `DbInitializer.cs`
- Schema scripts

## Configuration

**appsettings.json:**
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=...;Database=ContractClaimSystemDB;..."
  }
}
```

**Program.cs Configuration:**
- Entity Framework DbContext registration
- Connection string configuration with retry logic
- Service interface registration
- Database initialization on startup
- Session middleware configuration

## Key Features

1. **Full Database Persistence** - SQL Server with Entity Framework Core
2. **User Management** - Complete CRUD operations with role assignment
3. **Automated Rate Management** - Administrator sets rates, users apply automatically
4. **Multi-Stage Approval Workflow** - Coordinator review → Manager approval → Payment ready
5. **Professional Reporting** - PDF/CSV export with comprehensive layouts
6. **Performance Analytics** - Success rates and detailed metrics
7. **Document Security** - AES encryption for all stored documents
8. **Role-Based Access Control** - Four distinct user roles with granular permissions
9. **Real-Time Calculations** - Automatic total amount computation based on hours and rates
10. **Audit Trail** - Complete history of reviewer actions and comments
11. **Flexible Document Upload** - Optional supporting documentation
12. **Streamlined Workflow** - Quick action buttons reduce navigation steps

## Getting Started

### Prerequisites
- .NET 6.0 or later
- SQL Server 2019 or later
- Visual Studio 2022 or VS Code

### Installation

1. Clone the repository
```bash
git clone <repository-url>
cd Contract_Monthly_Claim_System
```

2. Update database connection string in `appsettings.json`

3. Apply database migrations
```bash
dotnet ef database update
```

4. Run the application
```bash
dotnet run
```

5. Access the application at `https://localhost:5001`

## User Roles

- **Administrator (HR):** User management, rate configuration, system reports
- **Coordinator:** Claim verification and initial review
- **Manager:** Final approval of verified claims
- **Contractor:** Claim submission and status tracking

## Security Considerations

- All passwords are hashed using BCrypt with cryptographic salt
- Sensitive documents are encrypted with AES-256
- Session tokens are secure with HttpOnly and Secure flags
- All database queries use parameterized statements
- CSRF tokens protect all state-changing operations

## Support

For technical issues or feature requests, please create an issue in the repository.

## License

This project is proprietary software. All rights reserved.
