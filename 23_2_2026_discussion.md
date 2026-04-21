# Role Permission  

---

# 1️⃣ CENTER MANAGEMENT MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Center  
- Document Gallery  

##  ✔  Roles & Permissions

| Role                | Permission                                                                 | Status |
|---------------------|---------------------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Center, Document Gallery)     | Done   |
| Manager             | View only (Center-wise)                                                  | Done   |

---

# 2️⃣ CLASS MANAGEMENT MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Class  
- Document Gallery  

##  ✔  Roles & Permissions

| Role                | Permission                                                                 | Status |
|---------------------|---------------------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Class, Document Gallery)      | Done   |
| Manager             | View only (Center-wise)                                                  | Done   |

---

# 3️⃣ FEES MANAGEMENT MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Fees  

##  ✔  Roles

| Role                | Permission                                                   | Status |
|---------------------|-------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Fees)            | Done   |

---

# 4️⃣ CHILD MASTER MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Child  

---

##  ✔  STATUS FLOW (Very Important)

### 🟡 1. Review (Default)

- When a Manager creates a student  
- Status = **Review**  
- Admin approval pending  
- Both Admin & Superadmin can accept the entry  

### 🟢 2. Active

- Admin or Manager accepts the entry  
- Student is under an active program  

### 🟠 3. Withdrawal

- Manager enters:
  - Withdrawal date  
  - Notes  
- Status becomes **Withdrawal**  
- Awaiting withdrawal confirmation  

### 🔴 4. Archive

- When the withdrawal date has passed  
- Automatically, the next day status = **Archive**  
- No longer active in the system  

### Show Child 
- show created date and created by in show page of child 
---

##  ✔  Status Permissions

# CHILD STATUS WORKFLOW

##  ✔  Task Flow

| Task            | Access                               | Status                     | Notifications |
|-----------------|--------------------------------------|----------------------------|--------------|
| Create Child    | Admin, Superadmin, Manager           | Review (Default)           | On create, notification sent to Admin, Superadmin, and Manager |
| Approve Child   | Admin, Superadmin                    | Active                     | Child becomes Active. Notification sent to Admin, Superadmin, and Manager |
| Withdraw Child  | Admin, Superadmin                    | Withdrawal                 | Child becomes Withdrawal. Notification sent to Admin, Superadmin, and Manager |
| Archive         | Automatic (Cron Job)                 | Archive                    | Automatically archived when the withdrawal date is reached (checked on the first day of each month) |

---

##  ✔  Important Notes

- If a **Manager** performs Approve or Withdrawal, the status will **not change immediately**.  
- A notification will be sent to Admin and Superadmin.  
- The status will change only after Admin or Superadmin approval.  

### Status Change Rules

- Review → Active:  
  If Manager approves, status remains **Review** until Admin approves. After Admin approval, status becomes **Active**.  

- Active → Withdrawal:  
  If Manager initiates withdrawal, status remains **Active** until Admin approves. After Admin approval, status becomes **Withdrawal**.  

---

# DATABASE REQUIREMENTS

A separate entry (status history table) is required in the database to track all status changes.

##  ✔  Audit Log Requirements

The system must track:

- Who created the record  
- Who updated the record  
- Created date & time  
- Updated date & time  

---

# CHILD MASTER TABLE REQUIREMENTS

In addition to the status history table, the **Child Master** table must include:

- `created_at`  
- `updated_at`  
- `created_by`  
- `updated_by`  

These fields are mandatory for proper tracking and auditing.

# 5️⃣ WAITING LIST MODULE 

##  ✔  Features (Per Center)

- Create, View, Update, Delete Waiting List Entries  

##  ✔  Roles

| Role                | Permission                                                                    |
|---------------------|-------------------------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Waiting List Entries)             |

---

# 6️⃣ FEES REPORTS MODULE

##  ✔  Features (Per Center)

### 1️⃣ Create Report

### 2️⃣ Fresh Reports

- Select date range  
- Select center/class  
- Generate report  

### 3️⃣ Copy Report

- Duplicate an existing report  
- Modify parameters  

### 4️⃣ Merge Reports

- Combine multiple fee reports into one  

### 5️⃣ Admin Fee Reports

- Visible only to Admin  
- Full financial overview  

### 6️⃣ List Fee Reports

- View all saved reports  
- Filter by date / center  

##  ✔  Roles

| Role                         | Permission |
|------------------------------|------------|
| Superadmin                   | Full       |
| Admin & Manager (List, Create) | Child / Parent / Class / Fee Plan / Manager / Notes |

---

# 7️⃣ EMPLOYEE REPORTS MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Employee  

##  ✔  Roles & Permissions

| Role                | Permission                                                   |
|---------------------|-------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Employee)        |
| Manager             | View only (Center-wise)                                    |

##  ✔  Employee Status

- Default: **Active**  
- If resign date is added → Status = **Resigned**  
- On last working date → Status = **Archive**  

---

# 8️⃣ EMPLOYEE WAITING LIST MODULE

##  ✔  Features (Per Center)

- Create, View, Update, Delete Employee Waiting  

##  ✔  Roles & Permissions

| Role                | Permission                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Employee Waiting)               |
| Superadmin          | Move Employee from Waiting List to Employee List (redirect to Edit page)  |
| Manager             | View only (Center-wise)                                                    |

---

# 9️⃣ WAGE REPORT MODULE

##  ✔  Features

1. Monthly Employee Report (Admin)  
2. List Report  

| Role        | Permission |
|------------|------------|
| Superadmin | Full       |

> Employee status must be validated before generating wage reports.

---



##  ✔  Security

Documents must be moved from: Public > Storage 

---

# BUG

- Check Create Child UI dropdown  

---

# REPORT MODULE

- Reports must be role-based and include a “Created By” field.  
- Reports can be archived.  
- Archived reports must be stored separately.  

---

# CLASS MANAGEMENT

Gallery must have two sections:

- Minor incidence  
- Major incidence  

---

# DASHBOARD

- Show pending tasks and reports  
- Show attendance summary  
- Show fee-pending child master alerts and notifications  
- Show activity timeline  

---

### Timeline & Task Management

* The Super Admin can create and assign tasks to any system user.
* Each task includes a date, time, assigned user, and last updated time.
* Users can mark tasks as completed or pending and add notes.
* The Super Admin can add, edit, and delete tasks.
* Managers can view tasks and update their status (overdue, pending, completed).
* Recurring tasks are automatically generated based on a schedule.
* All tasks are displayed in a timeline view, and notes are shown in a thread view.
* The admin receives an email notification one day before a task’s due date.
* Manager-wise email addresses can be added to specify managers for a particular center.

---

### Notification Section

Child Notifications

* Approval workflow includes:

  * Create child request
  * Approval
  * Approve request
  * Withdrawal
  * Withdrawal request
  * Delete
  * Delete request

---

### Summary of Employee Master (Sent on the 1st of Every Month)

1. New Joiners (Last Month)
2. Completed Probation (Last Month)
3. Last Day of Working (Last Month)
4. Expired Documents (Last Month)
5. Upcoming Completed Probation (Upcoming Month)
6. Upcoming Expiring Documents (Upcoming Month)

---

### Dashboard

* New Joiners (Monthly Summary)
* Completed Probation (Monthly Summary)
* Last Day of Working
* Expired Documents
* Upcoming Completed Probation
* Upcoming Expiring Documents
* Displayed on the dashboard along with quick links

---

### Child Master Changes

* The child list should support search functionality for both parent and child names.
* Search should also be possible based on status, with proper filtering options.

---

### Report Changes

* In the Merge Report section, we need the same Excel format as used in the Fee Report.
* Cross-check report status categories:

  * Existing
  * New
  * Withdrawals
    (These should match the Fee Report list and apply during report creation.)
* A folder-wise or tagging section is required to group and segregate reports month-wise.

---
# ACCOUNTING (ACCB) MODULE

- Export PDF data to CSV.  
- Directly upload into each report.  
- Automatic counting functionality is required.  

---

# Center 

* Add delete options in edit doc section 

# GENERAL SYSTEM RULES

- All delete operations must be **Soft Delete**  
- Audit log must track:
  - Who created  
  - Who updated  
  - Created date & time  
  - Updated date & time  

# UI Changes 

# User Management

* Add one user as a **Regional Manager** who has access to different centers under a single login.
* This user should have only manager-level access.
* The Regional Manager should be able to manage multiple locations (centers).
* Start with Melissa’s setup first.
