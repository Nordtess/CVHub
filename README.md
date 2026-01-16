<div align="center">

# 💼 CVHub: Professional Networking Done Right
**Where careers connect and talent shines—minus the corporate cringe.** A full-stack ASP.NET Core MVC platform built with Clean Architecture, wrapped in Razor views, and served with Docker on the side.

</div>

## 💡 Description
I built CVHub (a university project but I did 98% of it) to demonstrate how to architect a real-world, production-ready web application using modern .NET 8 patterns. It's a professional networking platform where users create detailed CV profiles, connect through messaging, collaborate on projects, and discover talent—all without the noise of traditional social networks.

This isn't just a CRUD playground—it's a showcase of **Clean Architecture**, **Domain-Driven Design**, and **containerized deployment**, proving that you can build scalable, maintainable web apps without sacrificing code quality.

### Key Architectural Highlights:

* **Clean Architecture Layers:** The project is split into three distinct layers—**Domain** (entities & business rules), **Infrastructure** (database & external concerns), and **WebApp** (presentation & controllers). Dependencies flow inward, making the core business logic immune to framework changes.
* **ASP.NET Identity Integration:** Secure authentication and authorization using Microsoft's battle-tested Identity framework, extended with custom user profiles, privacy controls, and soft-delete functionality.
* **Entity Framework Core + SQL Server:** All data persistence handled through EF Core with code-first migrations. Automatic migration application on startup ensures your database is always in sync.
* **Docker-Ready Deployment:** Complete Docker Compose setup with a containerized ASP.NET Core app and Azure SQL Edge database. One command (`docker-compose up`) and you're running the full stack locally.
* **Rich Domain Model:** Profiles, projects, competencies, work experience, education, messaging system (both direct messages and group conversations), and profile visit tracking—all modeled with proper relationships and validation.
* **Seed Data for Development:** Automatic demo data seeding in development mode so you can test features immediately without manual setup.

---

## 🧰 Tech Stack

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/dotnetcore/dotnetcore-original.svg" width="40" height="40" alt=".NET Core" title=".NET 8 (The Foundation)"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/csharp/csharp-original.svg" width="40" height="40" alt="C#" title="C# (The Language)"/>
  <img src="https://img.icons8.com/color/48/000000/microsoft-sql-server.png" width="40" height="40" alt="SQL Server" title="SQL Server (The Data Vault)"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="40" height="40" alt="Docker" title="Docker (The Container Ship)"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg" width="40" height="40" alt="Bootstrap" title="Bootstrap (The Pretty UI)"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" width="40" height="40" alt="JavaScript" title="JavaScript (The Interactive Bits)"/>
</p>

---

## 🎯 Features

### 👤 User Management
- **Full Profile System:** Extended ASP.NET Identity with custom fields (name, city, postal code, phone, profile image)
- **Privacy Controls:** Users can make profiles private or public
- **Soft Deletion:** Deactivate accounts without losing data
- **Normalized Search:** Fast, case-insensitive user search using pre-normalized name fields

### 📄 CV Builder
- **Work Experience:** Add multiple jobs with titles, companies, and date ranges
- **Education History:** Track degrees, schools, and graduation dates
- **Skills & Competencies:** Tag yourself with relevant technologies and expertise levels
- **Public CV Pages:** Shareable profile pages for showcasing your career

### 💬 Messaging System
- **Direct Messages:** One-on-one conversations between users
- **Group Conversations:** Multi-participant messaging with read/unread tracking
- **Real-time Notifications:** Badge indicators for unread message counts

### 🚀 Project Collaboration
- **Create Projects:** Showcase team projects with descriptions, images, and timelines
- **Team Management:** Add collaborators and track project participation
- **Project Discovery:** Browse and search for interesting initiatives

### 🔍 Search & Discovery
- **CV Search:** Find professionals by name, location, or skills
- **Profile Visits:** Track who's viewing your profile (with privacy respect)
- **Admin Dashboard:** User management and system oversight

---

## 🖼️ Screenshots

<p align="center">
  <img src="screenshots/home-page.png" alt="Screenshot 1: Home Page" width="800">
</p>
<p align="center">
  <strong>Screenshot 1:</strong> The landing page with user authentication and navigation.
</p>

<p align="center">
  <img src="screenshots/cv-profile.png" alt="Screenshot 2: CV Profile View" width="800">
</p>
<p align="center">
  <strong>Screenshot 2:</strong> A complete user CV profile showing work experience, education, and skills.
</p>

<p align="center">
  <img src="screenshots/messaging.png" alt="Screenshot 3: Messaging System" width="800">
</p>
<p align="center">
  <strong>Screenshot 3:</strong> The direct messaging interface with conversation history.
</p>

<p align="center">
  <img src="screenshots/project-showcase.png" alt="Screenshot 4: Project Showcase" width="800">
</p>
<p align="center">
  <strong>Screenshot 4:</strong> Project collaboration page displaying team projects and participants.
</p>

---

## ⚙️ How to Develop

### Prerequisites

You'll need:
- **.NET 8 SDK** (or later)
- **Docker Desktop** (for containerized development)
- **SQL Server** (LocalDB works fine, or use the Docker Compose setup)

### Option 1: Docker Compose (Recommended)

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/CVHub
cd CVHub

# 2. Start the entire stack (app + database)
docker-compose up --build

# 3. Open your browser
# The app will be available at http://localhost:5002
```

The Docker setup includes:
- ASP.NET Core app running on port 5002
- Azure SQL Edge database (SQL Server compatible)
- Automatic migrations and demo data seeding
- Volume mounts for live file changes

### Option 2: Local Development (Visual Studio / Rider)

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/CVHub
cd CVHub

# 2. Restore dependencies
dotnet restore

# 3. Update the connection string in appsettings.json
# (Default uses SQL Server LocalDB)

# 4. Apply migrations and run
cd WebApp
dotnet ef database update --project ../Infrastructure
dotnet run

# The app will start at https://localhost:5001 (or http://localhost:5000)
```

### Project Structure

```
CVHub/
├── Domain/                 # Core business entities and logic
│   ├── Entities/          # Profile, Project, Message, Education, etc.
│   ├── Identity/          # ApplicationUser (extended Identity)
│   └── Helpers/           # Name normalization utilities
├── Infrastructure/        # Data access and external concerns
│   ├── Data/             # ApplicationDbContext
│   ├── Migrations/       # EF Core migrations
│   └── Seeding/          # Demo data snapshots
├── WebApp/               # Presentation layer (MVC)
│   ├── Controllers/      # 13 controllers (Account, CV, Messages, etc.)
│   ├── Views/           # Razor views
│   ├── ViewModels/      # DTOs for views
│   ├── Services/        # Application services
│   └── wwwroot/         # Static files (CSS, JS, images)
├── docker-compose.yml    # Docker orchestration
└── Dockerfile           # Multi-stage build for the app
```

---

## 🗄️ Database Schema Highlights

The database includes:
- **AspNetUsers:** Extended Identity users with 12+ custom fields
- **Profiles:** Detailed CV information (bio, availability, competencies)
- **Educations:** Academic background
- **WorkExperiences:** Professional history
- **Projects:** Collaborative work showcase
- **Messages & Conversations:** Full messaging system with participants
- **ProfileVisits:** Engagement tracking

Over **20 migrations** have shaped this schema, showing the evolution from a simple user table to a full professional networking platform.

---

## 🔐 Security Features

- **ASP.NET Identity:** Industry-standard authentication with cookie-based sessions
- **Input Validation:** Comprehensive data annotations and regex patterns
- **SQL Injection Protection:** Parameterized queries via EF Core
- **Privacy Controls:** User-level profile visibility settings
- **Soft Deletes:** Data retention with deactivation flags

---

## 🚢 Deployment

The app is production-ready with:
- Multi-stage Docker builds (separate build/runtime containers)
- Environment-based configuration (Development/Production)
- Health checks for SQL Server dependency
- Automatic migration application on startup
- Volume-mounted static files for easy updates

---

## 🛠️ Technologies & Patterns Used

**Backend:**
- ASP.NET Core 8.0 MVC
- Entity Framework Core 8.0
- ASP.NET Identity
- Clean Architecture (Domain/Infrastructure/WebApp layers)
- Repository pattern via DbContext
- Dependency Injection (built-in DI container)

**Frontend:**
- Razor Views (server-side rendering)
- Bootstrap 5 (responsive UI)
- Vanilla JavaScript (interactivity)
- libman (client-side library management)

**Database:**
- SQL Server / Azure SQL Edge
- Code-First migrations
- Complex relationships (one-to-many, many-to-many)

**DevOps:**
- Docker & Docker Compose
- Multi-stage builds for optimization
- Environment variable configuration

---

## 📝 Future Enhancements (Roadmap)

- [ ] Real-time messaging with SignalR
- [ ] Advanced search with Elasticsearch
- [ ] File uploads for CV documents
- [ ] Email notifications (SendGrid integration)
- [ ] OAuth login (Google, LinkedIn)
- [ ] API endpoints for mobile apps
- [ ] CI/CD pipeline with GitHub Actions

---

## 👨‍💻 Author

**Nordtess**  
*Full-Stack Developer & Clean Architecture Enthusiast*

---

## 📜 License

This project is licensed under the MIT License—feel free to use it, learn from it, or build upon it!

---

<div align="center">

**Built with ❤️ and way too much coffee in Sweden 🇸🇪**

</div>
