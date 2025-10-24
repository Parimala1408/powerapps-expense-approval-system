# 💰 PowerApps Expense Approval System – Power Platform Project

A modern **Expense Approval System** built using **Power Apps**, **Dataverse**, **Power Automate**, and **Power BI** to automate expense tracking and approval workflows.

---

## 🚀 Features
- Submit expenses via **Power Apps Canvas App**
- Store data in **Dataverse**
- Automated approval workflow via **Power Automate**
- **Teams / Outlook** notifications for approvals
- Analytics dashboard in **Power BI**

---

## 🧱 Architecture

---

## ⚙️ Power Automate Flow
**Trigger:** When a new expense record is added  
**Actions:**
1. Send an approval email to the manager  
2. Update the Dataverse record with approval status  
3. Notify the employee in Teams or via Outlook email  

---

## 💾 Dataverse Tables
| Table | Description | Key Fields |
|--------|--------------|-------------|
| **Expenses** | Stores expense requests | ExpenseID, Title, Employee, Amount, Status |
| **Approvals** | Tracks manager decisions | ApprovalID, ExpenseID, Approver, Decision, Comments |

---

## 💡 Power Fx (Submit Button Example)
```plaintext
Patch(
    Expenses,
    Defaults(Expenses),
    {
        Title: txtTitle.Text,
        Employee: User().FullName,
        Amount: Value(txtAmount.Text),
        Category: drpCategory.Selected.Value,
        Status: "Pending"
    }
);
Notify("Expense submitted for approval!", NotificationType.Success);
Reset(txtTitle);
Reset(txtAmount);
