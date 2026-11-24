# Stage 4 – Notifications, file services and reliability

- Added authenticated multipart file uploads with a 10 MB limit and PDF/DOC/DOCX/JPG/PNG allowlist.
- Files use random server-generated names, metadata is stored in MySQL, and downloads require a valid bearer token.
- Added per-user in-app notification endpoints: list, unread count, mark one read and mark all read.
- Announcements fan out notifications to the selected audience; new assignments notify active students in the creator's department; leave decisions notify the requester.
- Added `database/migrate_stage4.sql` and matching fresh-install schema definitions.
- Added upload error responses and documented persistent private storage configuration.

## Remaining before production

- Dedicated notification-center and file-picker UI integration.
- Malware scanning and content-signature validation.
- Managed private object storage, HTTPS, production CORS allowlist, backups and retention policy.
- End-to-end testing against the institution's actual MySQL deployment.
