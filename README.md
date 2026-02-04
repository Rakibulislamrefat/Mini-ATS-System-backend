# Mini ATS (Applicant Tracking System)

A comprehensive full-stack Applicant Tracking System designed to streamline the recruitment process. This application allows HR professionals and recruiters to manage candidates, schedule interviews, and track recruitment progress through an intuitive dashboard.

## 🚀 Features

-   **Authentication**: Secure user registration and login (JWT-based).
-   **Dashboard**: Real-time overview of total candidates, interview stages, and hiring stats.
-   **Candidate Management**:
    -   Add, view, update, and delete candidates.
    -   Bulk import candidates via Excel (.xlsx).
    -   Track candidate status (Applied, Scheduled, Passed, Hired, Rejected).
-   **Interview Management**:
    -   Schedule First and Second round interviews.
    -   Manage interview details (Date, Duration, Platform, Meeting Link).
    -   Track interview outcomes.
-   **Responsive Design**: Built with a mobile-first approach using Tailwind CSS.

## 🛠 Tech Stack

### Backend
-   **Runtime**: Node.js
-   **Framework**: Express.js
-   **Database**: MongoDB (Mongoose ODM)
-   **Authentication**: JSON Web Tokens (JWT) & bcryptjs
-   **File Handling**: Multer (with Excel parsing support)
-   **Deployment**: Vercel (Serverless function optimization)

### Frontend
-   **Framework**: React (Vite)
-   **Language**: TypeScript
-   **Styling**: Tailwind CSS & shadcn/ui components
-   **State Management**: Redux Toolkit
-   **Routing**: React Router DOM
-   **HTTP Client**: Axios

## 📋 Prerequisites

Before running the project, ensure you have the following installed:
-   [Node.js](https://nodejs.org/) (v14 or higher)
-   [MongoDB](https://www.mongodb.com/) (Local or Atlas connection string)
-   [Git](https://git-scm.com/)

## ⚙️ Installation & Setup

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd Mini_ATS_system
```

### 2. Backend Setup
Navigate to the backend directory and install dependencies:
```bash
cd backend
npm install
```

Create a `.env` file in the `backend` directory:
```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRE=30d
```

Start the backend server:
```bash
# Development mode
npm run dev

# Production mode
npm start
```
The server will run on `http://localhost:5000`.

### 3. Frontend Setup
Navigate to the frontend directory and install dependencies:
```bash
cd ../frontend
npm install
```

Create a `.env` file in the `frontend` directory:
```env
VITE_API_URL=http://localhost:5000/api
```

Start the frontend development server:
```bash
npm run dev
```
The application will run on `http://localhost:5173`.

## 🧪 Development Workflow

1.  **Version Control**:
    -   Commit code regularly with clear messages (e.g., `feat: add candidate import`, `fix: interview scheduling bug`).
    -   Use feature branches for major changes.

2.  **Testing**:
    -   Test API endpoints using Postman or Insomnia.
    -   Verify frontend responsiveness on different screen sizes (Mobile, Tablet, Desktop).
    -   Check error handling (e.g., duplicate emails, invalid file formats).

3.  **Styling**:
    -   Uses Tailwind CSS for utility-first styling.
    -   Components are built for reusability and consistency.

## 🚀 Deployment (Vercel)

### Backend
1.  Install Vercel CLI or connect your GitHub repo to Vercel.
2.  Set `MONGO_URI` and other env vars in Vercel Project Settings.
3.  The project includes `vercel.json` configuration for serverless deployment.

### Frontend
1.  Connect your GitHub repo to Vercel.
2.  Set `VITE_API_URL` to your deployed backend URL (e.g., `https://your-backend.vercel.app/api`).
3.  Deploy!

## 📂 Project Structure

```
Mini_ATS_system/
├── backend/                # Node.js + Express API
│   ├── src/
│   │   ├── config/         # DB connection
│   │   ├── controllers/    # Route logic
│   │   ├── models/         # Mongoose schemas
│   │   ├── routes/         # API routes
│   │   └── middleware/     # Auth & Upload middleware
│   └── api/                # Vercel entry point
│
└── frontend/               # React + TypeScript App
    ├── src/
    │   ├── components/     # Reusable UI components
    │   ├── features/       # Redux slices
    │   ├── pages/          # Application views
    │   └── services/       # API services
    └── public/             # Static assets
```

## 🗄️ Database Schema & Design

The application uses MongoDB with the following collections and relationships:

### Collections

#### 1. Users (`users`)
Stores system users (Recruiters/Admins).
- **Fields**:
  - `name` (String): Full name
  - `email` (String): Unique email address
  - `password` (String): Hashed password
  - `role` (String): User role (e.g., 'admin', 'recruiter')
  - `isActive` (Boolean): Account status
  - `createdAt`: Timestamp

#### 2. Candidates (`candidates`)
Stores applicant information.
- **Fields**:
  - `name` (String): Candidate name
  - `email` (String): Contact email
  - `phone` (String): Contact number
  - `age` (Number): Candidate age
  - `yearsOfExperience` (Number): Total experience
  - `skills` (Array of Strings): List of technical skills
  - `status` (String): Current status (e.g., 'Applied', 'Scheduled', 'Hired')
  - `createdAt`, `updatedAt`: Timestamps

#### 3. Interviews (`interviews`)
Stores interview schedules and results.
- **Fields**:
  - `candidate` (ObjectId): Reference to `Candidate`
  - `type` (String): Interview round ('first', 'second')
  - `scheduledAt` (Date): Date and time of interview
  - `duration` (Number): Duration in minutes
  - `meetingPlatform` (String): e.g., 'Google Meet', 'Zoom'
  - `meetingLink` (String): URL for the meeting
  - `status` (String): 'scheduled', 'completed', 'cancelled'
  - `result` (String): 'passed', 'failed', 'pending'
  - `createdAt`, `updatedAt`: Timestamps

### Relationships

- **One-to-Many**: One Candidate can have multiple Interviews (though typically tracked sequentially).
- **Reference**: The `interviews` collection references the `candidates` collection via the `candidate` field (ObjectId).



