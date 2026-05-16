# 🛡️ TPRM Insurance Certificate Collection Agent

> *Automating the end-to-end collection of vendor insurance certificates using Google Workspace and Zapier*

---

## 📌 Overview

As part of an annual Third Party Risk Management process, organisations are required to collect and verify insurance certificates from all third-party vendors. This typically involves manual outreach, response tracking, follow up reminders, and escalation management — a process that is time-consuming and prone to inconsistency.

This project presents a fully automated Insurance Certificate Collection Agent built using Google Forms, Google Sheets, Gmail, and Zapier. The agent manages the entire process from initial outreach to escalation, with no manual intervention required unless a vendor fails to respond after multiple attempts.

---

## 🎯 The Problem

| Challenge | Impact |
|---|---|
| Manual email outreach to multiple vendors | Time-consuming and inconsistent |
| Tracking responses across multiple vendors | Risk of missing responses or follow ups |
| Sending reminders manually | Dependent on human memory and availability |
| Escalating non-responses | Delayed action on high risk vendors |

---

## 💡 The Solution

A fully automated agent that:

1. 📧 Sends a personalised insurance certificate request email to each vendor
2. 📋 Captures vendor responses via a structured Google Form
3. 📊 Updates the Insurance Tracker automatically with response details
4. 🔔 Notifies the Risk Manager when a response is received
5. ⏰ Sends an automatic reminder if no response after 5 working days
6. ⚠️ Escalates to the Risk Manager if still no response after 7 working days

---

## 📋 Insurance Coverage Types Requested

1. Cyber Insurance
2. Errors & Omissions Tech
3. General Liability
4. Employer's Liability
5. Product Liability
6. Professional Liability
7. Crime

### Information Requested Per Coverage Type
- Certificate of Insurance
- Policy Number
- Effective Dates
- Duration
- Type of Cover
- Geographical Limits

---

## 🏗️ Architecture

```
TRIGGER
  └── Schedule by Zapier (Annual) OR Manual Run
        │
        ▼
ZAP 1 — INITIAL OUTREACH
  └── Read Vendor List from Google Sheets
        │
        ├── Send personalised email to each vendor
        │     (requesting 7 insurance certificates)
        │
        └── Update Insurance Tracker — Email Sent Date + Status: Pending
        │
        ▼
VENDOR ACTION
  └── Vendor submits Google Form with insurance details
        │
        ▼
ZAP 2 — RESPONSE CAPTURE
  └── Triggered by new Google Form submission
        │
        ├── Update Insurance Tracker — Status: Responded
        │
        └── Send notification email to Risk Manager
        │
        ▼
ZAP 3 — REMINDER (Day 5)
  └── Daily check — find vendors where:
        ├── Status = Pending
        ├── Follow Up Sent = No
        └── Email Sent Date > 5 working days ago
        │
        ├── Send reminder email to vendor
        │
        └── Update Insurance Tracker — Status: Follow Up Sent
        │
        ▼
ZAP 4 — ESCALATION (Day 7)
  └── Daily check — find vendors where:
        ├── Status = Follow Up Sent
        ├── Follow Up Sent = Yes
        └── Email Sent Date > 7 working days ago
        │
        ├── Send escalation alert to Risk Manager
        │
        └── Update Insurance Tracker — Status: Escalated
```

---

## 🔧 Tools Used

| Tool | Purpose | Cost |
|---|---|---|
| Google Sheets | Vendor master & insurance tracker | Free |
| Google Forms | Vendor response intake | Free |
| Gmail | All outbound emails | Free |
| Zapier | Automation backbone (4 Zaps) | Free tier |

---

## 📁 Repository Structure

```
tprm-insurance-automation/
│
├── README.md                          ← You are here
│
├── docs/
│   ├── architecture_diagram.md        ← Full pipeline diagram
│   ├── setup_guide.md                 ← Step by step implementation guide
│   └── user_manual.md                 ← How to operate the system daily
│
├── google_sheets/
│   └── insurance_tracker_setup.md     ← Column structure & setup guide
│
├── google_forms/
│   └── insurance_submission_form.md   ← Form fields & structure
│
├── zapier/
│   ├── zap1_initial_email.md          ← Initial email Zap configuration
│   ├── zap2_capture_response.md       ← Response capture Zap configuration
│   ├── zap3_reminder.md               ← 5 day reminder Zap configuration
│   └── zap4_escalation.md             ← Escalation alert Zap configuration
│
├── email_templates/
│   ├── initial_request.txt            ← Initial insurance request email
│   ├── reminder_email.txt             ← 5 day reminder email
│   └── escalation_alert.txt           ← Escalation alert email
│
└── sample_outputs/
    └── vendor_a_insurance_tracker.json ← Sample completed tracker
```

---

## 📊 Insurance Tracker — Column Structure

| Column | Field |
|---|---|
| A | Vendor ID |
| B | Vendor Name |
| C | Vendor Contact Email |
| D | Email Sent Date |
| E | Response Status |
| F | Cyber Insurance |
| G | Errors & Omissions Tech |
| H | General Liability |
| I | Employer's Liability |
| J | Product Liability |
| K | Professional Liability |
| L | Crime |
| M | Policy Numbers Provided |
| N | Effective Dates Provided |
| O | Duration Provided |
| P | Type of Cover Provided |
| Q | Geographical Limits Provided |
| R | Certificates Attached |
| S | Response Date |
| T | Days to Respond |
| U | Follow Up Sent |
| V | Notes |

---

## 🚦 Response Status Values

| Status | Meaning | Colour |
|---|---|---|
| Pending | Email sent, awaiting response | 🟡 Yellow |
| Responded | Vendor has submitted the form | 🟢 Green |
| Follow Up Sent | Reminder sent after 5 working days | 🟠 Orange |
| Escalated | No response after 7 working days | 🔴 Red |
| Complete | Review verified and closed | 🟢 Dark Green |

---

## 🚀 How to Use

1. Add your vendors to the **Vendor Master** tab in Google Sheets
2. Run **Zap 1** manually or schedule it annually
3. Vendors receive personalised emails and submit responses via Google Form
4. **Zap 2** captures responses and updates the tracker automatically
5. **Zap 3** runs daily and sends reminders to non-responsive vendors after 5 working days
6. **Zap 4** runs daily and escalates to you after 7 working days of no response
7. Your only manual intervention is when a vendor is escalated

---

## 👤 Author

**Shamshuddin Manji**
Third Party Risk Manager | HR Tech Systems
*ChatGPT & Zapier: Agentic AI for Everyone — Coursera, Vanderbilt University (2026)*
*Generative AI Foundations for HR Professionals — Coursera (2026)*

---

## 📜 Disclaimer

This is a live operational framework built for Third Party Risk Management purposes. Vendor details have been anonymised. Always involve legal and compliance teams for actual vendor risk decisions.

---

## ⭐ If you found this useful, leave a comment!
