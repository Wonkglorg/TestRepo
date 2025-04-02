# MarkDoc

<ig src="/resources/images/logo_green.png" width="40%" alt="Logo" />

## System Documentation

---

## 📚 Table of Contents

- **[1. Overview & Introduction](#1-overview--introduction)**
- **[2. System Architecture](#2-system-architecture)**
    - [Setup & Configuration](#setup--configuration)
        - [Requirements](#requirements)
        - [Standalone](#standalone)
        - [Server](#server)
        - [basic Deployment to Linux using Jenkins](#basic-deployment-to-linux-using-jenkins)
    - [Frontend](#frontend)
    - [Backend-Api](#backend-api)
    - [Backend-Core](#backend-core)
    - [Technology Stack](#technology-stack)
    - [Deployment Environment](#deployment-environment)
    - [Infrastructure Details](#infrastructure-details)
- **[3. Functional Requirements](#3-functional-requirements)**
    - [Use Cases](#use-cases)
    - [User Roles & Permissions](#user-roles--permissions)
    - [Feature List](#feature-list)
- **[4. API Documentation](#4-api-documentation)**
    - [Authentication](#authentication)
    - [API Endpoints](#api-endpoints)
    - [Error Codes](#error-codes)
- **[5. Database Design](#5-database-design)**
    - [ER Model](#er-model)
    - [ER Diagram](#er-diagram)
    - [Triggers](#triggers)
    - [Connection Pooling](#connection-pooling)
    - [Tables & Fields](#tables--fields)
    - [Data Flow](#data-flow)
- **[6. Security Considerations](#6-security-considerations)**
    - [Authentication & Authorization](#authentication--authorization)
- **[7. Deployment & CI/CD Pipeline](#7-deployment--cicd-pipeline)**
    - [Build Process](#build-process)
    - [Configuration Files](#configuration-files)
- **[8. Documentation](#8-documentation)**
    - [Javadoc](#javadoc)
- **[9. Monitoring & Logging](#9-monitoring--logging)**
    - [Logging Strategy](#logging-strategy)
- **[10. Maintenance & Future Enhancements](#10-maintenance--future-enhancements)**
    - [Planned Features](#planned-features)

<div style="page-break-after: always;"></div>

## 1. Overview & Introduction

**Project Name:** Documentation Tool
**Version:** 1.0.0   
**Authors:** Dominik Meierhofer   
**Date:** 2025-03-21   
**Purpose:** Web-based tool for creating and managing project documentation.  
**Scope:** This tool is intended for developers, technical writers, and project managers to collaboratively manage
project documentation using markdown. It includes permission access control and quality of life markdown editing.

---

<div style="page-break-after: always;"></div>

## 2. System Architecture

The application is split into the frontend, and 2 backend components consisting of the api and core modules.
The front and backend is seperated and communicates via RESTful API endpoints.

### Frontend

The frontend is written with the Angular-framework abd NodeJs Runtime.
The core languages are TypeScript, HTML and Css. The design colors are leaned on the existing webservices
from Merkur Versicherungen.

#### Pages

Our web application consists of three core components:

1. The navigation bar on the top is always visable and holds:

- Toggle button for the sidebar
- logo
- searchbar
- Profil

2. The toggable and dragable sidebar on the left with:

- filetree
- resource upload button
- admin navigation button

3. Main component in the middel of the window. Shows different pages

- editor
- view/preview
- Admin component

#### Backend interaction

Five typScript files to call the Rest Endpoints with HttpClient.
Every api.ts has a service.ts. Except the repoApi.
The services call the api enpoints methods and the services get injected by the components.
The Respons gets sent with JSON and handled with interfaces.

#### Api

| api              | Description                                                                          |
|------------------|--------------------------------------------------------------------------------------|
| `apiAuth.ts`     | Handels rest endpoints with HttpClient and baseUrl: http:'//localhost:8080/auth'     |
| `apiGroup.ts`    | Handels rest endpoints with HttpClient and baseUrl: http:'//localhost:8080/group'    |
| `apiRepo.ts`     | Handels rest endpoints with HttpClient and baseUrl: http:'//localhost:8080/repo'     |
| `apiResource.ts` | Handels rest endpoints with HttpClient and baseUrl: http:'//localhost:8080/resource' |
| `apiUser.ts`     | Handels rest endpoints with HttpClient and baseUrl: http:'//localhost:8080/user'     |

#### service

| api                  | Description                                                                          |
|----------------------|--------------------------------------------------------------------------------------|
| `authService.ts`     | service to call and subscribe the apiAuth.ts methods. Handle Response and errors     |
| `groupService.ts`    | service to call and subscribe the apiGroup.ts methods. Handle Response and errors    |
| `resourceService.ts` | service to call and subscribe the apiResource.ts methods. Handle Response and errors |
| `userService.ts`     | service to call and subscribe the apiUser.ts methods. Handle Response and errors     |

#### Response models

| Api response model                       | 
|------------------------------------------|
| `apiResponseFileTree.ts`                 |
| `apiResponseGetPermission.ts`     	      |
| `apiResponseGroup.ts`  		                | 
| `apiResponseLogin.ts`      		            |
| `apiResponseModel.ts`                    |
| `apiResponseModelDocumentContent.ts`     |
| `apiResponseModelRepos.ts`               |
| `apiResponseModelResourceBeingEdited.ts` |
| `apiResponseResource.ts`                 |
| `apiResponseTags.ts`                     |
| `apiResponseUser.ts`                     |

#### Plugins

##### Markdown editor

For our markdown editor we use the ngx-markdown-editor and ace-builds bootstrap font-awesome plugins
It is easy to implement, delivers syntax highlighting, a live preview option and a markdown toolbar.

##### Word Converter

To convert Word into markdown, we first use the 'npm mammoth' plugin to convert word into HMTL.
After that, the 'npm turndown' package converts the HTML to markdown.

##### User information

Users are informed by the system if something was successfull or not.
Small pop-ups come up in the left right corner. These Informations are easy generated with the ngx-toastr package

##### Icons

We use the library 'remixIcon' for all icons in the frontend.

---

### Backend API

The `api` module provides the RESTful API endpoints used by the frontend to interact with the backend. It is responsible
for handling all incoming and outgoing HTTP requests.
The separation of core and API was chosen to separate the functional logic of the application from the spring
dependency, this makes it easier to swap and to more precisely define unit tests.

Backend endpoints can be accessed using `api.markdoc.net`



---

#### Authentication

Authentication is handled using JWT tokens. The user logs in with their credentials, under "/auth/login" and upon
successful validation, all endpoints besides "auth/**" are jwt protected and need to be sent as a bearer header with
each request.

--- 

#### Web Tests

Web Tests are defined under: `test/doc/api/web` and should

---

#### Services

[Services](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Service.html)
are singleton classes that encapsulate the core business logic of the application. They validate and call the relevant
core processes.

These services are Spring-managed components, leveraging Inversion of Control (IoC) to enable clean, modular, and easily
accessible logic throughout the API module.

| Service             | Description                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| `PermissionService` | Handles resource filtering based on user or group permissions.                                        |
| `RepoService`       | Validates and manages access to repository objects, which serve as the foundation for all operations. |
| `ResourceService`   | Oversees all resource-related operations, including creation, deletion, editing, and retrieval.       |
| `UserService`       | Manages user/group-related actions such as creating, editing, and removing users.                     |

<img src="/resources/images/backend/java/services.png" alt="Services" width="1050" />

---

<div style="page-break-after: always;"></div>

#### Controllers

Controllers Represent the endpoints that are exposed and can be interacted with. Each controller endpoint should return
`ResponseEntity<RestResponse<T>>`  where T is the content of the response.

<img src="/resources/images/backend/java/controllers.png" alt="Controllers" width="1050" />

---

### Backend-Core

#### Exceptions

`Client Exceptions`
Are exceptions that should not be logged to the console but used as quick way to return back out of
methods to send the client a response from the controller.

| Exception                  | Description                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------|
| `InvalidGroupException`    | If a Group does not exist (should occur when retrieving or modifying a group)             |
| `InvalidPathException`     | If a Path is not valid or does not follow the required format                             |
| `InvalidUserException`     | If a User is not valid                                                                    |
| `InvalidRepoException`     | If a Repo is not valid                                                                    |
| `InvalidResourceException` | If a Resource is not valid (usually when it does not exist when editing or retrieving it) |
| `InvalidTagException`      | If a Referenced Tag is not valid (when retrieving or modidfying it)                       |

---

`Core Exceptions`
Are exceptions that should be logged and represent a wrong state of the application that should be addressed.

| Exception          | Description                                    |
|--------------------|------------------------------------------------|
| `SqlCoreException` | When an error occurred during an sql operation |

#### Git Classes

Each file modified / added or removed is stored as a branch commit under the local git repository, this allows the
application to leverage the robust git version control system.

<img src="/resources/images/backend/java/git-classes.png" alt="Git Code UML" width="70%" />

| Class         | Description                                                    |
|---------------|----------------------------------------------------------------|
| `User Branch` | Represents a Users Branch in the local git repo                |
| `Git Stage`   | Enum representing the different Stages the Git Repo can access |
| `Git Repo`    | The Overall Representation of a Repository                     |

#### Database Classes

Each operation that is performed on the database is stored in 1 of the Function Classes, which share a common interface
with the Representing [Service](#services) classes

<img src="/resources/images/backend/java/database-code-uml.png" alt="Datenbank Klassen" width="70%" />

---

#### Interface

The Database and the Services implement the same matching interface to ensure consistency between calls.

<img src="/resources/images/backend/java/interfaces.png" alt="Interfaces" width="70%"/>

#### Git

Git is represented by the backing GitRepo class, this class is responsible for providing high level git operations.
Each specific Users Branch is represented by a UserBranch class, this class is responsible for providing high level
access to a users created branch.

---

<div style="page-break-after: always;"></div>

## 3. Environment Setup

#### Environment Profiles

| Profile      | Description                                          |
|--------------|------------------------------------------------------|
| `dev`        | `Database`: Physical <br/> `Web tests`: With Gui     |
| `deployment` | `Database`: In Memory <br/> `Web Tests`: Without gui |
| `production` | `Database`: Physical <br/>                           |

#### Requirements

Java 21

#### Standalone

The project can be locally built and execute, or ran through the generated war file.

When building the project using `gradle build` 2 war files will be generated a standalone executeable version and a war
ending in `-plain.war` to deploy on providers like tomcat.

#### Server

Running the war on a server requires no extra tools or external applications.

Deploying the the code to a server can be done in multiple ways, either via the provided jenkins integrated pipeline
defined by the `Jenkinsfile`.

todo describe steps needed to setup the pipeline on an ubuntu server?

### Basic Deployment to Linux using Jenkins

When setting up a new server these are rough outlines to follow to get the application running on a linux server.

#### Prerequisites

Installing java 21 ```sudo apt install openjdk-21-jdk```

Installing Jenkins

````
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install Jenkins
````

Installing NPM

```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g @angular/cli@19.1.6
```

#### Setup

Enabling jenkins Service

```
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Connect to Jenkins and start the setup process by visiting `http://<ip>:9090`

Once setup create a new Pipeline:   
<img src="/resources/images/jenkins/Setup_1.png" alt="Dataflow" width="350" />

Defining the repository to load the pipeline from:   
<img src="/resources/images/jenkins/Setup_2.png" alt="Dataflow" width="350" />

The correct permissions as specified in the pipeline need to be given to the jenkins user.

Setting up a basic Executable war file Service:
```sudo nano /etc/systemd/system/markdoc.service```

```
[Unit]
Description=MarkDoc Backend Service
After=network.target

[Service]
Type=simple
User=jenkins
ExecStart=/usr/bin/java -jar /opt/staging/MarkDoc-Backend.war
Restart=on-failure
RestartSec=5
WorkingDirectory=/opt/staging
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

To allow jenkins to start the service the jenkins user needs to be added to the sudoers file:
```sudo visudo```
```jenkins ALL=(ALL) NOPASSWD: /bin/systemctl start markdoc.service```

### Technology Stack

- **Frontend:** Angular, NodeJs, TypeScript, Html, Css
- **Backend:** Spring Boot, Java
- **Backend-Testing:** JUnit
- **Database:** SQLite
- **Cloud Provider:** On-Premises, Hetzner
- **Deployment Tools:** Jenkins, Nginx

### Infrastructure Details

#### Caffeine

Caffeine is utilized as an in-memory caching layer as well as manual caching when applicable to improve
performance and reduce load on the underlying data
store. Frequently accessed data, such as permissions and resource metadata, are cached to ensure fast retrieval and
minimal latency during read operations.

---

<div style="page-break-after: always;"></div>

## 4. Functional Requirements

### Use Cases

- Create a new markdown file
- Edit existing documentation with live preview
- Assign read/write permissions to users
- Convert word documents to markdown

### User Roles & Permissions

- **Admin**: Full access
- **User**: Limited access

### Feature List

### 📋 Feature List

- **Full-Text Search**
  Full Text Search across documents and repositories.
- **Live Markdown Preview**
  Real-time rendering of markdown content while editing.
- **User Management**
  Add, remove, and update users with fine-grained control over their permissions.
- **Word-to-Markdown Conversion**
  Convert Microsoft Word documents into markdown format.
- **API Integration**
  RESTful API endpoints enable communication between frontend and backend.
- **Advanced Filtering**
  Filter documents by tags, categories, and blacklist/whitelist rules.
- **Multi-Repository Support**
  Seamlessly manage multiple repositories as a unified workspace.
  Repositories can be attached or removed without disrupting functionality.
- **Git-Based Version Control**
  Integrated Git support for change tracking, rollbacks, and collaboration history.
- **Ant Pattern Permissions**
  Use Ant-style patterns to configure access rules for users and groups.
- **User Groups**
  Define user groups for easier bulk permission management.
- **Serverless Architecture**
  Self-contained app with no external server dependency—runs entirely from a Git repo and local SQLite database.

---

<div style="page-break-after: always;"></div>

## 5. API Documentation

### Authentication

- **Method:** JWT
- **Example Request:**
  ```bash
  curl -H "Authorization: Bearer <token>" https://api.example.com/resource
  ```

### API Endpoints

Endpoints get automatically generated with swagger which can be found under: `/swagger-ui/index.html`
below are a few endpoints listed for reference, this may not be up to date or complete, the truth is always found under
the swagger endpoint

#### Auth

| Method | Endpoint       | Description |
|--------|----------------|-------------|
| POST   | `/auth/login`  | User login  |
| GET    | `/auth/logout` | User logout |

---

#### User

| Method | Endpoint                      | Description                      |
|--------|-------------------------------|----------------------------------|
| POST   | `/api/user/add`               | Adds a new user                  |
| POST   | `/api/user/remove`            | Removes a user                   |
| POST   | `/api/user/permission/add`    | Adds a permission to a user      |
| POST   | `/api/user/permission/remove` | Removes a permission from a user |
| POST   | `/api/user/permission/update` | Updates a permission from a user |
| GET    | `/api/user/get`               | Get users                        |

---

#### Resource

| Method | Endpoint                       | Description                          |
|--------|--------------------------------|--------------------------------------|
| POST   | `/api/resource/add`            | Adds a resource                      |
| POST   | `/api/resource/remove`         | Removes a resource                   |
| POST   | `/api/resource/update`         | Updates a resource                   |
| POST   | `/api/resource/move`           | Moves a resource                     |
| POST   | `/api/resource/get`            | Gets a resource                      |
| POST   | `/api/resource/get/filetree`   | Constructs a file tree               |
| POST   | `/api/resource/editing/set`    | Sets a resource as being edited      |
| POST   | `/api/resource/editing/remove` | Removes a file as being edited       |
| GET    | `/api/resource/editing/get`    | Checks if a resource is being edited |
| POST   | `/api/resource/tag/add`        | Adds a new tag                       |
| POST   | `/api/resource/tag/remove`     | Removes a tag                        |
| POST   | `/api/resource/tag/get`        | Retrieves all tags                   |

---

#### Group

| Method | Endpoint                       | Description                       |
|--------|--------------------------------|-----------------------------------|
| POST   | `/api/group/add`               | Adds a new group                  |
| POST   | `/api/group/remove`            | Removes a group                   |
| POST   | `/api/group/rename`            | Renames a group                   |
| POST   | `/api/group/user/add`          | Adds a user to a group            |
| POST   | `/api/group/user/remove`       | Removes a user from a group       |
| POST   | `/api/group/permission/add`    | Adds a permission to a group      |
| POST   | `/api/group/permission/remove` | Removes a permission from a group |
| POST   | `/api/group/permission/update` | Updates a permission of a group   |
| GET    | `/api/group/get`               | Get groups                        |

---

#### Repo

| Method | Endpoint        | Description             |
|--------|-----------------|-------------------------|
| GET    | `/api/repo/get` | Gets all existing repos |

### Error Codes

| Code | Description           |
|------|-----------------------|
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 500  | Internal Server Error |

### Response Format

All responses follow the same format:

```json
{
  "message": "success-message",
  "error": "error-message",
  "content": {
  }
}
```

- Message: A success message if the request was successful
- Error: An error message if the request failed
- Content: The actual data returned by the API

#### Example Response

```json
{
  "message": "User created successfully.",
  "error": "",
  "content": {
    "id": "u12345",
    "username": "johndoe",
    "email": "johndoe@example.com"
  }
}
```

#### Example Error Response

```json
{
  "message": "",
  "error": "User not found.",
  "content": {}
}
```

---

<div style="page-break-after: always;"></div>

## 6. Database Design

The Database uses SQLite as its Backend this was chosen because it is a fast and robust database that is self contained
and needs to external host as specified in the requirements.

The application uses 2 separate Databases to manage its data. The users database is a global database storing all
existing users, their roles and login credentials. The data database is a local database that is created for each
repository and stores permissions to access resources based on the global users table and information related to
resources

### ER-Model

#### Users

<img src="/resources/images/backend/db/ER-Model-User.png" alt="ER Model User" width="55%" />

#### Resources

<img src ="/resources/images/backend/db/ER-Model-Data.png" alt="ER Model Data" width="55%" />

---

### ER Diagram

#### Users

<img src="/resources/images/backend/db/ER-Diagram-User.svg" alt="ER Diagram User" width="55%" />

#### Resources

<img src="/resources/images/backend/db/ER-Diagram-Data.svg" alt="ER Diagram Data" width="55%" />

### Triggers

The Database uses a few triggers to cleanup any data that needs to be removed alongside resources / users / groups when
they are removed. This needs to be done because most resource path relations to permissions don't necessarily need to be
an existing resource but can be an ant path referencing any form of resources, which would not be allowed in foreign key
relations.

### Functions

Functions are not intrinsically supported by the sqlite engine but the sqlite adapter supports runtime functions that
remain while the application is running, in the background they execute a java method to achieve said functionallity.

Example:

```java
Function.create(connection, "hashPassword",new Function() {
    @Override protected void xFunc () throws SQLException {
        String password = value_text(0);
        result(hashPassword(password));
    }
});
```

#### Available Functions

| Function      | Description                                                                              |
|---------------|------------------------------------------------------------------------------------------|
| hashpassword  | Hashes a password using the defined method from BCryptUtils                              |
| normalizePath | Normalizes a path to ensure it follows the correct format regardless of operating system |

### Connection Pooling

To increase performance and reduce the overhead of opening and closing connections to the database, a connection pool is
used, this pool is provided by the [HikariCp](https://github.com/brettwooldridge/HikariCP) dependency.

#### Configuration

The connection pool is configured with a leak detection threshold of 1000ms. In short this means that if a connection is
not closed within 1000ms of being opened, it is considered a leak and the connection is closed and removed from the
pool.

This should never be the case, if any connections stay longer open than this threshold this usually means the function
is not optimized and should be rewritten to ensure a fast and efficient REST response time.

```java
private static HikariDataSource getDataSource(Path openInPath) {
    HikariConfig hikariConfig = new HikariConfig();
    hikariConfig.setLeakDetectionThreshold(1000);
    hikariConfig.setJdbcUrl(SQLITE.driver() + openInPath.toString());
    return new HikariDataSource(hikariConfig);
}
```

#### Usage

A connection should be manually closed after use, this tells hikari to return the connection back to the pool.

```java

@Override
public boolean removeUser(RepoId repoId, UserId userId) throws CoreSqlException {
    Connection connection = database.getConnection();
    try (var statement = connection.prepareStatement("DELETE FROM Users WHERE user_id = ?")) {
        statement.setString(1, userId.id());
        return statement.executeUpdate() > 0;
    } catch (Exception e) {
        throw new CoreSqlException("Error response", e);
    } finally {
        connection.close();
    }
}
```

---

### Tables & Fields

#### `Roles`

- `role_id` (TEXT, Primary Key)
- `role_name` (TEXT)

#### `Users`

- `user_id` (TEXT, Primary Key)
- `password_hash` (TEXT)
- `created_at` (TIMESTAMP, default: `CURRENT_TIMESTAMP`)
- `created_by` (TEXT)
- `last_modified_at` (TIMESTAMP, default: `CURRENT_TIMESTAMP`)
- `last_modified_by` (TEXT)

#### `UserRoles`

- `user_id` (TEXT, Foreign Key → Users)
- `role_id` (TEXT, Foreign Key → Roles)
- **Primary Key**: (`role_id`, `user_id`)

#### `Groups`

- `group_id` (TEXT, Primary Key)
- `group_name` (TEXT)
- `created_at`, `created_by`, `last_modified_at`, `last_modified_by`

#### `UserGroups`

- `user_id` (TEXT, Foreign Key → Users)
- `group_id` (TEXT, Foreign Key → Groups)
- **Primary Key**: (`user_id`, `group_id`)

#### `Tags`

- `tag_id` (TEXT, Primary Key)
- `tag_name` (TEXT)
- `created_at`, `created_by`

#### `Resources`

- `resource_path` (TEXT, Primary Key)
- `created_at`, `created_by`, `last_modified_at`, `last_modified_by`
- `category` (TEXT)

#### `ResourceTags`

- `tag_id` (TEXT, Foreign Key → Tags)
- `resource_path` (TEXT, Foreign Key → Resources)
- `created_at`, `created_by`
- **Primary Key**: (`tag_id`, `resource_path`)

#### `GroupPermissions`

- `group_id` (TEXT, Foreign Key → Groups)
- `path` (TEXT)
- `type` (TEXT)
- **Primary Key**: (`group_id`, `path`)

#### `UserPermissions`

- `user_id` (TEXT, Foreign Key → Users)
- `path` (TEXT)
- `type` (TEXT)
- **Primary Key**: (`user_id`, `path`)

#### `AuditLog`

- `log_id` (INTEGER, Primary Key, AUTOINCREMENT)
- `user_id` (TEXT, Foreign Key → Users)
- `action` (TEXT)
- `permission_id` (TEXT)
- `timestamp` (TIMESTAMP, default: `CURRENT_TIMESTAMP`)
- `affected_userID` (TEXT, Foreign Key → Users)
- `affected_groupID` (TEXT, Foreign Key → Groups)

#### `FileData` (Virtual Table - Full Text Search)

- `resource_path` (TEXT)
- `data` (TEXT)

> Uses `fts5` with `trigram` tokenizer for full-text search.

#### `ResourceInfo` (View)

- A derived view combining `Resources` with `ResourceTags`
- Adds a virtual field: `hasTags` (BOOLEAN)

---

### Data Flow

Data is stored in an SQLite database. Each repository instance maintains its own **self-contained SQLite database file
**, which acts as the authoritative source of truth for:

- **Users and their roles**
- **Groups and their Users**
- **Permissions (user-level and group-level)**
- **Resources and their associated metadata**
- **Tags and resource-tag associations**
- **Search index data**
- **Audit logs for actions performed**

This design allows each repository to function independently, without needing a central database server, which enhances
**portability**, **isolation**, and **scalability** across multiple repositories.

#### Storage

- All entities are stored in normalized relational tables with **foreign key constraints** to maintain data integrity.
- Audit logging and timestamp fields (e.g., `created_at`, `last_modified_at`) track historical and operational metadata.
- Associated entities (e.g., `UserRoles`, `UserGroups`, `ResourceTags`) enforce **many-to-many relationships** between
  core data.

#### Access

- The database is accessed exclusively through the **backend API layer**, which exposes **predefined, secure endpoints**
  for Create, Read, Update, and Delete (CRUD) operations.
- The API ensures that only authorized users (based on roles and permissions) can access or modify data.
- On backend startup, sets up all required tables and constraints if they don't already exist.

#### Retrieval

- Resource listings and metadata can be queried directly using filters, or through the `ResourceInfo` view, which
  includes derived data like `hasTags` for more concise queries.
- Full-text content search is achieved by the `FileData` virtual table using **FTS5 with trigram tokenization**,
  allowing fast and fuzzy lookups of indexed file data.
- Tag associations and permission scopes can be resolved by joining related tables like `ResourceTags`,
  `GroupPermissions`, and `UserPermissions`.

#### Consistency

- Triggers handle **cascading updates and deletions**, such as cleaning up related records when a user or resource is
  deleted.
- Updates to key fields (like `resource_path`) are automatically propagated to all dependent tables, maintaining
  consistency without requiring manual intervention.

#### Example Flow

1. **User logs in** → API verifies credentials via `Users` and `UserRoles`.
2. **User accesses a resource** → API checks `UserPermissions` and `GroupPermissions`.
3. **User uploads a file** → A `Resources` entry is created, metadata is indexed in `FileData`, and optionally,
   `ResourceTags` are added.
4. **User deletes a tag** → Trigger deletes related entries in `ResourceTags`.
5. **Auditing** → Every action (e.g., permission change, resource update) is logged in the `AuditLog`.

<img src="/resources/images/backend/REST/Request.png" alt="Dataflow" width="30%" />

---

<div style="page-break-after: always;"></div>

## 7. Security Considerations

### Authentication & Authorization

Passwords are hashed using BCrypt with 12 salt rounds. User authentication is handled via JWT tokens, which are
generated upon successful login and validated for each subsequent request.

The authentication is handled using the springs integrated Security framework,
the configurations and filters are located inside the Doc-Api:security directory.

---

<div style="page-break-after: always;"></div>

## 8. Deployment & CI/CD Pipeline

Deployment is managed through a [Jenkins](https://www.jenkins.io/doc/) pipeline, which is defined in the `Jenkinsfile`
located in the repository.

### Build Process

The build process is initiated manually and does not occur automatically. This approach was chosen to ensure that the
build only happens when explicitly requested.

<img src="/resources/images/jenkins/Backend%20Pipeline.png" alt="Dataflow" width="160" />

#### War

The backend war is automatically created, moved to staging, then the old process is stopped and the new one is started.

---

### Configuration Files

The application's configuration is managed through the `application.yml` file. This file includes important settings for
**Cross-Origin Resource Sharing (CORS)** and **Git repository definitions**. Below is a breakdown of each section and
how to configure it.

#### Nginx

#### Jenkins

---

#### 🔗 Cross-Origin Configuration

To enable communication between your frontend applications and the backend API, you can define allowed origins under the
`crossOrigin` section.

```yaml
doc:
  web:
    api:
      crossOrigin:
        - origin: "http://localhost:8080"
          path: "/**"
        - origin: "http://localhost:4200"
          path: "/**"
```

**Explanation:**

- `origin`: The URL allowed to access the backend.
- `path`: The path pattern that the specified origin is allowed to access. It follows Ant-Path styled declaration to
  allow access to endpoints.

---

#### 📁 Git Repository Configuration

The `repositories` section defines the Git repositories that the documentation tool can access. Each repository entry
should include an identifier and a path, with additional options for read-only repositories.

```yaml
doc:
  git:
    repositories:
      - id: "testRepo1"
        path: test-temp/git/repo1
      - id: "testRepo2"
        path: test-temp/git/repo2
        isReadOnly: true        # Optional (default: false)
        dbStorage: path/to/db   # Required if isReadOnly is true
```

**Fields:**

- `id`: A unique name or identifier for the repository.
- `path`: The local file system path to the Git repository.
- `isReadOnly` *(optional)*: Set this to `true` if the repository should not be modified. Defaults to `false` if
  omitted.
- `dbStorage`: When `isReadOnly` is `true`, this field must be set to define where the associated database file should
  be stored, as it needs to be kept separate from the repository files.

---

<div style="page-break-after: always;"></div>

## 9. Documentation

### Javadoc

When using the provided jenkins pipeline

Class Documentation is automatically generated
and deployed to: `/var/www/html/javadoc`

Access is provided by nginx over the port 80 and can be accessed via `/javadoc`


<div style="page-break-after: always;"></div>

## 10. Monitoring & Logging

### Logging Strategy

Logging is done using the SLF4J framework with Logback as the implementation. Logs are categorized into different
levels:

| Code  | Description                                                               |
|-------|---------------------------------------------------------------------------|
| ERROR | For actual errors                                                         |
| WARN  | Warnings to keep track of but the application can run normally            |
| INFO  | Info logs show what the application is doing currently                    |
| DEBUG | Debug logs for developers only, does not show up in deployed applications |

<div style="page-break-after: always;"></div>

## 11. Maintenance & Future Enhancements

### Planned Features

#### Image support

Currently only text is supported unless they are directly embedded in the markdown file. Images stored and managed by
the tool does not support uploading and referencing images.

#### Github support

Currently only local repositories are supported. Github integration would allow for easier collaboration and sharing of
documentation.
