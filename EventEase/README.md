# EventEase

A comprehensive event management application designed to streamline the planning, organization, and execution of events. EventEase provides powerful tools for managing attendees, scheduling, venues, and all aspects of event coordination from a single, intuitive platform.

## Overview

EventEase is a full-featured event management system that enables organizations to plan, execute, and track events efficiently. Whether managing corporate conferences, seminars, social gatherings, or large-scale events, EventEase provides the tools necessary to handle registrations, scheduling, communications, and reporting with ease.

## Key Features

- **Event Creation & Management**: Create and configure events with detailed settings and customization options
- **Attendee Management**: Register, track, and communicate with attendees
- **Scheduling & Timelines**: Organize event schedules, sessions, and timelines
- **Venue Management**: Manage multiple venues and event locations
- **Registration System**: Streamlined attendee registration and check-in processes
- **Communications**: Built-in messaging and notification system for attendees
- **Reporting & Analytics**: Generate comprehensive reports on event performance and attendance
- **Dashboard**: Real-time overview of event status and key metrics

## Folder Structure

```
EventEase/
├── Models/                       # Data models and entities
├── Controllers/                  # Application logic and request handling
├── Views/                        # User interface templates and pages
├── Services/                     # Business logic and service layer
├── Data/                         # Database context and migrations
├── Pages/                        # Application pages and components
├── wwwroot/                      # Static files (CSS, JavaScript, images)
│   ├── css/                      # Stylesheets
│   ├── js/                       # Client-side scripts
│   └── images/                   # Image assets
├── appsettings.json             # Application configuration
├── program.cs                    # Application startup
└── README.md                     # This file
```

## System Requirements

- **Operating System**: Windows, macOS, or Linux
- **Runtime**: .NET 6.0 or later
- **Database**: SQL Server 2019 or later (or compatible database)
- **IDE**: Visual Studio 2022 or Visual Studio Code (recommended)
- **Browser**: Modern web browser (Chrome, Firefox, Edge, Safari)

## Installation

### Prerequisites

1. Ensure .NET 6.0 or later is installed
2. SQL Server or compatible database installed and configured
3. Git for version control

### Setup Steps

1. Clone the repository
   ```
   git clone https://github.com/Chuma-Makhathini/Projects.git
   cd Projects/EventEase
   ```

2. Restore NuGet packages
   ```
   dotnet restore
   ```

3. Configure the database connection in `appsettings.json`
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=YOUR_SERVER;Database=EventEaseDB;Trusted_Connection=true;"
   }
   ```

4. Apply database migrations
   ```
   dotnet ef database update
   ```

5. Build the application
   ```
   dotnet build
   ```

6. Run the application
   ```
   dotnet run
   ```

The application will be available at `https://localhost:5001` (or the configured port).

## Configuration

### Application Settings

Customize the application by editing `appsettings.json`:

- **Database Connection**: Configure your SQL Server connection string
- **Email Settings**: Configure SMTP for event notifications
- **Authentication**: Set up user authentication and authorization
- **API Keys**: Configure third-party service integrations

### Environment Variables

Set the following environment variables for sensitive configurations:

```
ASPNETCORE_ENVIRONMENT=Development|Production
DATABASE_CONNECTION_STRING=your_connection_string
SMTP_PASSWORD=your_email_password
```

## Usage Guide

### Getting Started

1. **Create an Event**
   - Navigate to "New Event"
   - Fill in event details (name, date, location, description)
   - Configure event settings and permissions

2. **Add Attendees**
   - Create registration forms
   - Import attendee lists or enable online registration
   - Track RSVPs and confirmations

3. **Manage Schedule**
   - Add sessions and speakers
   - Set time slots and durations
   - Organize track schedules

4. **Configure Venue**
   - Add venue information
   - Set capacity and layout
   - Manage seating arrangements

5. **Send Communications**
   - Create event announcements
   - Send notifications to attendees
   - Track email performance

### Main Features

#### Dashboard
- View event overview and key metrics
- Monitor registration status
- Track attendance and engagement

#### Event Management
- Create multiple events
- Configure event details and permissions
- Manage event status and lifecycle

#### Attendee Management
- Register and manage attendees
- Track attendance
- Send targeted communications
- Export attendee data

#### Reporting
- Generate attendance reports
- Create financial summaries
- Analyze event performance
- Export data for external analysis

## Usage Examples

### Creating an Event

```
Event Name: Tech Conference 2026
Date: June 15-17, 2026
Location: Convention Center, City
Capacity: 500 attendees
Registration: Online
Status: Planning
```

### Registering Attendees

```
First Name: John
Last Name: Doe
Email: john.doe@example.com
Company: Tech Corp
Ticket Type: General Admission
Dietary Requirements: Vegetarian
```

### Sending Event Announcement

```
Subject: Tech Conference 2026 - Final Reminders
Recipients: All Registered Attendees
Content: Important updates about schedule and logistics
Send Date: 1 day before event
```

## API Endpoints

The application provides RESTful APIs for integration:

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/events` | List all events |
| POST | `/api/events` | Create new event |
| GET | `/api/events/{id}` | Get event details |
| PUT | `/api/events/{id}` | Update event |
| DELETE | `/api/events/{id}` | Delete event |
| GET | `/api/events/{id}/attendees` | List event attendees |
| POST | `/api/events/{id}/attendees` | Register attendee |
| GET | `/api/events/{id}/reports` | Generate event report |

## Database Schema

Key tables in the EventEase database:

- **Events**: Core event information
- **Attendees**: Event attendee records
- **Sessions**: Event sessions and presentations
- **Venues**: Venue and location information
- **Registrations**: Attendee registration details
- **Communications**: Event messages and notifications
- **Reports**: Event analytics and reporting data

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Database connection fails | Verify connection string in `appsettings.json` and SQL Server is running |
| Pages not loading | Clear browser cache and restart the application |
| Email notifications not sending | Check SMTP configuration and email service credentials |
| Registration form not appearing | Verify event is in correct status and registration is enabled |
| Reports showing no data | Ensure event has completed and attendees have checked in |
| Performance issues | Check database indexes and server resources |

## Technology Stack

- **Backend**: C# (.NET 6.0)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: T-SQL, SQL Server
- **UI Framework**: ASP.NET Core MVC
- **Architecture**: Model-View-Controller (MVC)

## Deployment

### Production Deployment

1. Update `appsettings.Production.json` with production settings
2. Set `ASPNETCORE_ENVIRONMENT=Production`
3. Publish the application
   ```
   dotnet publish -c Release
   ```
4. Deploy to hosting platform (Azure, IIS, Docker, etc.)
5. Configure database backups and monitoring

## Support & Feedback

For issues, feature requests, or feedback, please open an issue in the repository or contact the development team.

## License

This project is provided for professional use in event management and organization.

## Contributing

Contributions are welcome. Please follow the project's coding standards and submit pull requests with detailed descriptions of changes.
