# Power Fx Snippets (Canvas App)

## Submit Button (OnSelect)
If(
    IsBlank(txtTitle.Text) || IsBlank(txtAmount.Text) || IsBlank(txtManagerEmail.Text),
    Notify("Title, Amount and Manager Email are required.", NotificationType.Error),
    Patch(
        Expenses,
        Defaults(Expenses),
        {
            Title: txtTitle.Text,
            Employee: User().FullName,
            EmployeeEmail: User().Email,
            Department: drpDepartment.Selected.Value,
            Amount: Value(txtAmount.Text),
            Category: drpCategory.Selected.Value,
            ReceiptUrl: txtReceiptUrl.Text,
            Status: "Pending",
            SubmittedOn: Now(),
            ManagerEmail: txtManagerEmail.Text
        }
    );
    Reset(txtTitle); Reset(txtAmount); Reset(txtReceiptUrl); Reset(txtManagerEmail);
    Notify("Expense submitted for approval!", NotificationType.Success)
);

## List Expenses (Gallery.Items)
SortByColumns(Filter(Expenses, EmployeeEmail = User().Email), "SubmittedOn", Descending)

## Status Color (e.g., Label.Color)
Switch(
    ThisItem.Status,
    "Approved", ColorValue("#16a34a"),
    "Rejected", ColorValue("#dc2626"),
    "Pending",  ColorValue("#ca8a04"),
    "Paid",     ColorValue("#2563eb"),
    Color.Black
)

## Basic Validation for Amount (txtAmount.OnChange)
If(!IsNumeric(Self.Text) || Value(Self.Text) <= 0,
    Notify("Enter a positive number for Amount.", NotificationType.Warning)
)
