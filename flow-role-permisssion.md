You already implemented most of the **role-based child flow (Admin / Manager)** correctly. I’ll explain the **complete flow of Roles & Permissions for Child Management** based on your code so you clearly understand what happens at each stage.

---

# 1️⃣ Roles in Your System

From your controller and blade:

* **Superadmin**
* **Admin**
* **Manager**

Helper method used:

```php
$user->isAdminOrSuperadmin()
```

Which means:

| Role       | Permissions                    |
| ---------- | ------------------------------ |
| Superadmin | Full control                   |
| Admin      | Full control                   |
| Manager    | Limited (request actions only) |

---

# 2️⃣ Child Status Meaning

Your code uses this array in `show.blade.php`:

```php
$statuses = ['Review', 'Active', 'Withdrawal', 'Archive'];
```

| Status | Meaning                   |
| ------ | ------------------------- |
| **0**  | Review (waiting approval) |
| **1**  | Active                    |
| **2**  | Withdrawal                |
| **3**  | Archive                   |

---

# 3️⃣ Child Lifecycle Flow

Here is the **full child flow**.

```
Create Child
     │
     ▼
Status = 0 (Review)
     │
     │ Manager → Request Approval
     │
     ▼
Admin Approves
     │
     ▼
Status = 1 (Active)
     │
     ├── Manager Request Withdrawal
     │
     ▼
Withdrawal Pending
     │
     ▼
Admin Approves Withdrawal
     │
     ▼
Status = 2 (Withdrawal)
```

---

# 4️⃣ Approval Flow (Manager vs Admin)

## Manager Flow

Manager **cannot approve directly**.

### Show Page Button

```php
@if (!$user->isAdminOrSuperadmin())
<button class="btn btn-info-light btn-sm">
Request Approval
</button>
@endif
```

Controller:

```php
if ($role === 'Manager') {
    Notification::send($admins, new ChildPendingApprovalNotification($child));
}
```

So:

Manager → Request Approval → Admin gets notification

---

## Admin Flow

Admin can directly approve.

```php
if ($child->status == 0) {
    $child->status = 1;
    $child->save();
}
```

Notification sent.

---

# 5️⃣ Withdrawal Flow

### Manager Request Withdrawal

Manager clicks:

```
Request Withdrawal
```

Form sends:

```
action = withdraw
```

Controller:

```php
if ($r->input('action') === 'withdraw') {

$data['withdrawal_date'] = $r->withdrawal_date;
$data['withdrawal_requeste_date'] = now();
$data['withdrawal_note'] = $r->withdrawal_note;

unset($data['status']);
}
```

Important:

Manager **cannot change status**.

Status remains:

```
status = 1 (Active)
```

But request exists.

---

### Show Page Indicator

```php
@if($child->status == 1 && $child->withdrawal_requeste_date && !$user->isAdminOrSuperadmin())
<span class="badge bg-info">
Withdrawal Request Pending
</span>
@endif
```

---

# 6️⃣ Admin Withdrawal Approval

Admin sees button:

```php
@if($child->status == 1 && $child->withdrawal_date && $user->isAdminOrSuperadmin())
<button>
Approve Withdrawal
</button>
@endif
```

Controller:

```php
public function approveWithdrawal($id)
{
$child->status = 2;
$child->save();
}
```

Now child becomes:

```
Status = 2 (Withdrawal)
```

---

# 7️⃣ Delete Flow

### Manager

Manager cannot delete.

Show page:

```
Request Delete
```

Controller:

```php
if (!$user->isAdminOrSuperadmin()) {

Notification::send($admins, new ChildDeletePendingNotification($child));

return back()->with('success','Delete request sent to Admin.');
}
```

---

### Admin

Admin can delete directly.

```php
$child->delete();
```

---

# 8️⃣ Edit Permissions

Your blade allows **both roles to edit**.

```php
<a href="{{ route('current-child.edit', $child->child_id) }}">
Edit
</a>
```

But behavior changes:

| Role    | Action                            |
| ------- | --------------------------------- |
| Manager | Can edit but only request actions |
| Admin   | Full update + approval            |

---

# 9️⃣ Notifications in Your Flow

You already implemented these:

| Action                 | Notification                         |
| ---------------------- | ------------------------------------ |
| Child Approval Request | `ChildPendingApprovalNotification`   |
| Child Approved         | `ChildApprovedNotification`          |
| Withdrawal Request     | `ChildWithdrawalPendingNotification` |
| Withdrawal Approved    | `ChildStatusChanged`                 |
| Delete Request         | `ChildDeletePendingNotification`     |

---

# 🔟 Complete Role Permission Table

| Action             | Manager | Admin | Superadmin |
| ------------------ | ------- | ----- | ---------- |
| Create Child       | ✅       | ✅     | ✅          |
| Edit Child         | ✅       | ✅     | ✅          |
| Approve Child      | ❌       | ✅     | ✅          |
| Request Approval   | ✅       | ❌     | ❌          |
| Request Withdrawal | ✅       | ❌     | ❌          |
| Approve Withdrawal | ❌       | ✅     | ✅          |
| Delete Child       | ❌       | ✅     | ✅          |
| Request Delete     | ✅       | ❌     | ❌          |
