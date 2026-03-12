# ✂️ Smart Barber Booking System

> A cloud-based, AI-assisted reservation and shop-management platform designed to digitize traditional barbershop appointment processes.

## 📋 Table of Contents
* [Project Vision & Impact](#-project-vision--impact)
* [Core Features](#-core-features)
* [Technology Stack](#-technology-stack)
* [System Architecture](#-system-architecture)
* [Security & Data Privacy](#-security--data-privacy)
* [Risk Management](#-risk-management)
* [Validation & Testing Plan](#-validation--testing-plan)
* [Deployment Prerequisites](#-deployment-prerequisites)
* [Contributors](#-contributors)

---

## 🎯 Project Vision & Impact
The system is built to provide a digital operating layer for small and mid-sized barbershops, offering a reliable booking engine, consistent customer communication, and actionable operational visibility. 

**Addressing Current Challenges:**
* **Phone Traffic:** Mitigates the struggle of managing appointments via phone during peak hours, aiming to resolve a ~60% missed call rate. 
* **Manual Errors:** Eliminates confusion with paper-based records, reducing the ~15% conflict rate to zero single-source scheduling. 
* **No-Shows:** Reduces missed appointments (currently at ~30%) by up to 60% through automated reminders. 
* **Business Impact:** Projects operational efficiency gains of ~2 hours/day by reducing manual admin workload, and approx. $15,000 additional annual revenue.

---

## ⚙️ Core Features
* **User Registration (FR-01):** Secure customer registration using email and phone numbers. 
* **Appointment Booking (FR-02):** 24/7 self-service booking allowing customers to select staff, services, date, and time. 
* **AI Style Preview (FR-03):** Customers can securely upload photos and see hairstyle previews on their own faces using a Python-based AI service. 
* **Payment Integration (FR-04):** Secure payments accepted directly through the system. 
* **Notification System (FR-05):** Automated SMS and email sent for appointment confirmations and reminders. 
* **Admin Dashboard (FR-06):** A central command center for business owners to manage staff, services, schedules, and daily revenue statistics. 

---

## 💻 Technology Stack
The platform uses a web-first stack with a dedicated API backend and supporting services for AI processing and asynchronous tasks. 

* **Frontend:** React 18, Tailwind CSS 
* **Backend:** .NET Web API (C#) 
* **AI Service:** Google Nano Banana API (Python Image Processing) 
* **Database:** PostgreSQL (Primary), Redis (Caching & Background Jobs) 
* **DevOps & Infrastructure:** Docker (Containerization), AWS S3, Git/GitHub, Jira 

---

## 🏗️ System Architecture
The solution follows an N-Tier architecture designed to be cloud-ready and containerized for repeatable deployment. 

* **Client Layer:** Initiates booking requests, photo uploads, and secure payment transactions. 
* **Core Application Layer (.NET Core):** Processes requests, checks for scheduling conflicts using server-side slot calculation, executes the AI engine, and triggers notifications. 
* **Data Storage Layer:** PostgreSQL persists user profiles, appointments, and barber schedules. 
* **Concurrency Control:** To prevent double bookings, the database performs a transaction lock on the selected row during the confirmation process.

---

## 🔐 Security & Data Privacy
The architecture is based on the "Least Privilege" principle, strictly separating Customer, Staff, Manager, and Admin capabilities. 

* **Authentication:** All API requests are protected via `/api/auth/*` endpoints using JSON Web Tokens (JWT). 
* **Resource Scoping:** Users can only view and edit their own appointments and data via JWT claims. 
* **Data Encryption:** All data transfers are mandatorily executed over HTTPS, and user passwords are hashed in the database.
* **Compliance:** Fully compliant with GDPR and KVKK standards, applying PII (Personally Identifiable Information) minimization. 
* **AI Artifact Security:** Photos uploaded for the AI Style Preview are encrypted using AES-256 and automatically deleted permanently from the AWS S3 bucket within 24 hours. 

---

## 🚦 Risk Management
* **API Downtime:** Mitigated by implementing retry logic and circuit breaker patterns in the frontend. 
* **Server Overload:** Addressed by utilizing Redis caching to reduce database hits and horizontally scaling Docker containers. 
* **AI Processing Latency:** Handled by running image processing tasks as asynchronous background jobs to prevent UI freezing.
* **Appointment Overrun:** Prevented by automatically appending a mandatory 15-minute buffer time to the duration of every scheduled service. 

---

## 🧪 Validation & Testing Plan
To ensure zero-fault tolerance required for the appointment logic, the system utilizes a multi-layer testing strategy:

1. **Automated End-to-End (E2E) Testing:** The React client is subjected to automated UI tests using Java and Selenium (or similar frameworks) to verify seamless 4-step booking flows and AI image uploads. 
2. **API Integration Testing:** Concurrent requests are simulated against the `/api/appointments` endpoint using tools like REST Assured or Postman to confirm that transaction locks absolutely prevent double bookings.
3. **Unit Testing:** Core business logic components, specifically `SlotCalculator` and `AppointmentController`, are tested in isolation. 
4. **Performance Testing:** Ensures base API response times remain under 200ms under normal system load and verifies Redis caching efficiency. 

---

## 🚀 Deployment Prerequisites
The system adopts a containerized deployment strategy for scalability. 

* Docker engine (local or cloud host) to run the backend and supporting services.
* Access to persistent storage for PostgreSQL data and backups.
* HTTPS setup (domain + TLS certificate) for secure client-to-API communication. 
* Configuration secrets: DB connection settings, JWT signing secret, AWS S3 credentials, and Redis connection settings. 

---

## 👥 Contributors
* **Tolga Ertunç** (B2280.060052) 
* **İlke Görkem Şahin** (B2180.060042)
