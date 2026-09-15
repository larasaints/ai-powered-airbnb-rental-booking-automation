# 🤖 AI-Powered Airbnb Rental Booking Automation Engine
An enterprise-grade, event-driven operations automation pipeline designed to eliminate short-term property rental overhead. This system catches inbound property inquiries, cross-references calendar availability arrays, runs contextual multi-tiered pricing analysis using **Gemini 3.6 Flash**, manages database states, and dynamically builds and stages production-ready raw HTML email responses in Gmail.

## 🚀 The Core Business Challenge
Manual daily/short-term/yearly rental management introduces severe processing latency, human calculation errors in weekend/weekday pricing matrices, and scheduling vulnerabilities. This pipeline provides complete system isolation for
 **Casa De Lara by SMDC** properties (Shore Residences Pasay & Jazz Residences Makati), safely scaling operations without increasing headcount.

## 🛠️ Technical Architecture & Pipeline Topology
The workflow operates via a tightly decoupled 4-tier processing layout:

1. **Ingestion Layer (`google-sheets:watchRows`)**: Pulls webhook-like chronological tracking arrays from the database (`Form Responses 1`), extracting visitor profiles, headcount configurations, property constraints, and booking windows.
2. **Conditional Validation Guardrail (`google-calendar:searchEvents`)**: Executes lookup queries against calendar timelines using custom boundaries:
   * `timeMin`: `{{parseDate(12.checkIn; "MM/DD/YYYY")}}`
   * `timeMax`: `{{addDays(parseDate(12.checkOut; "MM/DD/YYYY"); 1)}}`
3. **Logic Routing & Failure Mitigation (`builtin:BasicRouter`)**: Checks the length array (`__IMTLENGTH__`). If an intersection is found (>0), it forks to a multi-channel graceful exit path updating the sheet to "Fully Booked" and staging rejection responses. If 0 conflicts exist, the main booking pipeline unlocks.
4. **Context-Aware Prompt Engineering & GenAI Layer (`gemini-ai`)**: Calls Gemini 3.6 Flash using a rigid system instructions matrix to calculate subtotals, enforce standard check-in/out policies, and render localized HTML customer assets.
5. **Execution Layer (`Gmail / Calendar API`)**: Commits calendar holds with embedded metadata tokens and creates structured draft emails inside Gmail using `rawHtml` payload delivery.

## 📊 Business Rules & Segmented Profile Intelligence
* **Prospective Tenants**: Automatically computes tiered room totals (headcount + seasonal rules) and appends an itemized, fully-refundable ₱1,000 Security Deposit line item alongside integrated BDO/GCash payment components.
* **Licensed Real Estate Brokers**: Strips away standard payment sections, enforces base fixed pricing logic, displays partner commission markup warnings, and appends mandatory PRC ID verification hooks to finalize viewings.

## 📊 System Architecture (Backend Workflow)
Below is the event-driven logical pipeline built to process, filter, and route the inbound short-term rental data:<br>
<img width="1071" height="494" alt="The Architecture Make Scenario Layout" src="https://github.com/user-attachments/assets/d26e749f-cdff-4fae-a778-59359deeede2" />


---
## 📅 Data Ingestion & State Database (Google Sheets)
This sheet functions as the operational database layer, catching inbound submissions and storing AI categorization states alongside calculated response strings: <br>
<img width="1115" height="543" alt="The Data Flow Google Sheet Headers" src="https://github.com/user-attachments/assets/f52ccf8e-7551-471f-8d1b-dcc24d226bdb" />


---
## 📧 Live Output Generation Demo (Frontend Result)
This is the final production-ready raw HTML email template dynamically calculated and staged inside Gmail by the engine:

<strong> Gmail Draft Output Demo Test 01 Jazz Available</strong> <br>
<img width="1216" height="2368" alt="Test01 Jazz Available" src="https://github.com/user-attachments/assets/acb80004-c872-442f-bf45-0f34f06e9237" />


<strong> Gmail Draft Output Demo Test 02 Jazz Unvailable</strong> <br>
<img width="1160" height="1168" alt="Test 02 Jazz Unavailable" src="https://github.com/user-attachments/assets/110dc08f-d729-4c29-9376-76058c661db0" />


<strong> Gmail Draft Output Demo Test 03 Shore Available</strong> <br>
<img width="1184" height="1500" alt="Test03 Shore Available" src="https://github.com/user-attachments/assets/99de4e89-b459-476a-9150-e807e063a775" />


<strong> Gmail Draft Output Demo Test 04 Shore Unavailable</strong> <br>
<img width="1160" height="568" alt="Test 4 Shore Unavailable" src="https://github.com/user-attachments/assets/a98d5583-3358-4754-8fdc-326e53de4dd6" />




