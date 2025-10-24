# Flow Setup (Power Automate)

1) Go to https://make.powerautomate.com → choose your environment.
2) Create a **Solution** → `ExpenseApproval`.
3) Inside the solution → **New → Cloud flow → Automated**.
4) Trigger: **Dataverse → When a row is added, modified or deleted**
   - Change Type: **Added**
   - Table name: **Expenses**
   - Scope: **Organization**
5) Add action: **Approvals → Start and wait for an approval**
   - Approval type: *Approve/Reject – First to respond*
   - Assigned to: **ManagerEmail** (from trigger)
   - Title/details: use dynamic fields (Title, Amount, Category, Employee)
6) Add **Condition**:
   - `Outcome` == `Approve`
   - If Yes:
     - **Dataverse → Update row** (Expenses.Status = Approved)
     - **Teams → Post message** to Finance channel (optional)
     - **Outlook → Send an email (V2)** to EmployeeEmail (Approved)
   - If No:
     - **Dataverse → Update row** (Expenses.Status = Rejected)
     - **Outlook → Send an email (V2)** to EmployeeEmail (Rejected)
7) Save and **Test** by creating a new Expense row in the Canvas app.
