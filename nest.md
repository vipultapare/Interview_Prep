
# NestJS – Modules, Controllers, Services & Dependency Injection

## Table of Contents

1. [Introduction to NestJS Architecture](#1-introduction-to-nestjs-architecture)
2. [Why NestJS Uses Modules, Controllers and Services](#2-why-nestjs-uses-modules-controllers-and-services)
3. [NestJS Architecture Overview](#3-nestjs-architecture-overview)
4. [Controllers](#4-controllers)
5. [Services](#5-services)
6. [Dependency Injection](#6-dependency-injection)
7. [Modules](#7-modules)
8. [Complete Project Implementation](#8-complete-project-implementation)
9. [How the Request Flow Works](#9-how-the-request-flow-works)
10. [Module Imports and Exports](#10-module-imports-and-exports)
11. [AppModule](#11-appmodule)
12. [NestJS CLI Commands](#12-nestjs-cli-commands)
13. [Project Structure](#13-project-structure)
14. [Controller vs Service vs Module](#14-controller-vs-service-vs-module)
15. [Common Mistakes](#15-common-mistakes)
16. [Interview Questions](#16-interview-questions)
17. [Interview-Ready Explanation](#17-interview-ready-explanation)
18. [Quick Revision](#18-quick-revision)

---

# 1. Introduction to NestJS Architecture

NestJS is a Node.js framework used to build scalable and maintainable backend applications.

NestJS uses TypeScript and provides a structured architecture based on several fundamental building blocks.

The three major building blocks are:

- Modules
- Controllers
- Services

These components help separate responsibilities within a backend application.

| Component | Responsibility |
|---|---|
| Module | Organizes related application components |
| Controller | Handles incoming HTTP requests |
| Service | Contains business logic |

---

# 2. Why NestJS Uses Modules, Controllers and Services

Imagine building a Project Management application.

The application needs to:

- Create projects.
- Fetch projects.
- Update projects.
- Delete projects.
- Manage clients.
- Manage users.
- Authenticate users.

If we put all the logic inside a single file, the application would become difficult to maintain.

Instead, NestJS separates responsibilities.

### Controller

Responsible for receiving requests and defining API endpoints.

### Service

Responsible for business logic and operations.

### Module

Responsible for organizing and connecting related components.

This separation makes the application:

- Maintainable
- Scalable
- Reusable
- Testable
- Organized

---

# 3. NestJS Architecture Overview

```text
                HTTP REQUEST
                     |
                     v
              ProjectsController
                     |
                     v
              ProjectsService
                     |
                     v
                  Database
                     |
                     v
              ProjectsService
                     |
                     v
              ProjectsController
                     |
                     v
                HTTP RESPONSE
```

Modules organize these components and manage their dependencies.

```text
                 ProjectsModule
                      |
          ┌───────────┴───────────┐
          |                       |
          v                       v
 ProjectsController         ProjectsService
```

---

# 4. Controllers

## What is a Controller?

A Controller is responsible for handling incoming HTTP requests and defining the routes through which clients interact with the backend application.

In simple words:

**A Controller is the entry point for HTTP requests.**

For example, when the frontend sends:

```http
GET /projects
```

The Controller receives the request and determines which method should execute.

## Creating a Controller

### projects.controller.ts

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('projects')
export class ProjectsController {

  @Get()
  getProjects() {
    return 'Getting all projects';
  }

}
```

### Understanding the Code

#### @Controller()

```typescript
@Controller('projects')
```

This defines the route prefix for the Controller.

All routes defined inside this Controller begin with:

```text
/projects
```

#### @Get()

```typescript
@Get()
```

This defines an HTTP GET route.

Combined with the Controller prefix, the endpoint becomes:

```http
GET /projects
```

#### getProjects()

```typescript
getProjects() {
  return 'Getting all projects';
}
```

This method executes when a request reaches the endpoint.

---

## Common Controller Decorators

| Decorator | Purpose |
|---|---|
| `@Controller()` | Defines a Controller |
| `@Get()` | Handles GET requests |
| `@Post()` | Handles POST requests |
| `@Put()` | Handles PUT requests |
| `@Patch()` | Handles PATCH requests |
| `@Delete()` | Handles DELETE requests |
| `@Param()` | Extracts route parameters |
| `@Query()` | Extracts query parameters |
| `@Body()` | Extracts request body |

## Example: CRUD Controller

```typescript
import {
  Controller,
  Get,
  Post,
  Put,
  Patch,
  Delete,
} from '@nestjs/common';

@Controller('projects')
export class ProjectsController {

  @Get()
  getAllProjects() {
    return 'Get all projects';
  }

  @Get(':id')
  getProjectById() {
    return 'Get project by ID';
  }

  @Post()
  createProject() {
    return 'Create project';
  }

  @Put(':id')
  updateProject() {
    return 'Replace project';
  }

  @Patch(':id')
  updateProjectPartially() {
    return 'Update project partially';
  }

  @Delete(':id')
  deleteProject() {
    return 'Delete project';
  }

}
```

### Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/projects` | Get all projects |
| GET | `/projects/:id` | Get one project |
| POST | `/projects` | Create project |
| PUT | `/projects/:id` | Replace/update project |
| PATCH | `/projects/:id` | Partially update project |
| DELETE | `/projects/:id` | Delete project |

---

## Route Parameters

Route parameters are used to identify specific resources.

### Example

```typescript
@Get(':id')
getProjectById(@Param('id') id: string) {
  return `Project ID: ${id}`;
}
```

Request:

```http
GET /projects/10
```

Response:

```text
Project ID: 10
```

---

## Query Parameters

Query parameters are commonly used for filtering, searching and pagination.

### Example

```typescript
@Get()
getProjects(@Query('status') status: string) {
  return `Projects with status: ${status}`;
}
```

Request:

```http
GET /projects?status=active
```

---

## Request Body

The request body is commonly used when creating or updating resources.

```typescript
@Post()
createProject(@Body() project: any) {
  return project;
}
```

Example request:

```json
{
  "name": "Shree Cement",
  "status": "active"
}
```

---

# 5. Services

## What is a Service?

A Service is responsible for implementing business logic.

In simple words:

**A Service is where the actual work is performed.**

Services commonly handle:

- Database operations
- Business logic
- Data processing
- Calculations
- External API communication
- Reusable operations

Controllers generally delegate business logic to Services.

---

## Creating a Service

### projects.service.ts

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class ProjectsService {

  getAllProjects() {
    return [
      { id: 1, name: 'Shree Cement' },
      { id: 2, name: 'Electrolux' },
      { id: 3, name: 'TSS' },
    ];
  }

  getProjectById(id: number) {
    return {
      id,
      name: 'Sample Project',
    };
  }

  createProject(project: any) {
    return {
      message: 'Project created successfully',
      project,
    };
  }

}
```

## What is @Injectable()?

```typescript
@Injectable()
```

This decorator marks a class as a provider that can participate in NestJS Dependency Injection.

NestJS can create and manage instances of the class and inject them into other classes when required.

---

## Why Do We Need Services?

Without Services, we might put business logic directly inside the Controller.

```typescript
@Controller('projects')
export class ProjectsController {

  @Get()
  getProjects() {

    // Database logic

    // Business logic

    // Validation logic

    // Data processing

  }

}
```

This makes Controllers difficult to maintain as the application grows.

Instead:

```text
ProjectsController
       |
       v
ProjectsService
       |
       v
Database
```

The Controller handles the request.

The Service performs the operation.

---

# 6. Dependency Injection

## What is Dependency Injection?

Dependency Injection is a design pattern where a class receives the dependencies it needs instead of creating those dependencies itself.

NestJS provides a built-in Dependency Injection system.

### Without Dependency Injection

```typescript
export class ProjectsController {

  private projectsService = new ProjectsService();

}
```

The Controller manually creates the Service.

This tightly couples the Controller to the implementation.

### With Dependency Injection

```typescript
export class ProjectsController {

  constructor(
    private readonly projectsService: ProjectsService
  ) {}

}
```

NestJS manages the instance and injects it into the Controller.

---

## Understanding Constructor Injection

```typescript
constructor(
  private readonly projectsService: ProjectsService
) {}
```

This is constructor-based Dependency Injection.

NestJS sees that the Controller requires `ProjectsService`.

If the Service is registered as a provider in the module, NestJS can resolve and inject it.

### Benefits

- Loose coupling
- Reusability
- Easier testing
- Easier maintenance
- Centralized dependency management

---

# 7. Modules

## What is a Module?

A Module is used to organize and group related application components.

In simple words:

**A Module tells NestJS which Controllers and Providers belong together and how they are connected.**

For example:

- AuthModule
- UsersModule
- ProjectsModule
- ClientsModule
- NotificationsModule

Each module manages a specific feature or domain.

---

## Creating a Module

### projects.module.ts

```typescript
import { Module } from '@nestjs/common';

import { ProjectsController } from './projects.controller';

import { ProjectsService } from './projects.service';

@Module({

  controllers: [ProjectsController],

  providers: [ProjectsService],

})

export class ProjectsModule {}
```

---

## Understanding @Module()

The `@Module()` decorator accepts metadata.

### Controllers

```typescript
controllers: [ProjectsController]
```

Registers the Controllers belonging to the module.

### Providers

```typescript
providers: [ProjectsService]
```

Registers Services and other providers with NestJS Dependency Injection.

### Imports

```typescript
imports: []
```

Allows the module to access providers exported from other modules that it imports.

### Exports

```typescript
exports: [ProjectsService]
```

Makes selected providers available to other modules that import this module.

---

## Module Metadata

| Property | Purpose |
|---|---|
| `controllers` | Registers Controllers |
| `providers` | Registers Services and other providers |
| `imports` | Imports other Modules |
| `exports` | Exposes selected Providers |

---

# 8. Complete Project Implementation

Let's create a simple Projects feature using Modules, Controllers and Services.

## Folder Structure

```text
src/
│
├── projects/
│   ├── projects.controller.ts
│   ├── projects.service.ts
│   └── projects.module.ts
│
├── app.module.ts
│
└── main.ts
```

---

## Step 1: Create Projects Service

### projects.service.ts

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class ProjectsService {

  private projects = [
    { id: 1, name: 'Shree Cement' },
    { id: 2, name: 'Electrolux' },
  ];

  getAllProjects() {
    return this.projects;
  }

  getProjectById(id: number) {
    return this.projects.find(
      project => project.id === id
    );
  }

  createProject(project: any) {

    const newProject = {
      id: this.projects.length + 1,
      ...project,
    };

    this.projects.push(newProject);

    return newProject;
  }

}
```

The Service contains the logic for retrieving and creating projects.

This example uses an in-memory array instead of a database.

---

## Step 2: Create Projects Controller

### projects.controller.ts

```typescript
import {
  Controller,
  Get,
  Post,
  Param,
  Body,
} from '@nestjs/common';

import { ProjectsService } from './projects.service';

@Controller('projects')
export class ProjectsController {

  constructor(
    private readonly projectsService: ProjectsService
  ) {}

  @Get()
  getAllProjects() {
    return this.projectsService.getAllProjects();
  }

  @Get(':id')
  getProjectById(@Param('id') id: string) {
    return this.projectsService.getProjectById(Number(id));
  }

  @Post()
  createProject(@Body() project: any) {
    return this.projectsService.createProject(project);
  }

}
```

The Controller receives HTTP requests and delegates operations to ProjectsService.

---

## Step 3: Create Projects Module

### projects.module.ts

```typescript
import { Module } from '@nestjs/common';

import { ProjectsController } from './projects.controller';

import { ProjectsService } from './projects.service';

@Module({

  controllers: [ProjectsController],

  providers: [ProjectsService],

})

export class ProjectsModule {}
```

The Module registers the Controller and Service.

---

## Step 4: Create App Module

### app.module.ts

```typescript
import { Module } from '@nestjs/common';

import { ProjectsModule } from './projects/projects.module';

@Module({

  imports: [ProjectsModule],

})

export class AppModule {}
```

The AppModule imports ProjectsModule.

---

# 9. How the Request Flow Works

Suppose the frontend sends:

```http
GET http://localhost:3000/projects
```

### Step 1: Frontend sends request

```http
GET /projects
```

### Step 2: Controller receives request

NestJS identifies:

```typescript
@Controller('projects')
```

and:

```typescript
@Get()
```

### Step 3: Controller calls Service

```typescript
return this.projectsService.getAllProjects();
```

### Step 4: Service executes business logic

```typescript
getAllProjects() {
  return this.projects;
}
```

The Service returns the data.

### Step 5: Controller returns the response

NestJS serializes the returned data into an HTTP response, generally JSON.

### Complete Flow

```text
Frontend
   |
   | GET /projects
   v
ProjectsController
   |
   | getAllProjects()
   v
ProjectsService
   |
   | Retrieves Data
   v
Database / Data Source
   |
   v
ProjectsService
   |
   v
ProjectsController
   |
   v
HTTP Response
```

---

# 10. Module Imports and Exports

Modules can share Providers with other modules.

Suppose ProjectsModule needs UsersService.

UsersService belongs to UsersModule.

We need to:

1. Register UsersService in UsersModule.
2. Export UsersService from UsersModule.
3. Import UsersModule into ProjectsModule.
4. Inject UsersService into ProjectsService.

---

## Step 1: Create Users Module

### users.module.ts

```typescript
import { Module } from '@nestjs/common';

import { UsersController } from './users.controller';

import { UsersService } from './users.service';

@Module({

  controllers: [UsersController],

  providers: [UsersService],

  exports: [UsersService],

})

export class UsersModule {}
```

The `exports` property makes UsersService available to importing modules.

---

## Step 2: Import UsersModule into ProjectsModule

### projects.module.ts

```typescript
import { Module } from '@nestjs/common';

import { ProjectsController } from './projects.controller';

import { ProjectsService } from './projects.service';

import { UsersModule } from '../users/users.module';

@Module({

  imports: [UsersModule],

  controllers: [ProjectsController],

  providers: [ProjectsService],

})

export class ProjectsModule {}
```

---

## Step 3: Inject UsersService into ProjectsService

### projects.service.ts

```typescript
import { Injectable } from '@nestjs/common';

import { UsersService } from '../users/users.service';

@Injectable()
export class ProjectsService {

  constructor(
    private readonly usersService: UsersService
  ) {}

  getProjectsByUser(userId: number) {

    const user = this.usersService.findUserById(userId);

    return {
      user,
      projects: [],
    };

  }

}
```

Now ProjectsService can use UsersService because UsersModule exports it and ProjectsModule imports UsersModule.

---

## Module Communication

```text
                UsersModule
                    |
                    |
              exports UsersService
                    |
                    v
               ProjectsModule
                    |
                    v
             ProjectsService
                    |
                    v
               UsersService
```

---

# 11. AppModule

AppModule is generally the root module of a NestJS application.

It imports the feature modules required by the application.

### app.module.ts

```typescript
import { Module } from '@nestjs/common';

import { AuthModule } from './auth/auth.module';

import { UsersModule } from './users/users.module';

import { ProjectsModule } from './projects/projects.module';

import { ClientsModule } from './clients/clients.module';

import { NotificationsModule } from './notifications/notifications.module';

@Module({

  imports: [
    AuthModule,
    UsersModule,
    ProjectsModule,
    ClientsModule,
    NotificationsModule,
  ],

})

export class AppModule {}
```

### AppModule Responsibilities

- Acts as the root module.
- Imports feature modules.
- Helps NestJS assemble the application dependency graph.

---

# 12. NestJS CLI Commands

NestJS CLI can automatically generate modules, controllers and services.

## Generate Module

```bash
nest g module projects
```

## Generate Controller

```bash
nest g controller projects
```

## Generate Service

```bash
nest g service projects
```

## Generate Complete CRUD Resource

```bash
nest g resource projects
```

The resource command generates a feature structure and scaffolding for common CRUD operations.

---

# 13. Project Structure

A scalable NestJS application may follow this structure:

```text
src/
│
├── app.module.ts
│
├── auth/
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   └── auth.module.ts
│
├── users/
│   ├── users.controller.ts
│   ├── users.service.ts
│   └── users.module.ts
│
├── projects/
│   ├── projects.controller.ts
│   ├── projects.service.ts
│   └── projects.module.ts
│
├── clients/
│   ├── clients.controller.ts
│   ├── clients.service.ts
│   └── clients.module.ts
│
└── notifications/
    ├── notifications.controller.ts
    ├── notifications.service.ts
    └── notifications.module.ts
```

### Feature-Based Architecture

Each feature is organized into its own folder.

For example:

- Authentication
- Users
- Projects
- Clients
- Notifications

This makes the application easier to maintain and extend.

---

# 14. Controller vs Service vs Module

| Feature | Controller | Service | Module |
|---|---|---|---|
| Purpose | Handle requests | Business logic | Organize components |
| HTTP routes | Yes | No | No |
| HTTP request handling | Yes | No | No |
| Business logic | Ideally minimal | Yes | No |
| Database interaction | Usually delegates | Commonly | No |
| Decorator | `@Controller()` | `@Injectable()` | `@Module()` |
| DI role | Receives dependencies | Receives dependencies | Registers dependencies |
| Example | ProjectsController | ProjectsService | ProjectsModule |

---

# 15. Common Mistakes

## Mistake 1: Putting Everything in Controller

Controllers should generally remain focused on request handling.

Business logic should be delegated to Services or other appropriate providers.

---

## Mistake 2: Forgetting to Register Service

Incorrect:

```typescript
@Module({

  controllers: [ProjectsController],

})
export class ProjectsModule {}
```

If ProjectsController injects ProjectsService, ProjectsService must be registered or otherwise available through the module dependency graph.

Correct:

```typescript
@Module({

  controllers: [ProjectsController],

  providers: [ProjectsService],

})
export class ProjectsModule {}
```

---

## Mistake 3: Forgetting to Export a Service

If another module needs a Service, the owning module must export it, and the consuming module must import the owning module.

---

## Mistake 4: Manually Instantiating Services

Avoid:

```typescript
const service = new ProjectsService();
```

In NestJS, use Dependency Injection so the framework can manage the provider.

---

## Mistake 5: Confusing Modules and Services

A Module organizes and registers components.

A Service performs operations.

A Controller handles incoming requests.

---

# 16. Interview Questions

## Q1. What is a Controller in NestJS?

A Controller handles incoming HTTP requests, defines routes and delegates business logic to Services.

---

## Q2. What is a Service in NestJS?

A Service is a provider that generally contains business logic and performs operations such as database queries, calculations or external API interactions.

---

## Q3. What is a Module in NestJS?

A Module organizes related Controllers and Providers and manages dependencies through imports, exports and registrations.

---

## Q4. What is Dependency Injection?

Dependency Injection is a design pattern in which a class receives dependencies from an external system rather than creating them itself.

NestJS provides a built-in DI container.

---

## Q5. What is @Injectable()?

`@Injectable()` marks a class as a provider that can participate in NestJS Dependency Injection.

---

## Q6. What is @Controller()?

`@Controller()` defines a Controller and optionally its route prefix.

---

## Q7. What is @Module()?

`@Module()` defines module metadata such as Controllers, Providers, Imports and Exports.

---

## Q8. What is the purpose of providers?

Providers are classes or other injectable values that NestJS can manage and inject into other components.

Services are commonly registered as providers.

---

## Q9. What is the purpose of imports in a Module?

Imports allow a module to access providers exported from other modules.

---

## Q10. What is the purpose of exports in a Module?

Exports make selected providers available to other modules that import the module.

---

## Q11. How does a Controller communicate with a Service?

A Controller receives the Service through Dependency Injection, typically using constructor injection, and calls its methods.

---

## Q12. Why do we separate Controller and Service?

This separation keeps request handling separate from business logic, making applications more maintainable, reusable and testable.

---

## Q13. What is AppModule?

AppModule is generally the root module that imports the application's feature modules.

---

## Q14. What is constructor injection?

Constructor injection is a technique where dependencies are supplied through a class constructor.

---

## Q15. Can one Module use another Module's Service?

Yes. The module owning the Service exports it, and the consuming module imports that module.

---

# 17. Interview-Ready Explanation

If an interviewer asks:

**"Explain Modules, Controllers and Services in NestJS."**

You can answer:

NestJS follows a modular architecture in which Modules, Controllers and Services are the fundamental building blocks.

A Controller is responsible for handling incoming HTTP requests. We define API routes using decorators such as `@Get()`, `@Post()`, `@Put()` and `@Delete()`. The Controller receives the request, extracts the required data and delegates the business logic to a Service.

A Service is responsible for implementing business logic. We generally use Services for database operations, business rules, calculations, data processing and communication with other services. Services are decorated with `@Injectable()` so that NestJS can manage them through Dependency Injection.

A Module is used to organize related Controllers and Providers. Using the `@Module()` decorator, we register Controllers and Providers, import other modules when required and export providers that other modules need to access.

NestJS also provides Dependency Injection, which allows us to inject Services into Controllers or other Services instead of manually creating instances.

This separation of responsibilities makes the application modular, scalable, reusable and easier to maintain.

---

# 18. Quick Revision

| Concept | Meaning |
|---|---|
| NestJS | Node.js backend framework |
| Controller | Handles HTTP requests |
| Service | Contains business logic |
| Module | Organizes components |
| `@Controller()` | Defines a Controller |
| `@Injectable()` | Marks a class as injectable |
| `@Module()` | Defines module metadata |
| `@Get()` | Handles GET requests |
| `@Post()` | Handles POST requests |
| `@Param()` | Extracts route parameters |
| `@Query()` | Extracts query parameters |
| `@Body()` | Extracts request body |
| Dependency Injection | Provides dependencies to classes |
| Providers | Injectable components managed by NestJS |
| Imports | Imports other modules |
| Exports | Exposes providers to other modules |
| AppModule | Root module |

---

# Final Summary

```text
MODULE
   |
   |-- Organizes
   |
   |-- Controller
   |      |
   |      |-- Receives HTTP Request
   |      |
   |      |-- Calls Service
   |
   |-- Service
          |
          |-- Business Logic
          |
          |-- Database Operations
          |
          |-- External API Operations
```

### Remember

- **Module = Organizer**
- **Controller = Request Handler**
- **Service = Business Logic**
- **Dependency Injection = Dependencies provided by NestJS**

Understanding these four concepts is the foundation of building backend applications using NestJS.
