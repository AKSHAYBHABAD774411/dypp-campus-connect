# DYPP Campus Connect

A responsive full-stack starter portal for D. Y. Patil Polytechnic, Ambi, Pune.

## Stack
- Frontend: React + Vite
- Backend: Node.js + Express
- Database: MySQL (`mysql2`)
- Authentication: JWT + bcrypt
- UI: responsive dark futuristic dashboard

## Requirements
- Node.js 20+
- MySQL 8+

## Setup

### 1. Database
Create a database and user in MySQL, then import `database/schema.sql` for a fresh installation. If you already installed Stage 1, back up the database and run `database/migrate_stage2.sql` exactly once instead.

```sql
CREATE DATABASE dypp_campus;
```

### 2. Backend
```bash
cd server
cp .env.example .env
# Update DB credentials and JWT_SECRET
npm install
npm run seed
npm run dev
```

API runs at http://localhost:5000.

Demo accounts (password for all: `Demo@123`)
- admin@dypp.edu.in
- hod@dypp.edu.in
- faculty@dypp.edu.in
- student@dypp.edu.in
- parent@dypp.edu.in

### 3. Frontend
In a second terminal:
```bash
cd client
npm install
npm run dev
```
Open http://localhost:5173.

## Stage 2 connected workflows
The following authenticated API workflows are now included:
- `GET /api/dashboard/summary` – role-aware dashboard counts
- `GET /api/attendance/me` – own or linked student's subject attendance
- `POST /api/attendance/mark` – faculty/HOD/admin attendance session with per-student entries
- `GET /api/attendance/class` and `GET /api/users/students` – department-scoped class roster
- `GET/POST /api/assignments` and `POST /api/assignments/:id/submit`
- `PATCH /api/submissions/:id/evaluate` – faculty evaluation status
- `GET/POST /api/marks` – published marks and authorized mark entry
- `GET /api/timetable` and `POST/PATCH /api/timetable` – role-aware timetable retrieval and HOD/Admin scheduling
- `GET/POST /api/materials` – study resource library
- `GET/POST /api/subjects` – subject catalogue
- `GET/POST /api/leave` and `PATCH /api/leave/:id` – leave requests and approvals
- `GET/POST /api/announcements` – audience-based notices
- Parent accounts are linked to a student using `users.linked_student_id`.

The client now loads connected attendance, timetable, assignments, marks, leave, announcement, study-resource and roster records when signed in. Faculty/HOD/Admin users can create assignments, mark attendance, enter class-test marks and publish notices from the relevant module screens. Student/faculty users can submit leave requests.

## Included modules
- Role-based login: Student, Faculty, HOD, Admin, Parent
- Role-aware dashboard and navigation
- Attendance, timetable, assignments, study materials, class tests/results
- Lesson planning, syllabus tracking, department reports
- Announcements, leave requests, parent monitoring
- AI assistant interface (requires a configured server-side AI provider)

## Important production checklist
This is an enhanced development build, not a deployed or institution-approved production system. File submissions currently accept a file URL; a secure upload provider and malware scanning must be configured before accepting student files.
Before real student data is entered:
1. Replace demo accounts and change all secrets.
2. Configure HTTPS, backups, audit logs, rate limiting and institutional access policies.
3. Add verified student/faculty records and import approved academic data.
4. Review privacy, retention and parent-consent procedures.
5. Configure an AI provider on the server. Never put an AI API key in frontend code.
6. Have the college IT team security-test and approve the deployment.

## Stage 2 demo data
After importing the schema and running `npm run seed`, the seed script creates five role accounts, links the parent to the demo student, and inserts sample attendance, timetable, assignment, class-test and announcement records. The demo student is in Computer Engineering, semester 5, division A.

## AI assistant
The `/api/assistant` route provides a safe integration point. Without `AI_API_URL` and `AI_API_KEY`, it returns a helpful demo response. Configure a trusted AI service compatible with the server's expected JSON request before enabling it for users.

## Stage 3 additions
- Admin account directory and account creation / activation controls (`/api/admin/users`, `/api/users`).
- HOD/Admin faculty directory (`/api/department/faculty`).
- Attendance and marks reporting endpoints (`/api/reports/attendance`, `/api/reports/marks`) with browser CSV export.
- Leave approval actions, lesson-plan workflows, and submission review listing.
- Report and user-management access is role-restricted; HOD reports and approvals are department-scoped.

Run `node --check server/src/routes.js` after updating. Stage 3 has not yet been runtime-tested against a live MySQL database. Back up the database before applying schema changes from future stages.


## Stage 4 – Notifications and secure file access

Stage 4 adds authenticated file upload/retrieval and in-app notifications.

1. Install server dependencies: `cd server && npm install` (includes Multer).
2. Run the Stage 4 database migration once: `mysql -u <user> -p <database> < database/migrate_stage4.sql`.
3. Start the API with `npm run dev` and the client with `npm run dev` from `client`.
4. Upload endpoint: `POST /api/files/upload` as multipart form data with field name `file`; allowed types are PDF, DOC, DOCX, JPG and PNG, maximum 10 MB.
5. Retrieve a file using the returned `/api/files/<stored-name>` path with a valid bearer token. Files are not served from a public static directory.
6. Notifications: `GET /api/notifications`, `GET /api/notifications/unread-count`, `PATCH /api/notifications/:id/read`, and `POST /api/notifications/read-all`.

Announcements create notifications for their audience. New assignments notify active students in the creator's department, and leave decisions notify the requester. Uploaded files are stored in `server/uploads` by default; set `UPLOAD_DIR` to a persistent private storage path in deployment.

Production requirements: use HTTPS, private persistent storage or a managed object store, malware scanning, database backups, a production CORS allowlist, verified file signatures, retention rules and monitored logging. The API currently provides the upload/notification services; the current portal screens still need a dedicated notification center and file-picker integration in a subsequent UI pass.
