# Tsshegofatso & Friends — Accounting platform sample

A responsive, dependency-free accounting and compliance website made for GitHub Pages. Uses HTML, CSS and JavaScript. No Node.js, npm or build step is required.

## Included

- Public home, nine-service catalogue, example pricing, FAQs, contact, privacy and terms pages.
- Client sample dashboard with company creation, service requests and status filtering.
- Local appointment scheduling with weekday validation, slot conflict checks and cancellation.
- Local file attachments with download and removal, local messages and planning reminders.
- Sample invoices and printing, admin status/assignment workflow, Excel (.xlsx) data export and local data reset.
- Mobile layouts, keyboard accessible controls, hash navigation compatible with GitHub project subpaths.
- GitHub Actions deployment workflow.

## Publish on GitHub — easiest option

1. Download and extract the ZIP.
2. Create a new public GitHub repository, for example `accounting-platform`.
3. Upload the **contents** of the extracted `accounting-platform` folder. `index.html` must be at the repository root, next to `assets`, not inside another folder.
4. Commit the files to `main`.
5. In the repository, open **Settings → Pages**.
6. Choose **Deploy from a branch**, then **main** and **/(root)**, and Save.
7. GitHub displays the published URL on the Pages settings screen after deployment. It generally has the form `https://YOUR-USERNAME.github.io/accounting-platform/`.

If uploading through GitHub's website, hidden `.github` files might not be selected. The branch deployment option works without them. With Git, all provided files are included.

## Alternative: GitHub Actions

Upload the entire project including `.github/workflows/pages.yml`. In **Settings → Pages → Source**, choose **GitHub Actions**. Push to `main` or run **Deploy GitHub Pages** manually from Actions. Do not use both deployment options at once.

## Run locally in VS Code

Open the extracted folder in VS Code. Use the Live Server extension, or run `python -m http.server 8000` in the terminal and open `http://localhost:8000`. Opening `index.html` directly may work, but local-storage behaviour under `file://` can vary by browser.

## Edit your brand

- `index.html`: page title, description, header brand, footer.
- `assets/app.js`: all page copy, service catalogue and illustrative prices; search for `Tsshegofatso & Friends` to replace the sample name.
- `assets/styles.css`: colours, spacing, layout and typography.
- `assets/favicon.svg`: favicon.
- Replace the placeholder contact page with your verified business email, phone and address.
- Google Fonts is optional. Remove the CSS `@import` to rely on system font fallbacks.

## What this release is

This is a static, interactive prototype, not the complete production system in the supplied technical specification. Sample records are stored in the current browser only. No information is shared between visitors, devices or accountants. Account credentials determine the client or admin workspace. Client routes block admin access and only admin views expose status and assignment updates. The presentation login is stored in the browser session and requires backend authentication for production. Use sample data and files in this version.

There is no real login, registration, email verification, shared server uploads, payment gateway, tax filing, government integration or server-side audit trail. The booking form does not notify anyone. Document details use local storage; file bytes use IndexedDB in the same browser. Prices, invoices and initial records are illustrative. Compliance planning dates are entered by the sample user, not calculated legal deadlines. Local time slots are 30-minute consultations with hourly starts.

GitHub Pages cannot run the Spring Boot/MySQL backend from the specification. For live client operations, keep this frontend on Pages and deploy a backend separately. Implement authenticated client/staff APIs, ownership checks, database persistence, private object storage, audited workflows, notifications and payment webhooks. Replace browser-local functions with those APIs, configure HTTPS and CORS for your Pages domain, and keep secrets exclusively on the server. Publish firm-specific privacy/terms and confirmed pricing before accepting clients.

## Files

```
index.html
assets/app.js
assets/excel-export.js
assets/document-files.js
assets/styles.css
assets/favicon.svg
.github/workflows/pages.yml
.nojekyll
README.md
```

No external images, npm dependencies or backend credentials are included. The application uses hash-based routes, so refreshing a portal page works on GitHub Pages without rewrite rules.

## Excel export

Click **Export to Excel** in any portal view to download `tsshegofatso-friends-data.xlsx`. It includes Companies, Requests, Appointments, Documents, Invoices, Messages and Compliance worksheets. Empty sections retain their column headers. Headers are styled, filterable and frozen; invoice amounts are numeric ZAR values. Phone and registration numbers stay as text. Only records in this browser are exported. The exporter is bundled locally and works without an external spreadsheet service.

## Local document files

Documents now accepts PDF, JPG, PNG, Word, Excel, CSV and text files up to 10 MB each. Choose a company, a request belonging to that company, a category and a file, then select **Save file locally**. Saved documents have Download and Remove buttons. The app stores actual file bytes in IndexedDB on the same browser and website origin; it does not send them to staff. Clear local sample data also deletes attached files. Old filename-only records remain labelled Record only. Excel exports document details, sizes and file types, not file contents. Storage may be unavailable or full; the form reports save failures. Changing the website origin or browser gives a separate store.

## Client and admin roles

Select **Log in** in the header and use the client or admin presentation credentials listed below. Clients can create requests and view progress. Admins can manage statuses and assign accountants through Manage buttons. Direct admin links are blocked while using the client role. Use **Log out** in the sidebar, then sign into the other presentation account. The admin can review the local dataset; the client view filters records by ownership. Real user authentication, record ownership and authorisation must be enforced on a backend before real client use.

## Presentation login credentials

The role picker has been replaced by an email/password sample login. Select **Log in** in the header.

| Role | Email | Password |
| --- | --- | --- |
| Client | client@tsshegofatso.example | Client123! |
| Admin | admin@tsshegofatso.example | Admin123! |

Correct credentials open the corresponding dashboard. Incorrect credentials show an error. Use **Log out** in the sidebar before signing into the other account. The session stays in the current tab across refreshes. Passwords are not stored in browser session storage, but these fixed sample credentials are public in the app source and in the presenter guide. This is not secure authentication. The admin reviews client records in the same browser; clients see only records owned by the presentation client. Production accounts require a backend.

## Updated client and admin workflows

Contact: +27 67 237 8646, with telephone and WhatsApp enquiry links. Login credentials are listed in this README, not displayed in the login interface. Admins can manage appointment dates, times and statuses, with slot collision checks. Request management includes internal notes, client-visible updates, document requests and local history. Internal notes are not shown in client request details, but they are not protected against inspecting browser storage. Prices clarify example scope and separately quoted government fees. All changes remain local, with no email or shared backend connection.

## Login required for actions

Visitors may browse the home, services, pricing, contact and policy pages. Booking, portal pages, records, files, messaging, Excel export and local reset require a presentation login. Opening a booking link while signed out shows the login form; after successful login the app returns to the requested booking and preserves the selected service. Client accounts cannot access admin routes. These are browser-side presentation controls, not production authentication.

## Role visibility and permissions

| Area | Client account | Admin account |
| --- | --- | --- |
| Dashboard and Excel export | Own records only | All local client records |
| Companies | View and add own companies | Review client companies |
| Requests | Create and track own requests | Review, assign accountants, change status, request documents and post updates |
| Internal request notes | Hidden from details and exports | View and add |
| Documents | Upload, download and remove own files | Review requested documents and download client files |
| Appointments | Book and cancel own active appointments | Review, approve, reschedule, complete or cancel appointments |
| Invoices | View and print own invoices | Review and print client invoices |
| Messages and compliance | Create and view own messages and reminders | Review client messages and reminders |
| Clear all local data | Unavailable | Available on Privacy page |

Opening the other role's routes is blocked. Document, request, invoice and cancellation handlers check record access, including manually supplied record IDs. Navigating or logging out closes open dialogs. Client exports exclude other owners and internal notes. Existing unowned version-one records are assigned to the original presentation client during migration; explicitly owned records retain their owners. New client records have an owner ID.

These checks separate presentation workflows in the interface. The source, fixed passwords and browser storage remain inspectable. For the backend, derive user identity from a verified session and enforce ownership and role permissions on every API, file download and export. Never trust a role or owner ID sent by this frontend.
