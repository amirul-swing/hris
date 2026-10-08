# Swing HRIS - Attendance (mockup)

Clickable prototype of the Attendance module for the Swing HRIS. It covers time off only: paid leave, sick leave, special leave, maternity leave, unpaid leave and public holidays. It does not do clock-in or clock-out.

Open `index.html` in a browser. No build step and no backend. Data is kept in the browser's `localStorage`. Use **Account > Reset demo data** to start over.

## Demo accounts

| Role | User ID | Password |
| --- | --- | --- |
| HR admin | `SW-ID-0001` | `swing-admin` |
| Employee (ID) | `SW-ID-0002` | `swing2026` |
| Employee (MY) | `SW-MY-0003` | `swing2026` |

## Employee side

- **Overview**: balance per leave type (available, used, pending), upcoming time off, next public holidays for the employee's country.
- **Request leave**: counts working days only and skips weekends and the country's public holidays. Supports half days, a live balance-after summary, and an attachment rule (sick leave of 2+ days needs a medical certificate). Also checks for overlapping requests.
- **My requests**: history with status filter. Pending or future approved requests can be cancelled.
- **Public holidays**, **Account** (change password).

## Admin side (People Ops)

- **Overview**: pending approvals, who is off today, off in the next 7 days, active accounts.
- **Approvals**: approve, or reject with a reason the employee sees. Shows the balance after approval and flags a missing medical certificate.
- **Employees & access**: create an account, which generates a user ID (`SW-<country>-<seq>`) and a one-time temporary password. Also reset passwords and deactivate or reactivate accounts. Email sign-in is not connected yet, so the admin shares the credentials directly. The employee must set their own password on first sign-in.
- **Leave calendar**: month view of approved and pending leave plus holidays, filterable by country.
- **Leave policy**: yearly quotas per country (ID / MY).
- **Public holidays**: add or remove holidays per country.

## Not production

- Passwords are stored in plain text in `localStorage`. A real build must hash them server-side (e.g. bcrypt) and issue sessions.
- The 2026 holiday lists are sample data. Verify against the official SKB (Indonesia) and the federal gazette (Malaysia). Malaysian state holidays are not included.
- Quotas are not prorated by join date and do not carry over.
