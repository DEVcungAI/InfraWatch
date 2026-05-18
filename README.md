# InfraWatch: IT Infrastructure Monitoring Platform

InfraWatch is an ASP.NET Core-based IT Asset and Network Monitoring System designed to help IT teams manage infrastructure assets, monitor device availability, track operational logs, and support basic incident response workflows.

The project simulates a real-world IT operations environment where servers, network devices, printers, IP phones, CCTV/NVR systems, and other IT assets need to be registered, monitored, and maintained.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Folder Structure](#folder-structure)
- [Database Design](#database-design)
- [API Endpoints](#api-endpoints)
- [Monitoring Workflow](#monitoring-workflow)
- [Installation and Setup](#installation-and-setup)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Testing with Swagger](#testing-with-swagger)
- [Future Improvements](#future-improvements)
- [What I Learned](#what-i-learned)
- [Interview Talking Points](#interview-talking-points)
- [License](#license)

---

## Project Overview:

InfraWatch was built as a hands-on project to strengthen knowledge in:

- IT asset management
- Network monitoring
- ASP.NET Core Web API development
- SQL Server database integration
- Entity Framework Core
- Background services
- 3-layer architecture
- Infrastructure operations workflow
- IT documentation and procedure design

The main goal of this project is to demonstrate how an IT support or infrastructure team can register assets, monitor device health, track device status changes, and maintain logs for troubleshooting and operational review.

---

## Key Features:

### Asset Management:

- Add new IT assets
- View all registered assets
- View asset details
- Update asset information
- Delete assets when no longer in use

Example asset types:

- Server
- Router
- Switch
- Printer
- IP Phone
- CCTV Camera
- NVR
- Workstation
- Laptop
- POS Terminal

---

### Network Health Monitoring:

- Perform ping-based health checks
- Determine whether an asset is `UP`, `DOWN`, or `UNKNOWN`
- Update last checked timestamp
- Store monitoring results in logs

---

### Background Monitoring Worker:

- Runs periodic health checks automatically
- Uses ASP.NET Core BackgroundService
- Monitors registered assets at scheduled intervals
- Updates asset status without manual API calls

---

### Logging and Audit Trail:

- Store asset monitoring logs
- Track status changes over time
- Support troubleshooting and historical analysis

---

### Alert Logic:

- Detect unavailable devices
- Flag assets with failed health checks
- Prepare foundation for future email or dashboard alerts

---

### 3-Layer Architecture:

The project follows a 3-layer architecture:

```
Presentation Layer  → Controllers
Business Layer      → Services
Data Access Layer   → Repositories / DbContext
```

# Technology Stack:
- C#
- ASP.NET Core Web API
- SQL Server 2022
- Entity Framework Core
- Swagger / OpenAPI
- BackgroundService
- Visual Studio 2022
- Windows Server 2022
- GitHub for Desktop


# System Architecture:

```
Client / Swagger / Postman
    ↓
Controllers
    ↓
Services
    ↓
Repositories
    ↓
Entity Framework Core
    ↓
SQL Server Database
```


# Background monitoring flow:

```
MonitoringWorker
    ↓
MonitoringService
    ↓
Ping / Health Check
    ↓
Update Asset Status
    ↓
Save Monitoring Log
    ↓
SQL Server
```


# Folder Structure:

```
InfraWatch/
│
├── Controllers/
│   ├── AssetsController.cs
│   ├── MonitoringController.cs
│   └── LogsController.cs
│
├── Models/
│   ├── Asset.cs
│   ├── AssetLog.cs
│   └── Alert.cs
│
├── DTOs/
│   ├── AssetCreateDto.cs
│   ├── AssetUpdateDto.cs
│   ├── AssetResponseDto.cs
│   └── MonitoringResultDto.cs
│
├── Data/
│   └── AppDbContext.cs
│
├── Repositories/
│   ├── Interfaces/
│   │   ├── IAssetRepository.cs
│   │   ├── IAssetLogRepository.cs
│   │   └── IAlertRepository.cs
│   │
│   └── Implementations/
│       ├── AssetRepository.cs
│       ├── AssetLogRepository.cs
│       └── AlertRepository.cs
│
├── Services/
│   ├── Interfaces/
│   │   ├── IAssetService.cs
│   │   ├── IMonitoringService.cs
│   │   └── IAlertService.cs
│   │
│   └── Implementations/
│       ├── AssetService.cs
│       ├── MonitoringService.cs
│       └── AlertService.cs
│
├── BackgroundServices/
│   └── MonitoringWorker.cs
│
├── Middlewares/
│   └── ExceptionHandlingMiddleware.cs
│
├── Helpers/
│   ├── PingHelper.cs
│   └── DateTimeHelper.cs
│
├── Migrations/
│
├── Properties/
│   └── launchSettings.json
│
├── appsettings.json
├── appsettings.Development.json
├── Program.cs
└── README.md
```