# Excel Formula Integrity Validation Using Power Automate

## Overview

This project demonstrates how to use **Power Automate**, **Excel Online**, and **Outlook** to identify formula validation errors that may not always be detected in Excel’s **Agent Mode**.

While Agent Mode introduces AI-driven assistance in Excel, it currently has limitations in financial modeling scenarios, especially where **formula dependencies** and **reconciliation checks** are involved.

This project aims to close that gap by creating a validation automation workflow.

---

## Dataset Used

| Check Name | Status | Timestamp |
|-------------|---------|-----------|
| Assets = Liabilities + Equity | Valid | 11/04/2025 03:30 |
| Cash Flow Reconciliation | Valid | 11/04/2025 03:30 |
| Net Income Flow-through | Error | 11/04/2025 03:30 |
| Test Error Trigger | Error | 11/04/2025 03:30 |

---

## Power Automate Flow Logic

1. **Trigger:**  
   Starts when an Excel file in OneDrive is modified.

2. **List Rows:**  
   Retrieves validation data from a table in Excel.

3. **Filter Array:**  
   Keeps only rows where `Status = "Error"`.

4. **Initialize Variable:**  
   Creates a string variable `ErrorSummary` for formatted results.

5. **Apply to Each:**  
   Adds each failed check (with timestamp) to the summary list.

6. **Condition:**  
   - If errors exist → Sends an email alert.  
   - If no errors → Ends quietly.

7. **Send Email:**  
   Sends an HTML email with **bolded** and **red-highlighted** error details.

---

## Sample Output (Email)

**Subject:** Financial Model Validation Errors Found  

**Body:**  
A validation error was found in your financial model.  

Errors:  

<span style="color:#d9534f; font-weight:bold;">Net Income Flow-through: Error (11/04/2025 03:30)</span>  
<span style="color:#d9534f; font-weight:bold;">Test Error Trigger: Error (11/04/2025 03:30)</span>  

Please review the Excel model and correct the issues.

---

## Why It Matters

According to [Microsoft Support: FAQ about Agent Mode in Excel (Frontier)](https://support.microsoft.com/en-us/office/faq-about-agent-mode-in-excel-frontier):

> “Agent Mode in Excel uses AI to generate suggestions and results. While powerful, it can sometimes make mistakes, misinterpret information, or produce inaccurate outcomes.”

This project provides a **real-time validation layer** outside of Agent Mode — improving accuracy and maintaining audit trails in financial models.

---

## Screenshots

- **Flow Overview:**  
  ![Flow Overview](./screenshots/flow-overview.png)

- **Email Output:**  
  ![Email Output](./screenshots/email-output.png)

---

## Next Steps

Part Two will focus on **testing the Formula Integrity Flow with Agent Mode in Excel** to evaluate:
- How AI-driven results compare to Power Automate validation outcomes.
- Which error scenarios are flagged or missed.
- How integration could evolve for enterprise-grade financial checks.

---

## License
MIT License © 2025
