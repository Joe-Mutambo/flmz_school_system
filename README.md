# School Management System for Vulnerable Children (Prototype)

**Date:** May 12, 2025  
This prototype web application was developed to address data management challenges for vulnerable children. It provides a unified platform for role-based data collection, monitoring, and reporting.

---

## 📐 1. System Architecture & Data Model

### Architecture Overview

- **Frontend**
  - **Framework:** React.js (Vite + TypeScript)
  - **Styling:** Tailwind CSS
  - **Routing:** React Router
  - **State Management:** React Context API (AuthContext)
  - **Forms:** Formik + Yup
  - **Data Viz:** Chart.js via react-chartjs-2

- **Backend**
  - **Platform:** Supabase (BaaS)
  - **Authentication:** Supabase Auth
  - **Database:** PostgreSQL (hosted by Supabase)
  - **Edge Functions:** RPC (PostgreSQL Functions)
  - **Security:** Supabase Row-Level Security (RLS)
  - **(Planned)** Storage & Realtime Subscriptions

### Data Model Summary

| Table | Description |
|-------|-------------|
| `roles` | User roles (super_admin, admin, field_officer, teacher) |
| `users` | User profiles (linked to auth.users & roles) |
| `schools` | Participating school data |
| `school_staff` | Links users to schools |
| `children` | Core child information |
| `guardians` | Guardian details |
| `home_visits` | Field officer visit logs |
| `vulnerability_assessments` | Yearly assessment records |
| `literacy_assessments` | Teacher-submitted assessments |
| `issues` | Issues reported for a child |
| `issue_updates` | Status change/update logs |

Refer to `schema.sql` for complete definitions.

---

## ✅ 2. Features & Limitations

### ✅ Implemented

- **Unified Data Storage** in Supabase
- **Role-Based Login & Page Access**
- **Basic RLS Enforcement**
- **Child Management** (View/Add/Edit)
- **Smart Forms** (Home Visits, Literacy, Vulnerability, Issues, Guardian Info)
- **Historical Record Access** (linked to children)
- **Issue Tracking** (status, updates)
- **Basic Dashboards** using Chart.js + Supabase RPC

### ⚠️ Limitations

- UI lacks polish and responsiveness
- No real-time features
- File upload (e.g. birth records) not implemented
- Error handling is basic
- No PWA/offline capability
- No Admin UI for user/role management
- Testing is minimal (manual/dev testing only)
- No migration from Google Sheets/JotForm

---

## 🧰 3. Technologies & Rationale

| Tool | Purpose |
|------|---------|
| **React + Vite + TS** | Modern, fast, type-safe UI dev |
| **Supabase** | Full BaaS stack (DB, Auth, RPC) |
| **Tailwind CSS** | Rapid, utility-first UI styling |
| **Formik + Yup** | Form logic + validation |
| **Chart.js** | Dashboards & analytics charts |
| **PostgreSQL + RLS** | Structured, secure data model |

---

## ⚙️ 4. Installation & Setup

### 🔧 Prerequisites

- Node.js v18+
- Supabase account

### 🚀 Steps

1. **Clone**
   ```bash
   git clone <repository_url>
   cd <project_directory>
Install

bash
Copy
Edit
npm install
Setup Supabase

Create a project at supabase.io

In SQL Editor, run schema.sql, rpc_functions.sql, seed.sql (if provided)

Configure .env

env
Copy
Edit
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
Start Dev Server

bash
Copy
Edit
npm run dev
Access App
Open http://localhost:<port>, the port where your application is running in your browser.

🚧 5. Roadmap
🔒 RLS & RPC Audits

🗂️ Guardian UI Enhancements

📁 Supabase Storage Integration

🔔 Issue Notifications & Comments

🔄 Data Migration Tools (from Google Sheets/JotForm)

🧪 End-to-End Testing

📱 Offline/PWA Support

👤 User & Role Management UI

🎨 UI/UX Enhancements

📊 Dashboard Enhancements

👥 Test Accounts
Field Officer: field_officer_test@example.com / 123@Pazzz
Teacher: teacher_test@example.com / 123@Pazzz
📄 License
MIT

