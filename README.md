# CityInfo API

A RESTful Web API built with ASP.NET Core 6.0 that provides information about cities and their points of interest. This project demonstrates modern API development practices including authentication, authorization, logging, API versioning, and comprehensive documentation.

## 🚀 Features

- **City Management**: CRUD operations for cities and their details
- **Points of Interest**: Manage landmarks, museums, and other attractions for each city
- **File Management**: Upload and download city-related files (images, documents)
- **JWT Authentication**: Secure endpoints with token-based authentication
- **Authorization Policies**: Claim-based authorization (e.g., city-specific access)
- **API Versioning**: Support for multiple API versions
- **Swagger/OpenAPI**: Interactive API documentation
- **Structured Logging**: Serilog integration with file and console output
- **Entity Framework Core**: SQLite database with code-first migrations
- **AutoMapper**: Automatic object-to-object mapping
- **Content Negotiation**: Support for JSON and XML responses

## 📋 Prerequisites

Before running this project, ensure you have the following installed:

- [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0) or later
- A code editor (e.g., [Visual Studio](https://visualstudio.microsoft.com/), [Visual Studio Code](https://code.visualstudio.com/), or [JetBrains Rider](https://www.jetbrains.com/rider/))
- SQLite (included with .NET SDK)

## 🛠️ Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd CityInfo
```

### 2. Restore Dependencies

Navigate to the project directory and restore NuGet packages:

```bash
cd CityInfo.API
dotnet restore
```

### 3. Database Setup

The project uses SQLite with Entity Framework Core. The database file (`CityInfo.db`) should already exist, but if you need to recreate it or apply migrations:

```bash
# Apply migrations to create/update the database
dotnet ef database update

# (Optional) Create a new migration if you modify entities
dotnet ef migrations add <MigrationName>
```

### 4. Configuration

The application uses `appsettings.Development.json` for local development. Key configuration sections include:

- **ConnectionString**: SQLite database path
- **Authentication**: JWT settings (issuer, audience, secret key)
- **MailSettings**: Email configuration for notifications

> **Note**: The default JWT secret is for development only. Use a secure secret in production.

### 5. Run the Application

Start the API server:

```bash
dotnet run
```

The API will be available at:
- **HTTPS**: `https://localhost:7015`
- **HTTP**: `http://localhost:5015` (if configured)

### 6. Access Swagger UI

Once the application is running, navigate to:

```
https://localhost:7015/swagger
```

This provides an interactive interface to explore and test all API endpoints.

## 🔐 Authentication

The API uses JWT Bearer authentication. To access protected endpoints:

### 1. Obtain a Token

Send a POST request to `/api/authentication/authenticate` with valid credentials:

```json
{
  "userName": "your-username",
  "password": "your-password"
}
```

### 2. Use the Token

Include the token in the `Authorization` header for subsequent requests:

```
Authorization: Bearer <your-token>
```

In Swagger UI, click the **Authorize** button and enter `Bearer <your-token>`.

## 📁 Project Structure

```
CityInfo/
├── CityInfo.API/
│   ├── Controllers/          # API endpoints
│   │   ├── AuthenticationController.cs
│   │   ├── CitiesController.cs
│   │   ├── FilesController.cs
│   │   └── PointsOfInterestController.cs
│   ├── DbContexts/           # Entity Framework context
│   ├── Entities/             # Database entities
│   ├── Models/               # DTOs (Data Transfer Objects)
│   ├── Profiles/             # AutoMapper profiles
│   ├── Services/             # Business logic services
│   ├── Migrations/           # EF Core migrations
│   ├── Program.cs            # Application entry point
│   ├── appsettings.json      # Base configuration
│   ├── appsettings.Development.json  # Development settings
│   └── CityInfo.db           # SQLite database
└── README.md
```

## 🧪 Testing the API

### Using Swagger UI

1. Navigate to `https://localhost:7015/swagger`
2. Authenticate using the **Authorize** button
3. Expand any endpoint and click **Try it out**
4. Fill in the required parameters and click **Execute**

### Using cURL

```bash
# Get all cities
curl -X GET "https://localhost:7015/api/cities" -H "accept: application/json"

# Get a specific city
curl -X GET "https://localhost:7015/api/cities/1" -H "accept: application/json"

# Authenticate
curl -X POST "https://localhost:7015/api/authentication/authenticate" \
  -H "Content-Type: application/json" \
  -d '{"userName":"testuser","password":"testpass"}'
```

## 📝 API Endpoints

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|---------------|
| `/api/authentication/authenticate` | POST | Obtain JWT token | No |
| `/api/cities` | GET | Get all cities | Optional |
| `/api/cities/{id}` | GET | Get city by ID | Optional |
| `/api/cities` | POST | Create a new city | Yes |
| `/api/cities/{id}` | PUT | Update a city | Yes |
| `/api/cities/{id}` | DELETE | Delete a city | Yes |
| `/api/cities/{cityId}/pointsofinterest` | GET | Get POIs for a city | Optional |
| `/api/cities/{cityId}/pointsofinterest/{id}` | GET | Get specific POI | Optional |
| `/api/cities/{cityId}/pointsofinterest` | POST | Create a POI | Yes |
| `/api/cities/{cityId}/pointsofinterest/{id}` | PUT/PATCH | Update a POI | Yes |
| `/api/cities/{cityId}/pointsofinterest/{id}` | DELETE | Delete a POI | Yes |
| `/api/files` | GET/POST | Manage files | Varies |

## 🔧 Configuration Options

### Logging

Logs are written to:
- **Console**: Real-time output during development
- **File**: `logs/cityinfo.txt` (rolling daily logs)

Adjust log levels in `appsettings.Development.json`:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}
```

### API Versioning

The API supports versioning. Default version is `1.0`. Specify version in requests:

```
GET /api/cities?api-version=1.0
```

## 🚢 Deployment

### Production Configuration

1. Update `appsettings.Production.json` with production settings
2. Use a strong, unique JWT secret key
3. Configure a production-grade database (SQL Server, PostgreSQL, etc.)
4. Enable HTTPS and configure SSL certificates
5. Set appropriate CORS policies

### Build for Production

```bash
dotnet publish -c Release -o ./publish
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📧 Support

For questions or issues, please open an issue on the GitHub repository or contact the development team.

---

**Built with ❤️ using ASP.NET Core**
