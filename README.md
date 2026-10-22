# Swing HRIS - Attendance (mockup)

Clickable prototype of the Attendance module for the Swing HRIS: paid leave, sick leave, other leave and public holidays. It does not do clock-in or clock-out.

Open `index.html` in a browser. No build step and no backend. Data is kept in the browser's `localStorage`. Use **Account > Reset demo data** to start over. Importing a spreadsheet needs an internet connection (the reader loads from cdnjs).

The look follows the Swing decks in monochrome: black on white, Swing purple as the only accent. It also has a dark mode.

## Getting started

1. Sign in as HR admin: `admin` / `swing-admin`.
2. Go to **Employees & access > Import master data** and pick the master data `.xlsx`. This creates one account per row, with the username and temporary password from the file.
3. Fill in **Join date** and **Direct report to**, either in the file before importing or inline in the Employees table.
4. Share each person's username and temporary password with them. They set their own password at first sign-in.

The employee roster is **not** stored in this repository, because the repo is public. Keep the master data file private.

### Master data columns

| Column | Notes |
| --- | --- |
| Name | Required |
| FT / PT | `FT` or `PT`. "Employed - Part Time" also reads as PT |
| Entity | `Swing` or `GSA` |
| Join Date | Date, e.g. `2024-06-10`. Drives paid leave |
| Direct Report To | Leader's name. This leader approves their leave |
| Access | `Reportee`, `Leader` or `HR admin` |
| Username | Optional. Generated as `first.last` if empty |
| Temporary Password | Optional. Generated if empty |

Re-importing matches rows by username (then by name) and updates them. Passwords of existing accounts are not touched.

## Leave rules

- **Paid leave**: 1 day is earned for every full month of service from the join date (someone who joined 10 Mar earns on 10 Apr, 10 May, and so on).
- Days earned in a year stay valid that year and the next year, then expire on 31 Dec. The oldest days are used first. Both numbers can be changed in **Leave policy**.
- A paid leave request is blocked if the person does not have enough valid days on the first day of leave.
- **Sick leave**: needs a surat sakit (doctor's note) attached. Does not use the paid balance.
- **Other leave**: the employee must specify what it is for. Does not use the paid balance.
- Days count working days only. Weekends and public holidays are skipped. Half days are possible for single-day requests.

## Access levels and reporting line

| Access | Can do |
| --- | --- |
| Reportee | Request leave, see own balance and history |
| Leader | Also approve or reject leave for their **direct reports**. Has team view and team calendar |
| HR admin | Also approve or reject **any** request. Manages accounts, master data, reporting line, policy and holidays |

- Nobody approves their own leave.
- Anyone without a leader goes to People Ops.
- Only leaders and HR admins can be picked as a leader. The reporting line editor never offers a choice that would create a loop.

## Not production

- Passwords are stored in plain text in `localStorage`, and temporary passwords are visible to HR admin. A real build must hash them server-side and issue sessions.
- Approval rights are checked in the browser only.
- The 2026 holiday lists are sample data. Verify against the official SKB (Indonesia) and the federal gazette (Malaysia).
