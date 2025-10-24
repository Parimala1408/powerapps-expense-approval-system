## Dataverse Tables

### Expenses
- ExpenseID (Auto Number) — Primary Name: Title
- Title (Text)
- Employee (Text)
- EmployeeEmail (Text)
- Department (Choice: HR, Finance, IT, Sales, Ops, Other)
- Amount (Currency)
- Category (Choice: Travel, Meals, Supplies, Software, Other)
- ReceiptUrl (Text)
- Status (Choice: Pending, Approved, Rejected, Paid)
- SubmittedOn (DateTime)
- ManagerEmail (Text)

### Approvals
- ApprovalID (Auto Number)
- Expense (Lookup → Expenses)
- ApproverEmail (Text)
- Decision (Choice: Pending, Approved, Rejected)
- DecisionOn (DateTime)
- Comments (Multiline)

### Relationships
- Approvals.Expense → Expenses.ExpenseID (1:N)
