# Backend Authentication System (Express & Mongoose)

A professional-grade, full-stack ready backend authentication system built using **Express 5** and **Mongoose (MongoDB)**. It implements a robust authentication lifecycle, including user registration with email verification, secure login with automated JWT access/refresh token dual-cookie management, password reset flows, and structural DTO validation middlewares.

---

## 🚀 Key Features

* **Robust JWT Authentication System:** Dual-token mechanism utilizing a short-lived `accessToken` and a long-lived, rotation-capable `refreshToken` securely hashed and persisted in MongoDB.
* **Layered Structural DTO Validation:** Custom validation layer powered by **Joi** that enforces structural integrity, strips unauthorized fields, and intercepts invalid requests before hitting controllers.
* **Secure Email Lifecycle (Nodemailer):** Automated transactional mail delivery using SMTP transport configurations to manage both signup account activations and secure account recovery workflows.
* **Advanced Mongoose Schemas & Hooks:** Automatic background pre-save password encryption using salt-hashed `bcryptjs` routines and explicit field isolation boundaries (`select: false`) for maximum security.
* **Role-Based Access Control Middleware:** Production-ready authentication and authorization guards to selectively restrict routes based on administrative privileges (`customer`, `seller`, `admin`).

---

## 🛠️ Architecture & Project Directory Structure

The project follows a modular architecture, segregating global frameworks (`common`) from feature-specific runtime boundaries (`modules/auth`).

```text
backend-cohort/
├── server.js                        # Application entry point & Database initialization
└── src/
    ├── app.js                       # Express application bootstrap & core middlewares
    ├── common/                      # Global shareable abstractions
    │   ├── config/
    │   │   ├── db.js                # Database connection configuration
    │   │   └── email.js             # Nodemailer transporter and templates
    │   ├── dto/
    │   │   └── base.dto.js          # Core Joi validation wrapper
    │   ├── middleware/
    │   │   └── validate.middleware.js # Middleware wrapper for DTO requests
    │   └── utils/
    │       ├── api-error.js         # Central operational error builder
    │       ├── api-response.js      # Structured HTTP response helper
    │       └── jwt.utlis.js         # JWT generation, verification, and crypto helpers
    └── modules/
        └── auth/                    # Complete encapsulated Authentication module
            ├── auth.controller.js   # HTTP Request/Response orchestration handles
            ├── auth.middleware.js   # Protection guards & RBAC authorization filters
            ├── auth.model.js        # Mongoose User Schema & Schema Hooks
            ├── auth.route.js        # Dedicated auth URI mappings
            ├── auth.service.js      # Core logical business transactions
            └── dto/                 # Feature-specific validation payload DTOs
                ├── forgot-password.dto.js
                ├── login.dto.js
                ├── register.dto.js
                └── reset-password.dto.js