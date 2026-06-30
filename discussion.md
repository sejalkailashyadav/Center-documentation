# Role Permission  

---
#### **Super Admin**

* Has full access to all modules and features.

#### **Admin**

* Has full access except for:

  * Wage Access
  * User Access
  * Report Copy
  * Merge
  * Repo Access

#### **Admin Fee**

* Has the same access as Admin.
* Additionally, has access to the **“Admin Fee Report Section.”**

#### **Regional Manager**

* Has the same access as Manager.
* Only the Super Admin can assign or add multiple managers.

#### **Manager**

* Has limited access restricted to their assigned centers only.

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

# Dashboard

* New Joiners (Monthly Summary)
* Completed Probation (Monthly Summary) 
* Last Day of Working
* Expired Documents
* Upcoming Completed Probation
* Upcoming Expiring Documents
* Displayed on the dashboard along with quick links

---

# User Management

* Add one user as a **Regional Manager** who has access to different centers under a single login.
* This user should have only manager-level access.
* The Regional Manager should be able to manage multiple locations (centers).
* Start with Melissa’s setup first.

---

# Report 

* In the Merge Report section, we need the same Excel format as used in the Fee Report.
* Cross-check report status categories:

  * Existing
  * New
  * Withdrawals
    (These should match the Fee Report list and apply during report creation.)
* A folder-wise or tagging section is required to group and segregate reports month-wise.
      User  can create folders inside folders and organize reports by year and month..
      we can move reports by adding a Finalize button on each report row.

---

#  Task Managment 

<img width="475" height="845" alt="image" src="https://github.com/user-attachments/assets/c07eaefd-55a7-44c4-987d-aa96d7142daa" />
"Why I don’t see Pooja”s user name here?"

<img width="475" height="845" alt="image" src="https://github.com/user-attachments/assets/de3b22ef-4219-4834-b51a-a66272fec9dc" />
"Can we remove mandatory to select centre and also allow to assign to user"

# Next-Level Setup Changes

<img width="388" height="845" alt="image" src="https://github.com/user-attachments/assets/dd91779d-5985-4b67-b041-ae9ab2740239" />

* The child list should include filtering by age (ascending/descending).
* Filter staff by location in the staff listing.
* Filter centres by region — needs discussion.
* Center Management changes:
  * `CRC PAYROLL` → `CRC ID`
  * `CRC BUSINESS NO` → `Business No`
* Added Vancouver and Chef's Corner, but duplicate entries appear in the centres list — needs discussion.
* Add a section for wage increases and dates:
  * Wage increase: `$ amount`
  * Date when wages should be updated
* Add search options for staff and children.


* here are the issues I’m currently having with the portal.
I’m unable to create and save a new child profile because there is no fee schedule added (I’ve attached a screenshot for reference). It also won’t allow me to select the days of attendance. When I try to click “create child,” at the bottom it says that I’m missing banking information, but there are no indicators showing that those fields are required.
Additionally, not an urgent issue, but I noticed there are two “E’s” in “Enter Home Address” if that’s something they can or want to correct if they're already in there!
I’ve attached screenshots to help, hopefully they’re useful!
<img width="1280" height="434" alt="image" src="https://github.com/user-attachments/assets/86980325-d3fe-45d8-bc70-a4ef4e3f5489" />

* Let’s create one email address where all people who are testing their system, if they have any issues they can send us an email and you guys can directly solve this and respond back to them with solutions or what to do.
---
  
### Child Master

* The child list should support search functionality for both parent and child names.
* Search should also be possible based on status, with proper filtering options.

---

# Center 

* Add delete options in edit doc section 



## 2. Reference Letter Upload Enhancement

### Requirement

* Allow uploading of **multiple reference letter documents**.
* A minimum of **three reference letters** should be supported.
* Users should be able to upload multiple files without restrictions on a single document upload.

---

## 3. File Upload Issue

### Current Issue

* The file upload functionality currently allows only a **single file upload**.

### Required Fix

* Enable support for **multiple file uploads** where applicable.
* Verify and resolve any validation or configuration issues preventing multiple document uploads.

# GENERAL SYSTEM RULES

- All delete operations must be **Soft Delete**  
- Audit log must track:
  - Who created  
  - Who updated  
  - Created date & time  
  - Updated date & time  

# Whole System UI Changes 

# ACCOUNTING (ACCB) MODULE

- Export PDF data to CSV.  
- Directly upload into each report.  
- Automatic counting functionality is required.  

---
# Employee Module 

* Add step-by-step Employee Master documentation covering employee account creation and management.
* Documented the complete employee login process.
* Add Forgot Password flow with password reset steps.
* Included re-login process after successful password reset.

* Added Employee Master documentation covering account creation, login, forgot password, and password reset flows.
* Implemented System Login Logs to track user login activity; accessible only by Super Admin.
* Moved documents from the public folder to a secure internal location.
* Improved and organized documentation structure for better maintainability and security.
  
# Responsive webiste  & UI 
- Center Managnment
- Child Managnment
- Employee Managment
- Timeline Magagment

-  need to make the entire website responsive and mobile-friendly.

# Employee Module 

## 1. Employee Profile Workflow Setup

Implement a workflow in the Employee Module similar to the existing **Child Master** process:

**Current Child Master Workflow:**

1. Create
2. Review
3. Approve

**Proposed Employee Profile Workflow:**

1. Employee creates the profile.
2. Manager reviews the profile.
3. Manager approves the profile.

**Note:** The workflow requirements for the Employee Profile module need further discussion and confirmation.

### Fees Master

#### Changes 

1. **Fee Master Access for All User Types**

   * On the **Next Level Childcare** setup, Fee Master access has been enabled for **all user types**.

2. **Fee Master Documentation Add**

   * Added step-by-step documentation explaining how to add fees in Fee Master.
   * Included a tutorial video for easier understanding and user guidance.

3. **UI/UX Improvements**

   * Enhanced the overall user interface and user experience.
   * Improved layout, readability, and usability.

4. **Pagination Add**

   * Implemented pagination for better data management and performance.

5. **Sorting Functionality Add**

   * Added sorting options to help users organize records efficiently.

6. **Search Functionality Add**

   * Implemented search functionality for quick and easy record lookup.

7. **General Enhancements**

   * Refined the Fee Master module for better usability, consistency, and overall performance.
   * Fixed UI-related issues and improved responsiveness.

### Notes

* Fee Master access for all user types is enabled **only for the Next Level Childcare setup**.
* Documentation and video guide are available within the module for user reference.

---
### Employee Notification Requirements

1. Send a notification when a document is approaching its expiry date.

2. Include the following details in the notification:
   - Document name
   - Expiry date
   - Remaining days until expiry

3. Send an email notification for two cases:
   - Upcoming document expiry
   - Missing or pending documents

4. email notifications should automatically stop once the document's expiry date has passed.

5. No further reminders should be sent for documents whose expiry date has already expired.

----------------------------

# Required Changes / Enhancements

## 1. Reports – “NEW” Status Issue

* Fix the issue related to the **“NEW”** status in reports.
* Ensure records with “NEW” status display correctly in all relevant reports.

## 2. Dashboard – Review Children

* Add an option to **Review Children** directly from the dashboard.
* Users should be able to:

  * Approve
  * Reject
  * Edit
  * Send Back
* This should follow the same workflow as the existing approval process.

## 3. Wage Reports

* Retest wage reports after employee changes.
* Verify that all employee updates are reflected correctly in the reports.

## 4. Role Permissions

* Implement detailed **role-based and module-wise permissions**.
* Permissions should be configurable individually for each user.
* Admin should be able to control which modules each user can access.

## 5. Mobile Responsiveness

* Make every module fully mobile-friendly.
* Ensure all screens are responsive and work properly on mobile devices.

### 6. Admin Logs

* Maintain login and activity logs for all users.
* Admin can view user login/logout times and accessed modules.
* Support filtering by user and date.
