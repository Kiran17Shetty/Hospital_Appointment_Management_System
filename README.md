# Hospital Appointment Management System (HAMS)

A full-stack hospital appointment management platform built with a Spring Boot microservices backend and an Angular frontend.

## Repository Layout

- `Hospital_Appointment_Management_System_Backend/` – Spring Boot microservices backend with Eureka service discovery and API Gateway.
- `hospital-appointment-management-system-frontend/` – Angular SPA frontend.

## Overview

This project implements a hospital appointment system with three main user roles:

- **Patient**: Book, reschedule, cancel appointments, view medical history, and manage patient profile.
- **Doctor**: Publish availability, manage appointments, write prescriptions, and view profile.
- **Admin**: Review appointments, doctors, and patients.

The backend uses a microservices architecture with each service responsible for a bounded domain and service discovery managed by Eureka.

## Services

The backend contains the following services:

- `eureka-server` – service registry.
- `api-gateway` – gateway that validates JWT tokens and routes requests.
- `auth-service` – user registration, login, JWT issuance, and user lookup.
- `patient-service` – patient profile CRUD.
- `doctor-profile-service` – doctor profile CRUD.
- `doctor-service` – doctor availability, slot generation, and prescription handling.
- `appointment-service` – appointment booking, cancellation, rescheduling, and completion.
- `medical-history-service` – medical record CRUD.
- `notification-service` – sends email updates for appointment events.

## Ports

| Service | Default Port |
|---|---|
| `eureka-server` | 8761 |
| `api-gateway` | 8090 |
| `auth-service` | 8091 |
| `patient-service` | 8081 |
| `doctor-profile-service` | 8082 |
| `appointment-service` | 8083 |
| `doctor-service` | 8084 |
| `medical-history-service` | 8085 |
| `notification-service` | 8086 |
| Frontend | 4200 |

## Prerequisites

- Java 21
- Maven 3.9+
- Node.js 20+
- npm 10+
- MySQL 8

## Setup

1. Clone the repository to your machine.
2. Start MySQL and create the following databases:

```sql
CREATE DATABASE auth_db;
CREATE DATABASE patient_db;
CREATE DATABASE doctor_db;
CREATE DATABASE appointment_db;
CREATE DATABASE medical_history_db;
```

3. Configure environment variables as needed for local development.

## Environment Variables

The backend services use the following environment variables:

- `JWT_SECRET` – JWT signing key for `api-gateway` and `auth-service`.
- `DB_PASSWORD` – MySQL password used by data services.
- `MAIL_PASSWORD` – Gmail App Password for `notification-service` email delivery.

The frontend configuration is stored in `hospital-appointment-management-system-frontend/src/environments/environment.ts`.

## Running the Backend

Open a PowerShell terminal and start services in this order.

```powershell
cd .\Hospital_Appointment_Management_System_Backend\eureka-server
./mvnw spring-boot:run
```

Then start the microservices:

```powershell
cd ..\auth-service
./mvnw spring-boot:run

cd ..\patient-service
./mvnw spring-boot:run

cd ..\doctor-profile-service
./mvnw spring-boot:run

cd ..\doctor-service
./mvnw spring-boot:run

cd ..\medical-history-service
./mvnw spring-boot:run

cd ..\appointment-service
./mvnw spring-boot:run

cd ..\notification-service
./mvnw spring-boot:run
```

Finally start the gateway:

```powershell
cd ..\api-gateway
./mvnw spring-boot:run
```

Verify service registration at `http://localhost:8761`.

## Running the Frontend

```powershell
cd .\hospital-appointment-management-system-frontend
npm install
npm start
```

Open the app in your browser at `http://localhost:4200`.

## Build Commands

- Backend: `mvn clean package -DskipTests` from `Hospital_Appointment_Management_System_Backend/`.
- Frontend: `ng build --configuration production` from `hospital-appointment-management-system-frontend/`.

## Testing

- Backend tests: run `./mvnw test` inside each backend service folder.
- Frontend tests: run `npm test` inside `hospital-appointment-management-system-frontend/`.

## Documentation

- Backend README: `Hospital_Appointment_Management_System_Backend/README.md`
- Frontend README: `hospital-appointment-management-system-frontend/README.md`

## Notes

- The API Gateway is responsible for authenticating requests and adding headers required by downstream services.
- Each microservice uses its own database schema.
- Email notifications are optional and require a valid Gmail App Password.

## License

This repository does not currently specify a license. Add one if you want to make your project open source.
