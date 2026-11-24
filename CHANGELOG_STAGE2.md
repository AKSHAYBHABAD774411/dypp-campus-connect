# Stage 2 development update

## Added
- Authenticated role-aware academic API routes.
- Parent-to-student account linking and parent-scoped attendance, marks and timetable reads.
- Attendance session and per-student attendance-entry tables, with aggregate percentage updates.
- Faculty/HOD/Admin attendance marking interface.
- Assignment creation, student submission URL workflow and evaluation status endpoint.
- Class-test mark entry and published student/parent result retrieval.
- Role-aware timetable reads and HOD/Admin timetable creation/update endpoints.
- Study material library endpoints and faculty/HOD/Admin publish interface.
- Student/faculty leave request submission and HOD/Admin review endpoints.
- Audience-based announcements and student roster access scoped to department for teaching roles.
- Connected module views for attendance, timetable, assignments, study materials, marks, leave and announcements.
- Stage 2 migration script for existing Stage 1 databases.

## Still required before production
- Secure file upload service, malware scanning and storage retention policy.
- Complete CRUD screens for all administrative modules and approval actions.
- Institutional student/faculty import and subject/faculty allocation workflows.
- Stronger audit logging, account recovery, MFA, backups and penetration testing.
- Configure and validate the institution-approved AI provider.
- Real-device QA, accessibility review and college sign-off.

## Stage 3 – Institutional administration and reporting
- Added Admin-only account directory, account activation/deactivation, and account creation through the portal UI.
- Added department-scoped faculty directory for HOD and institution-wide directory for Admin.
- Added attendance and marks report APIs with department and semester filters, plus client-side CSV export.
- Added leave approval/rejection actions in the Leave Approvals module.
- Added lesson-plan create/list/update workflows with Planned, Completed, and Deferred states.
- Added submission review list endpoint and department-scoped report access.
- Tightened marks entry and timetable update checks to prevent cross-department edits.
- Added responsive action controls and CSV export styling.

Stage 3 still requires database/runtime verification against the institution's MySQL instance. CSV export is generated in the browser. No live SMS/email gateway, cloud file storage, or AI provider has been configured.
