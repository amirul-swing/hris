# Swing HRIS - Attendance (mockup)

Clickable prototype of the Attendance module for the Swing HRIS. It covers time off only: paid leave, sick leave, special leave, maternity leave, unpaid leave and public holidays. It does not do clock-in or clock-out.

Open `index.html` in a browser. No build step and no backend. Data is kept in the browser's `localStorage`. Use **Account > Reset demo data** to start over.

## Access levels and reporting line

Every person has an access level and a **Reports to** (their leader).

| Access | Can do |
| --- | --- |
| Reportee | Request leave, see own balance and history |
| Leader | Everything a reportee can do, plus approve or reject leave for their **direct reports** and see a team view and team calendar |
| HR admin | Everything above, plus approve or reject **any** request, create and edit accounts, edit the reporting line, quotas and holidays |

Rules:
- Only a person's own leader, or an HR admin, can approve their leave. A leader cannot approve someone outside their direct reports.
- Nobody can approve their own leave. A leader's leave goes to their own leader. People at the top of the line go to People Ops.
- If a leader is deactivated, their reportees' requests go to People Ops until they get a new leader.
- Only leaders and HR admins can be picked as someone's leader. The reporting-line editor never offers a choice that would create a loop.
- A leader with direct reports cannot be changed to Reportee until their reports move.

## Demo accounts

| Who | Access | User ID | Password |
| --- | --- | --- | --- |
| Nadia Kartika | HR admin | `SW-ID-0001` | `swing-admin` |
| Budi Santoso (COO, top of the line) | Leader | `SW-ID-0007` | `swing2026` |
| Fajar Nugroho (Head of Ops ID) | Leader | `SW-ID-0008` | `swing2026` |
| Aiman Hakim (Country Manager MY) | Leader | `SW-MY-0003` | `swing2026` |
| Dimas Pratama (Tech Lead) | Leader | `SW-ID-0004` | `swing2026` |
| Rina Puspita | Reportee of Fajar | `SW-ID-0002` | `swing2026` |
| Tan Mei Ling | Reportee of Aiman | `SW-MY-0005` | `swing2026` |

## Screens

**My leave (everyone)**: overview with balances, request leave (working days only, half days, medical certificate rule for sick leave of 2+ days, overlap check, shows who will approve), my requests with who decided, public holidays, account.

**My team (leaders)**: team approvals for direct reports, team members (who is in or off today, balances, next time off), team calendar.

**People Ops (HR admin)**:
- Dashboard
- All approvals: approve or reject on behalf of any leader.
- Employees & access: create an account (generates a user ID `SW-<country>-<seq>` and a one-time temporary password), edit access level and leader, reset password, deactivate.
- Reporting line: org tree with a "Reports to" picker per person.
- Leave calendar, leave policy (quotas per country), public holidays.

Email sign-in is not connected yet. The admin shares the user ID and temporary password directly, and the employee sets their own password on first sign-in.

## Not production

- Passwords are stored in plain text in `localStorage`. A real build must hash them server-side (e.g. bcrypt) and issue sessions.
- Approval rights are checked in the browser only. A real build must enforce them on the server.
- The 2026 holiday lists are sample data. Verify against the official SKB (Indonesia) and the federal gazette (Malaysia). Malaysian state holidays are not included.
- Quotas are not prorated by join date and do not carry over.
