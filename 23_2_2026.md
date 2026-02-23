# Role Permission  

---

# 1️⃣ CENTER MANAGEMENT MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Center  
- Document Gallery  

## 🔹 Roles & Permissions

| Role                | Permission                                                                 | Status |
|---------------------|---------------------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Center, Document Gallery)     | Done   |
| Manager             | View only (Center-wise)                                                  | Done   |

---

# 2️⃣ CLASS MANAGEMENT MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Class  
- Document Gallery  

## 🔹 Roles & Permissions

| Role                | Permission                                                                 | Status |
|---------------------|---------------------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Class, Document Gallery)      | Done   |
| Manager             | View only (Center-wise)                                                  | Done   |

---

# 3️⃣ FEES MANAGEMENT MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Fees  

## 🔹 Roles

| Role                | Permission                                                   | Status |
|---------------------|-------------------------------------------------------------|--------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Fees)            | Done   |

---

# 4️⃣ CHILD MASTER MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Child  

---

## 🔹 STATUS FLOW (Very Important)

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

---

## 🔹 Status Permissions

| Status      | Admin & Superadmin | Manager |
|------------|--------------------|----------|
| Create     | Full access        | Full access |
| Review     | Approve / Reject   | Edit |
| Withdrawal | Approve (if approved by Admin & Superadmin, status becomes Withdrawal) | Initiate |
| Archive    | View               | View |

> Notification sent to Admin & Superadmin and Manager on create, approve, and withdrawal actions.

---

# 5️⃣ WAITING LIST MODULE 

## 🔹 Features (Per Center)

- Create, View, Update, Delete Waiting List Entries  

## 🔹 Roles

| Role                | Permission                                                                    |
|---------------------|-------------------------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Waiting List Entries)             |

---

# 6️⃣ FEES REPORTS MODULE

## 🔹 Features (Per Center)

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

## 🔹 Roles

| Role                         | Permission |
|------------------------------|------------|
| Superadmin                   | Full       |
| Admin & Manager (List, Create) | Child / Parent / Class / Fee Plan / Manager / Notes |

---

# 7️⃣ EMPLOYEE REPORTS MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Employee  

## 🔹 Roles & Permissions

| Role                | Permission                                                   |
|---------------------|-------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Employee)        |
| Manager             | View only (Center-wise)                                    |

## 🔹 Employee Status

- Default: **Active**  
- If resign date is added → Status = **Resigned**  
- On last working date → Status = **Archive**  

---

# 8️⃣ EMPLOYEE WAITING LIST MODULE

## 🔹 Features (Per Center)

- Create, View, Update, Delete Employee Waiting  

## 🔹 Roles & Permissions

| Role                | Permission                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Admin & Superadmin  | Full access (Create, View, Update, Delete Employee Waiting)               |
| Superadmin          | Move Employee from Waiting List to Employee List (redirect to Edit page)  |
| Manager             | View only (Center-wise)                                                    |

---

# 9️⃣ WAGE REPORT MODULE

## 🔹 Features

1. Monthly Employee Report (Admin)  
2. List Report  

| Role        | Permission |
|------------|------------|
| Superadmin | Full       |

> Employee status must be validated before generating wage reports.

---

# GENERAL SYSTEM RULES

- All delete operations must be **Soft Delete**  
- Audit log must track:
  - Who created  
  - Who updated  
  - Created date & time  
  - Updated date & time  

## 🔹 Security

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

# ACCOUNTING (ACCB) MODULE

- Export PDF data to CSV.  
- Directly upload into each report.  
- Automatic counting functionality is required.  

---

# CLASS MANAGEMENT

Gallery must have two sections:

- Minor Section  
- Major Section  

---

# DASHBOARD

- Show pending tasks and reports  
- Show attendance summary  
- Show fee-pending child master alerts and notifications  
- Show activity timeline  

---

## 🔹 Timeline & Task Management

- Each Admin in the center is assigned tasks with a specific date or time.  
- All assigned tasks are visible in the timeline view.  
- Tasks can be created per user.  
- Newly joined employees remain under probation for 3 months.  
- Probation status is tracked in the system until completion.  

## 🔹 Notifications

- On probation date (via employee email)  
- On child creation  
- On child approval  
- On child withdrawal  
