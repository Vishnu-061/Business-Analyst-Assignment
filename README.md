Clinic Operations Control System (Healthcare SMB Clinics)

Overview
This repository documents a **lightweight operations control system** designed for small healthcare clinics where:
- Medicines are not barcoded
- Entries are manual
- Doctors are overloaded with non-clinical work
- Errors are small but frequent

The system focuses on **process discipline, micro-checks, and structured workflows**, not heavy software or ERPs.


Objectives
- Protect doctor time (≤10 minutes per review cycle)
- Reduce manual errors in pharmacy & communication
- Ensure accurate billing, inventory tracking, and patient follow-ups
- Absorb daily operational chaos into simple systems staff can run



SYSTEM 1: Pharmacy Inventory & Billing Control  
*(Business Analyst – Operations Accuracy System)*

What This Solves
- Wrong medicine entries
- Quantity mismatches
- Revenue leakage
- End-of-day confusion


Core Principle
**Do not reconcile at month-end. Detect errors daily in small doses.**


Step 1: Medicine Master Control
Create a **Medicine_Master** sheet with:
- Medicine Name
- Strength
- Unit Type (Strip / Bottle)
- Standard Selling Price
- Reorder Threshold

This becomes the **single source of truth**.


Step 2: Daily Sales Entry Discipline
Every sale must include:
- Medicine Name (dropdown)
- Quantity
- Price auto-filled
- Manual override flagged

Staff are trained to **pause if dropdown is unavailable**.


step 3: Micro-Checks (Daily)
Run 3 checks daily:
1. **Price Deviation Check** – any manual price edits
2. **High Quantity Check** – unusually large quantities
3. **Stock Risk Check** – nearing reorder threshold

Purpose: Alert staff, not punish them.


Step 4: Doctor Involvement (Only Exceptions)
Doctor is consulted only when:
- Medicine substitution occurred
- Clinical judgment affected inventory choice

Doctor never checks stock or bills.


Step 5: Daily Closure (5 minutes)
Before closing:
- Resolve flagged rows
- Carry forward unresolved items
- No backlog allowed


SYSTEM 2: Patient Care & Communication Control  
*(Patient Follow-up & WhatsApp Chaos Reduction)* :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}


What This Solves
- Doctor replying to WhatsApp messages
- Forgotten follow-ups
- Ad-hoc patient communication
- Context switching


Allowed Tools
- Hospital Management Software (HMS)
- Google Sheets
- Google Forms
- (Optional) Google Apps Script


Step 1: Message Type Classification
Create a **Message_Type_List**:

| Message Type | Doctor Input Needed |
|-------------|-------------------|
| Follow-up Reminder | No |
| Post-Procedure Care | No |
| Side-Effect Advisory | No |
| Custom Instruction | Yes |
| Patient Question Response | Yes |

This ensures **medical judgment is used only when required**.


Step 2: Care Control Sheet
Create one sheet: **Care_Control**

| Patient | Phone | Visit Type | Message Type | Message Text | Doctor Approval | Status |
|------|------|-----------|-------------|-------------|---------------|-------|

This sheet is the **single source of truth**.


Step 3: Doctor Review Window
Every 3–4 hours:
- Filter: `Doctor Approval = Required` AND `Status = Waiting`
- Sit with doctor for **10 minutes**
- Doctor dictates → Staff types once

Doctor never:
- Opens WhatsApp
- Types messages
- Replies individually


Step 4: Patient Question Handling
Patients submit questions via **Google Form**:
- Name
- Phone
- Question
- Urgency

Responses go to **Patient_Questions** sheet and are:
- Batched every 3 hours
- Reviewed once with doctor
- Sent systematically


Step 5: Message Dispatch Logic
Messages are sent only when:
- Message text is filled
- Status = Pending
- Approval = Not Required OR Approved
