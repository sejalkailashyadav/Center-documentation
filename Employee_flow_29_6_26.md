# Employee Module Flow (Role Wise)

## 1. Employee

* Can self-register using the public registration link.
* After registration, status becomes **Registered / Review**.
* Can log in and update their own profile and documents.
* Updates do not directly modify the employee record.
* Every change creates an **Employee Update Request** for approval.

---

## 2. Manager / Regional Manager

Managers and Regional Managers follow the same workflow.

They can:

* View employees within their assigned center(s).
* Verify newly registered employees.
* Approve or reject employee update requests.
* Resign employees.

### Access Scope

* **Manager:** Assigned center(s) only.
* **Regional Manager:** Multiple assigned centers.

---

## 3. Admin / Superadmin

Admin and Superadmin have full system access.

They can:

* View all employees.
* Add employees.
* Edit employees.
* Verify registrations.
* Approve or reject update requests.
* Resign employees.
* Delete employees.
* Filter employees by status, center, and location.
* Receive the automated 15-day Employee Summary Report.

They have complete visibility across all locations.

---

# Registration Flow

1. Employee submits the registration form.
2. Employee status becomes **Registered / Review**.
3. Manager or Regional Manager verifies the registration.
4. Employee status changes to **Active**.

---

# Update Flow

1. Employee updates profile information or documents.
2. Existing approved data remains unchanged.
3. Updated information is stored in the `employee_update_requests` table.
4. Employee status becomes **Update Requested**.

---

# Update Approval

1. Manager or Regional Manager reviews the pending update request.
2. If approved:

   * Requested data replaces the existing employee data.
   * Employee status changes back to **Active**.

---

# Update Rejection

1. Manager or Regional Manager rejects the update request with remarks.
2. Existing employee data remains unchanged.
3. Employee status becomes **Update Rejected**.
4. Employee can review the remarks and submit a new update request.

---

# Resignation Flow

* Employees cannot resign themselves.
* Manager, Regional Manager, Admin, or Superadmin records:

  * Notice Date
  * Last Working Date
  * Remarks
* Employee status becomes **Resign Approved**.
* Employee remains in the system until the Last Working Date.

---

# Archive Flow

A daily cron job checks employees whose status is **Resign Approved**.

If the **Last Working Date** is today or earlier:

* Employee status changes to **Archive**.
* Archived employees are excluded from active employee records.

---

# Delete Flow

Manager, Regional Manager, Admin, and Superadmin can soft delete duplicate, test, or invalid employee records.

* Employee status becomes **Deleted**.
* `deleted_at` is populated.
* Deleted records remain in the database.
* Deleted employees are hidden from normal listings and can be viewed using the **Deleted** filter.

---

# 15-Day Summary Report

Every 15 days, a scheduled cron job sends a summary email to **Admin** and **Superadmin**.

The report includes:

* New employee registrations
* Employee count by location
* Missing employee documents
* Missing child documents (Current Child Master)
* Center-wise child count
* Resigned employees
* Archived employees
* Deleted employees
* Pending employee update requests
* Pending employee registrations

---

# Employee Status Codes

| Code | Status              |
| ---- | ------------------- |
| 0    | Registered / Review |
| 1    | Active              |
| 2    | Update Requested    |
| 3    | Update Rejected     |
| 4    | Resign Approved     |
| 5    | Archive             |
| 6    | Deleted             |

---

# Workflow Overview

```text
Employee
    │
    ├── Self Registration
    ▼
Registered / Review (0)
    │
    ▼
Manager / Regional Manager Verification
    │
    ▼
Active (1)
    │
    ├───────────────────────────────┐
    │                               │
    ▼                               ▼
Update Request (2)            Resignation (4)
    │                               │
    ▼                               ▼
Approve / Reject             Last Working Date
    │                               │
    ├──────────────┐                ▼
    │              │          Daily Cron Job
    ▼              ▼                │
Active (1)   Update Rejected (3)    ▼
    ▲                         Archive (5)
    │
Employee Resubmits Update

Delete (Soft Delete)
        │
        ▼
Deleted (6)
```
