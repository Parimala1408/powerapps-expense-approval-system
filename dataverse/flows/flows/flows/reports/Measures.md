# Power BI – Suggested Measures (DAX)

Total Amount = SUM(Expenses[Amount])

Approved Amount = CALCULATE([Total Amount], Expenses[Status] = "Approved")

Rejected Amount = CALCULATE([Total Amount], Expenses[Status] = "Rejected")

Approval Rate % = 
VAR approved = CALCULATE(COUNTROWS(Expenses), Expenses[Status] = "Approved")
VAR total    = COUNTROWS(Expenses)
RETURN DIVIDE(approved, total)

Avg Approval Time (hrs) =
VAR t =
    AVERAGEX(
        FILTER(Approvals, Approvals[Decision] = "Approved"),
        DATEDIFF(Approvals[CreatedOn], Approvals[DecisionOn], HOUR)
    )
RETURN t
