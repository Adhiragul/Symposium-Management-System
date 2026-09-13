# SRM EEC SympoSphere - College Symposium & Workshop Management System

A full-stack **MERN** (MongoDB, Express, React, Node.js) web application tailored for **Easwari Engineering College (Autonomous) - SRM Group, Ramapuram, Chennai**.

This portal enables campus academic departments and student clubs to publish events, track live seating capacity with atomic concurrency, accept single-click student RSVPs, and export attendee rosters in **CSV** and **JSON** formats.

---

## 🌟 Key Highlights & Features

1. **SRM EEC Specialized Departments**:
   - **Cybersecurity (CS)**: Capture the Flag (CTF), Threat Hunting, Cyber Defense.
   - **Robotics and Automation (RA)**: ROS 2, Industrial Manipulators, LiDAR SLAM.
   - **Electrical and Electronics Engineering (EEE)**: Smart Grids, EV Powertrains, Power Electronics.
   - **Computer Science & Engineering (CSE)**: Competitive coding arena, Hackathons.
   - **Artificial Intelligence & Data Science (AI&DS)**: GenAI, RAG, Deep Learning.
   - **Information Technology (IT)**: Cloud Native, Kubernetes, DevOps.
   - **Electronics & Communication Engineering (ECE)**: IoT, Embedded Systems.

2. **Single-Click RSVP with Atomic Concurrency**:
   - High-concurrency safe seat reservation using MongoDB atomic queries (`seatsAvailable > 0` with `$inc: { seatsAvailable: -1 }`).
   - Prevents race conditions and overbooking when multiple students RSVP simultaneously.
   - Instant celebratory feedback with confetti animation.
   - Digital Entry Pass generation with unique ticket ID (e.g. `EEC-CYS-849201`) and scannable QR code.
   - Self-service cancellation that automatically returns the seat to the available pool.

3. **Multi-Criteria Event Filtering & Discovery**:
   - Filter by Department (including quick pills for Cybersecurity, Robotics & Automation, EEE, CSE, IT).
   - Filter by Category (Symposium, Workshop, Hackathon, Paper Presentation, Seminar, Technical Contest).
   - Filter by Availability ("Available Seats Only").
   - Instant real-time search across event titles, descriptions, and tags.
   - Sort by Date (upcoming/latest), Remaining Seats, or Total Capacity.

4. **Administrative Attendee Roster & Export (CSV & JSON)**:
   - Dedicated organizer attendee view for each published symposium/workshop.
   - **Export to CSV**: Formatted according to RFC 4180 with standard headers for Microsoft Excel and Google Sheets (`Ticket ID`, `Student Name`, `College Email`, `Department`, `Roll No`, `Attendance Status`, `Timestamp`).
   - **Export to JSON**: Structured data payload for integration with college academic databases.
   - One-click check-in toggle directly on the dashboard to mark students **Present** or **Absent**.

5. **Zero-Config Database Fallback**:
   - Connects to local MongoDB or MongoDB Atlas if `MONGODB_URI` is provided in `.env`.
   - Automatically falls back to an embedded `mongodb-memory-server` if no daemon is detected, auto-seeding sample symposiums and test accounts for instant out-of-the-box evaluation.

---

## 👥 Demo Accounts (Pre-seeded)

| Role | Email | Password | Department / Details |
| :--- | :--- | :--- | :--- |
| **Club Organizer / Faculty** | `organizer@eec.srmrmp.edu.in` | `Admin@123` | Prof. R. Venkatesh (Cybersecurity Dept Coordinator) |
| **Student Attendee** | `student@eec.srmrmp.edu.in` | `Student@123` | Adhiragul S (3rd Year, Roll No: `310621205001`) |
| **Robotics Student** | `karthik.ra@eec.srmrmp.edu.in` | `Student@123` | Karthik Narayanan (Robotics & Automation) |
| **EEE Student** | `swetha.eee@eec.srmrmp.edu.in` | `Student@123` | Swetha Raman (Electrical & Electronics) |

> 💡 *Tip: The portal includes 1-click demo login buttons in the navigation bar and on the Sign In page for rapid testing!*

---

## 🚀 Quick Start Guide

### Prerequisites
- [Node.js](https://nodejs.org/) (v18 or v20+ recommended)
- npm (installed with Node.js)

### 1. Install Dependencies
Run in the root directory:
```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### 2. Start Backend & Frontend

#### Option A: Run Both Together (Recommended)
From the root directory:
```bash
npm run dev
```

#### Option B: Run Individually
**Terminal 1 (Backend API):**
```bash
cd backend
npm run dev
```
*API runs at `http://localhost:5000`*

**Terminal 2 (Frontend Client):**
```bash
cd frontend
npm run dev
```
*Web application runs at `http://localhost:3000`*

---

## 📡 API Endpoints Reference

### Authentication (`/api/auth`)
- `POST /api/auth/register` - Create student or organizer account.
- `POST /api/auth/login` - Authenticate with email/password and obtain JWT.
- `GET /api/auth/me` - Retrieve current logged-in user profile.

### Events (`/api/events`)
- `GET /api/events` - List events with query filters (`department`, `category`, `search`, `availableOnly`, `sort`).
- `GET /api/events/metadata` - Fetch available SRM EEC departments, categories, and venues.
- `GET /api/events/:id` - Fetch single event details with organizer information.
- `POST /api/events` - Publish a new event *(Organizer/Admin only)*.
- `PUT /api/events/:id` - Update event specifications *(Event Organizer only)*.
- `DELETE /api/events/:id` - Remove event and clean registrations *(Event Organizer only)*.

### Registrations & RSVP (`/api/registrations`)
- `POST /api/registrations/rsvp/:eventId` - Concurrency-safe atomic RSVP and ticket reservation.
- `POST /api/registrations/cancel/:registrationId` - Cancel registration and reclaim seat.
- `GET /api/registrations/my-registrations` - List current student's registered passes.
- `GET /api/registrations/status/:eventId` - Check RSVP status for an event.
- `GET /api/registrations/event/:eventId/attendees` - Fetch event attendee roster *(Organizer only)*.
- `PATCH /api/registrations/:id/checkin` - Toggle attendance status *(Organizer only)*.

### Attendee Data Export (`/api/export`)
- `GET /api/export/event/:eventId/csv` - Download RFC 4180-compliant CSV attendee roster.
- `GET /api/export/event/:eventId/json` - Download structured JSON attendee dataset.

### Analytics & Statistics (`/api/stats`)
- `GET /api/stats/dashboard` - Get overall KPIs (total capacity, seats filled %, attendance %).

---

## 🏗️ Tech Stack

- **Frontend**: React 19, Vite, Tailwind CSS, Lucide Icons, Canvas Confetti, QRCode.React, React Router DOM v7, Axios.
- **Backend**: Node.js, Express.js, Mongoose ODM, JSONWebToken, Bcrypt.js, Json2csv.
- **Database**: MongoDB (supports local MongoDB, MongoDB Atlas, and embedded `mongodb-memory-server` zero-config fallback).

---

## 🏛️ Institution Context
**Easwari Engineering College (Autonomous)**
Approved by AICTE, Affiliated to Anna University, Accredited by NAAC with 'A' Grade, NBA Accredited.
*Bharathi Salai, Ramapuram, Chennai - 600089, Tamil Nadu, India.*
