# flmz_school_system

Project Documentation: School Management System for Vulnerable Children (Prototype)
Date of the README: May 12, 2025

This documentation provides an overview of the prototype web application developed to address data management challenges for vulnerable children served by your organization.

1. System Architecture and Data Model
The prototype follows a modern web application architecture designed for rapid development, scalability, and maintainability, leveraging a Backend-as-a-Service (BaaS) model.

Architecture
Frontend:
Framework: React.js (using Vite with TypeScript) for building a reactive and component-based user interface.
Styling: Tailwind CSS for utility-first styling, enabling rapid development of a responsive UI.
Routing: React Router for client-side navigation between pages.
State Management: React Context API (specifically AuthContext) for managing user authentication state and profile information globally.
Forms: Formik for form state management and Yup for schema-based validation, streamlining form handling.
Data Visualization: Chart.js (with react-chartjs-2) for rendering charts on the dashboard.
Backend:
Service: Supabase (Backend-as-a-Service)
Authentication: Manages user login (email/password) and session handling.
Database: PostgreSQL database hosted by Supabase, providing relational data storage.
Storage: (Planned) Supabase Storage for handling file uploads like birth records (not implemented in prototype).
Realtime: (Planned) Supabase Realtime subscriptions for features like live issue updates (not implemented in prototype).
Edge Functions / RPC: Supabase Edge Functions (implemented as Postgres Functions callable via RPC) for server-side data aggregation needed for dashboard statistics.
Security: Relies heavily on Supabase Auth and PostgreSQL Row-Level Security (RLS) policies to enforce role-based access control directly at the database level.
Data Model
The PostgreSQL database schema includes the following main tables with relationships enforced by foreign keys:

roles: Defines user roles (super_admin, admin, field_officer, teacher).
users: Stores user profile information, linked to auth.users and roles.
schools: Information about participating schools (Legacy Academy, Government).
school_staff: Links users (teachers) to specific schools.
children: Core table storing detailed information about each child.
guardians: Stores information about the guardians associated with each child.
home_visits: Records details from home visits conducted by field officers.
vulnerability_assessments: Stores data from annual vulnerability assessments.
literacy_assessments: Records literacy assessment results entered by teachers.
issues: Tracks issues reported concerning a child (health, safety, etc.).
issue_updates: Logs updates and status changes for each issue.
(Refer to the detailed schema definitions in the SQL setup scripts for specific fields, types, and constraints).

2. Features Implemented and Limitations
This prototype was developed under a tight timeframe (~1.5 days) and demonstrates core functionalities addressing the key challenges outlined in the assessment.

Implemented Features
Unified Data Storage: All data (children, guardians, visits, assessments, issues) is stored in a central Supabase PostgreSQL database.
Role-Based Authentication: Users can log in with pre-defined test accounts representing different roles (Teacher, Field Officer).
Role-Based Access Control (Basic):
Page access is restricted based on user role using Protected Routes.
Data visibility is filtered based on role via Supabase Row-Level Security (RLS) policies (e.g., Teachers see only their school's children). Fetching logic respects RLS.
Conditional UI elements (e.g., "Add Child" button visible only to specific roles).


Children Management:
List view of children (filtered by role).
Detailed child view page displaying basic info and tabs for related records.
Form for adding and editing child information (accessible by Admin/Field Officer).

Data Entry Forms (Core Functionality):
Forms implemented using Formik & Yup for:
Home Visits (Field Officer)
Literacy Assessments (Teacher)
Vulnerability Assessments (Field Officer - complex form structure implemented)
Issue Reporting (Teacher/Field Officer)
Guardian Info (Add/Edit, Field Officer/Admin)
"Smart" pre-filling: Child's name/ID is displayed on context-specific forms.
Historical Data Access: The Child Detail page displays lists of past Home Visits, Literacy Assessments, Vulnerability Assessments, and Issues associated with the child.

Issue Tracking (Basic):
Issues can be reported via a dedicated form.
Issues are listed on the Child Detail page.
A dedicated Issue Detail page shows full issue information and a history of updates.
Functionality to add new updates and change the status of an issue is implemented.


Dashboard (Basic):
Role-specific dashboard view.
Uses Supabase RPC functions for data aggregation (e.g., issues by status, children per school).
Integrates Chart.js to display basic Pie and Bar charts for key metrics.


Limitations
Time Constraint: The 3-day assessment timeline (effectively ~1.5 days of coding) meant not all features could be fully polished or implemented.
UI/UX: The user interface is functional using Tailwind CSS but lacks significant visual polish and advanced usability features. Responsiveness is basic.
RLS Complexity: While basic RLS is implemented, complex scenarios and edge cases require further refinement and rigorous testing. SECURITY DEFINER functions need careful review.
Error Handling: Basic error handling is present, but comprehensive user feedback (e.g., toasts) and logging are minimal.
Smart Data Collection: Limited to displaying child context; more advanced logic (e.g., skipping already answered questions from recent assessments) is not implemented.
Issue Update Atomicity: Updating an issue's status and adding an update log are done via separate awaits; using a database transaction (via RPC) would be more robust.
Guardian Management: Basic Add/Edit form provided; integration into the Child Detail page UI (e.g., via modal) could be improved.
File Storage: Functionality for uploading documents (e.g., birth records) is not implemented.
Real-time Features: No real-time updates implemented (e.g., for new issues).
Testing: Primarily developer testing; requires dedicated QA, unit, and integration tests.
Data Migration: No tools or scripts developed for migrating existing data from JotForm/Google Sheets.
Offline Capabilities: The application requires an active internet connection.
User Management UI: No interface for Admins to manage users or roles within the app (requires direct Supabase interaction).


3. Technologies Used and Rationale
React.js (Vite + TypeScript): Chosen for its component-based architecture, strong community support, performance (with Vite), and type safety (with TypeScript), enabling efficient development of complex UIs.
Supabase: Selected as the BaaS provider due to its integrated offering:
PostgreSQL: A robust, open-source relational database.
Auth: Built-in user authentication simplifies security implementation.
RLS: Powerful row-level security enables fine-grained, data-centric access control crucial for this application.
RPC/Edge Functions: Allows server-side logic (like data aggregation) close to the database.
Generous Free Tier: Suitable for prototype development and small-scale deployment.
Tailwind CSS: A utility-first CSS framework chosen for rapid UI development and easy customization without writing extensive custom CSS.
React Router: Standard library for handling client-side routing in React applications.
Formik & Yup: Industry-standard libraries for simplifying complex form state management and validation in React.
Chart.js & react-chartjs-2: Popular and easy-to-use charting library for visualizing dashboard data.
Rationale Summary: This stack facilitates rapid prototyping while providing a scalable, secure foundation using modern, well-supported web technologies perfectly suited for the project requirements.


4. Installation and Setup Instructions
Prerequisites: Node.js (v18+ recommended), npm/yarn.
Clone Repository: git clone <repository_url>
Navigate to Project: cd <project_directory>
Install Dependencies: npm install (or yarn install)
Supabase Setup:
Create a free project on Supabase.io.
Navigate to "SQL Editor" -> "Queries" -> "+ New query".
Run the SQL scripts provided in the repository (schema.sql, rpc_functions.sql, seed.sql - if provided) to set up the database tables, roles, RPC functions, and initial seed data (like roles).
Alternatively, manually create tables and functions based on definitions if scripts aren't separate.


Environment Variables:
Create a .env file in the project root.
Copy the contents of .env.example (if provided) or add the following:
VITE_SUPABASE_URL=YOUR_SUPABASE_PROJECT_URL
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_PUBLIC_KEY
Replace the placeholder values with your actual Supabase Project URL and Anon Key (found in Project Settings -> API).
Ensure .env is added to your .gitignore file.
Run Development Server: npm run dev (or yarn dev)
Access Application: Open your browser to http://localhost:5173 (or the port specified by Vite).
Test Logins: Use the test credentials provided (e.g., teacher_test@example.com, field_officer_test@example.com) or sign up new users (if signup is configured).


6. Future Development Roadmap
To evolve this prototype into a production-ready application, the following steps are recommended:

Complete Dashboard Features: Implement all planned role-specific widgets, charts (including trends), and necessary RPC aggregation functions.
Refine RLS & Security: Conduct a thorough security audit of all RLS policies and RPC functions. Implement stricter checks where necessary. Use database roles for RPC permissions.
Full Issue Tracking Lifecycle: Implement notifications for new issues/updates, allow assigning issues, and potentially add commenting features. Ensure update/status changes are atomic (use RPC).
Guardian Management UI: Improve the UI for adding/editing/viewing guardian details, possibly integrating it more closely with the Child Detail view (e.g., modal).
File Storage: Implement file uploads/downloads for birth records and potentially other documents using Supabase Storage, associating files with relevant child records.
User Management UI: Develop screens for Admins/Super Admins to invite, create, edit, and disable user accounts and manage role assignments directly within the application.
Advanced Smart Data Collection: Implement logic to compare current form data with previous assessments to highlight changes or skip redundant questions.
Offline Capabilities: Investigate solutions like PWA capabilities or libraries (e.g., RxDB with Supabase replication) to allow field officers limited functionality offline with subsequent synchronization.
Testing: Implement comprehensive unit, integration, and end-to-end tests. Conduct thorough User Acceptance Testing (UAT) with actual teachers and field officers.
UI/UX Polish: Refine the user interface based on user feedback, improve responsiveness, and add better user feedback mechanisms (e.g., loading spinners, toast notifications).
Data Migration Strategy: Develop and test scripts or a process to migrate existing data from Google Sheets/JotForm into the new Supabase database structure.
Deployment & Monitoring: Configure production deployment (e.g., Vercel/Netlify for frontend, Supabase handles backend), set up logging, monitoring, and database backup strategies.
