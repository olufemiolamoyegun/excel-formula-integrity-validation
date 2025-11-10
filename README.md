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


**HTML Version (with red highlights):**
<span style="color:#d9534f;">Net Income Flow-through: Error (11/04/2025 03:30)</span>  
<span style="color:#d9534f;">Test Error Trigger: Error (11/04/2025 03:30)</span>

---

## Flow Setup Example

### Connection References
![Connection References](Screenshot%202025-11-05%20at%2004.24.07.png)

### Flow Steps
![Power Automate Flow](Screenshot%202025-11-05%20at%2004.24.44.png)

---

## Why This Matters

While **Agent Mode** in Excel boosts productivity, it can:
- Miss formula linkage or integrity issues  
- Misinterpret dependent relationships  
- Modify workbooks directly without validation records  

This Power Automate flow helps:
- Maintain formula integrity  
- Provide real-time alerts  
- Preserve a transparent audit trail  

---

## References

- [Microsoft Support: FAQ about Agent Mode in Excel (Frontier)](https://support.microsoft.com/en-us/office/agent-mode-faq)  
- [Microsoft Tech Community – Excel AI and Agent Mode Discussions](https://techcommunity.microsoft.com/t5/excel/ct-p/Excel_Cat)

---

## Author

Created by **[Olufemi Olamoyegun]**  
Exploring automation workflows that strengthen Excel’s reliability for financial modeling and validation.

