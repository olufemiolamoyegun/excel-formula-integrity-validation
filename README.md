# Excel Formula Integrity Validation Using Power Automate

## Overview

This project demonstrates how to use **Power Automate**, **Excel Online**, and **Outlook** to identify formula validation errors that may not always be detected in Excel’s **Agent Mode**.

While Agent Mode introduces AI-driven assistance in Excel, it has limitations in financial modeling, especially for **formula dependencies** and **reconciliation checks**.

This project creates a validation automation workflow to fill that gap.

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

1. **Trigger**  
   Starts when an Excel file in OneDrive is modified.

2. **List Rows**  
   Retrieves validation data from a table in Excel.

3. **Filter Array**  
   Keeps only rows where `Status = "Error"`.

4. **Initialize Variable**  
   Creates a string variable `ErrorSummary` for formatted results.

5. **Apply to Each**  
   Adds each failed check (with timestamp) to the summary list.

6. **Condition**  
   - If errors exist → Sends an email alert.  
   - If no errors → Ends quietly.

7. **Send Email**  
   Sends an HTML email with **bolded** and **red-highlighted** error details.

---

## Sample Output (Email)

**Subject:** Financial Model Validation Errors Found  

**Body (HTML version with red highlights):**  
<span style="color:#d9534f;">A validation error was found in your financial model.</span><br>
<span style="color:#d9534f;">Net Income Flow-through: Error (11/04/2025 03:30)</span><br>
<span style="color:#d9534f;">Test Error Trigger: Error (11/04/2025 03:30)</span><br>
Please review the Excel model and correct the issues.

---

## Flow Setup Example

### Folder Structure
![Folder Structure](https://raw.githubusercontent.com/olufemiolamoyegun/excel-formula-integrity-validation/main/Folder%20Structure)

### Email Alert Example
![Email Alert](https://raw.githubusercontent.com/olufemiolamoyegun/excel-formula-integrity-validation/main/Email%20Alert.png)

### Power Automate Flow
![Power Automate Flow](https://raw.githubusercontent.com/olufemiolamoyegun/excel-formula-integrity-validation/main/Power%20Automate%20Flow.png)

---

## Usage

1. Upload your Excel file to OneDrive and ensure the validation table exists.  
2. Update the Power Automate flow to point to the correct Excel file and table.  
3. Ensure the “Filter Array” step checks `Status = "Error"`.  
4. Save and test the flow. Any validation errors will trigger an email alert.  
5. Optional: Customize the email template to include additional formatting or recipients.

---

## Why This Matters

Excel’s **Agent Mode** can:

- Miss formula linkage or integrity issues  
- Misinterpret dependent relationships  
- Modify workbooks without validation records  

This Power Automate flow helps:

- Maintain formula integrity  
- Provide real-time alerts  
- Preserve a transparent audit trail  

---

## References

- [[Microsoft Support: FAQ about Agent Mode in Excel (Frontier)](https://support.microsoft.com/en-us/office/agent-mode-faq)  ](https://support.microsoft.com/en-us/office/frequently-asked-questions-about-agent-mode-in-excel-frontier-1cfd906d-40b4-46be-8e2d-65b893e28a02?utm_source=chatgpt.com)


---

## Author

Created by **Olufemi Olamoyegun**  
Exploring automation workflows that strengthen Excel’s reliability for financial modelling and validation.


