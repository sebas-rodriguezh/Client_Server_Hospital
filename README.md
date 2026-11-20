# Hospital Management System

Client-server hospital management system built with Java, JavaFX, sockets and MySQL.

## Description

Desktop application for managing hospital prescriptions. A JavaFX client connects to a multithreaded socket server that handles the business logic and the MySQL database. Doctors prescribe medications to patients, pharmacists move each prescription through its fulfillment process, and administrators manage staff, patients and the medication catalog. Connected users can also talk to each other through a built-in chat.

## Features

- Client-server architecture over TCP sockets, with a server that handles multiple clients through a thread pool
- Role-based login (Admin, Doctor, Pharmacist) and password change
- Staff, patient and medication management for administrators
- Prescription creation with medications, quantity, duration and instructions
- Prescription workflow with states: Created, In Process, Ready and Delivered
- Prescription history and search by patient
- Dashboard with charts: medications prescribed per month and prescriptions by status
- Real-time chat between connected users on a separate chat server
- Asynchronous requests so the interface does not freeze while waiting for the server
- MySQL persistence with connection pooling (HikariCP)

## Tech Stack

- **Language:** Java
- **UI:** JavaFX (FXML)
- **Communication:** TCP sockets, multithreading (ExecutorService)
- **Database:** MySQL, HikariCP
- **Build:** Maven (multi-module: shared model, backend and frontend)
- **IDE:** IntelliJ IDEA

## Project Structure

```
├── src/          # Shared model (Patient, Prescription, Medication, Staff...) and SQL scripts
├── backend/      # Socket server, business logic and data access
└── frontend/     # JavaFX client (views, controllers and service proxies)
```

## How to Run

### Prerequisites

- JDK 24
- MySQL 8
- IntelliJ IDEA (recommended) or Maven

### 1. Create the database

Run the scripts in `src/bd_scripts/` in this order:

1. `create_bd_schema.sql`
2. `tabla_personal.sql`
3. `pacientes.sql`
4. `medicamentos.sql`
5. `recetas.sql`
6. `detalle_medicamentos.sql`

### 2. Configure the database connection

Edit `backend/src/main/resources/db.properties` with your MySQL credentials:

```properties
db.url=jdbc:mysql://localhost:3306/sistema_hospital
db.user=YOUR_USER
db.password=YOUR_PASSWORD
db.pool.size=10
```

### 3. Install the shared model

From the project root:

```bash
./mvnw install -DskipTests        # Windows: mvnw.cmd install -DskipTests
```

### 4. Start the server

Run `backend/src/main/java/org/example/backend/Servicios/HospitalServer.java` from IntelliJ. The server listens on port `8080` for requests and on port `7000` for the chat.

### 5. Start the client

```bash
cd frontend
./mvnw javafx:run                 # Windows: mvnw.cmd javafx:run
```

You can open several clients at the same time to test the chat between users.

### Test users

| Role | ID | Password |
|---|---|---|
| Admin | `admin` | `1234` |
| Doctor | `1111` | `1111` |
| Pharmacist | `2222` | `2222` |

## Team

Built with [Alejandro Calderón](https://github.com/AleCalderon1711), [victoriaacs](https://github.com/victoriaacs) and [Laura (lif964)](https://github.com/lif964).
