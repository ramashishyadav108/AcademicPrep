# AcademicPrep (EduTech Platform)

## 📌 Project Overview
AcademicPrep is a comprehensive, modern EdTech platform built with a **microservices-oriented backend architecture** and a **React-based single-page application** frontend. It enables instructors to create, manage, and sell courses while providing students with an interactive learning environment, secure payments, peer-to-peer discussions, and AI-powered study sessions.

---

## 🏗️ Architecture & Tech Stack

### Frontend (`/frontend`)
The frontend is a robust **React 18** application leveraging modern state management and UI libraries.
- **UI Frameworks:** React.js, TailwindCSS
- **State Management:** Redux Toolkit (`@reduxjs/toolkit`, `react-redux`)
- **Authentication:** Auth0 (`@auth0/auth0-react`), JWT Decode
- **Real-Time Communication:** Socket.io-Client (for discussions & live features)
- **AI Integration:** Google Cloud AI Platform (`@google-cloud/aiplatform`)
- **Icons & Components:** Lucide-React, React-Icons, Swiper (sliders), React-Dropzone
- **Charts & Data Visualization:** Chart.js, React-Chartjs-2
- **Routing:** React Router v7

### Backend (`/backend`)
The backend is highly modularised using a **Microservices Architecture**. It has an `api-gateway` that routes incoming traffic to the appropriate dedicated services. All microservices share common utilities through a local `shared-utils` package.

#### Microservices:
1. **`api-gateway`**: Acts as the single entry point for the frontend, routing traffic to downstream microservices using `http-proxy-middleware`.
2. **`user-service`**: Handles Authentication, User Profiles, Contact requests, Password Resets, and Instructor Applications.
3. **`course-service`**: Manages all course-related data (Courses, Categories, Sections, Subsections), Course Progress tracking, Ratings & Reviews, and real-time Discussions via `socket.io`.
4. **`payment-service`**: Handles payment transactions, Razorpay integrations, and Refund Requests.
5. **`ai-service`**: Provides AI-driven features (SmartStudy) communicating with Cloud AI resources.
6. **`shared-utils`**: Contains common middleware (Auth, Input Sanitization), Database Config (MongoDB/Mongoose), Email Services (NodeMailer with templates), Image Uploader (Cloudinary), and networking utils.

- **Backend Tech Stack:** Node.js, Express.js, MongoDB (Mongoose), Socket.io, Razorpay (Payments).

---

## 🚀 Key Features

* **Authentication & Authorization**: Secure login via JWT and Auth0 integration.
* **Course Catalog & Filtering**: Browse courses organized by diverse categories.
* **Interactive Learning via Video**: Embedded highly-optimized video learning components.
* **Real-time Discussions**: Peer-to-peer discussions using WebSockets (`socket.io`).
* **Instructor Dashboard**: Dedicated dashboard allowing educators to publish sections, upload videos, and track course success.
* **Payments & Cart**: Deep integration with Razorpay out of the box for handling course purchases.
* **AI SmartStudy**: Advanced ML/AI endpoints to recommend and guide student coursework using Google Cloud AI.
* **Progress Tracking & Certifications**: Granular tracking on student's progression.

---

## 📁 Repository Structure

```
AcademicPrep/
│
├── backend/
│   ├── api-gateway/       # API Gateway proxy service
│   ├── ai-service/        # SmartStudy features & controllers
│   ├── course-service/    # Course management API & socket integration
│   ├── payment-service/   # Razorpay processing and transactions
│   ├── user-service/      # Authentication, Profiles, OTP
│   └── shared-utils/      # Common utilities (Auth, DB, Emails, Uploads)
│
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/    # Reusable React UI components
│       ├── contexts/      # React contexts (e.g., SocketContext)
│       ├── pages/         # High-level screens
│       ├── slices/        # Redux slices
│       └── services/      # Frontend API integration
│
└── render.yaml            # Render Deployment Configuration
```

---

## 💻 Local Setup & Development

**Prerequisites:** Node.js (v18+ recommended), MongoDB, and a Razorpay Developer Account.

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   cd AcademicPrep
   ```

2. **Setup Environment Variables:**
   - Add a `.env` file to the root of each microservice (`user-service`, `course-service`, `payment-service`, `ai-service`).
   - Add a `.env` in the `frontend` folder for React environment variables.

3. **Install Dependencies:**
   Navigate into the `backend/*` folders and `frontend` folder to install dependencies.
   ```bash
   cd frontend && npm install
   cd ../backend/api-gateway && npm install
   # Repeat for other backend microservices
   ```
   *(Note: The microservices use `shared-utils` via local `file:../shared-utils` reference. Run `npm install` gracefully inside them).*

4. **Starting the Application:**
   Run each backend service individually or use a process runner/Docker (if configured).
   ```bash
   # Frontend
   npm start
   
   # Backend Gateway
   npm run dev
   ```

## ☁️ Deployment
The project aims toward continuous deployment using **Render**, utilizing the root `render.yaml` infrastructure-as-code file to automatically provision environments for each microservice and the frontend.
