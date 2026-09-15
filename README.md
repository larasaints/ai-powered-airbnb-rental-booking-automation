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
<img src="./assets/The%20Architecture%20Make%20Scenario%20Layout.png" alt="Make.com System Architecture" width="500"/>


---
## 📅 Data Ingestion & State Database (Google Sheets)
This sheet functions as the operational database layer, catching inbound submissions and storing AI categorization states alongside calculated response strings: <br>
<img src="./assets/The%20Data%20Flow%20Google%20Sheet%20Headers.png" alt="Google Sheets Data Tracking Layer" width="500"/>


---
## 📧 Live Output Generation Demo (Frontend Result)
This is the final production-ready raw HTML email template dynamically calculated and staged inside Gmail by the engine:

### 🏢 Unit 1 Gmail Draft AI Output Demo Test 01 & 02

| 🟢 Unit Available Layout | 🔴 Unit Unavailable Layout |
| :---: | :---: |
| <img src="./assets/Email%20Demo%20Test%2001%20Jazz%20Available.png" alt="Jazz Available" width="280"/> | <img src="./assets/Email%20Demo%20Test%2002%20Jazz%20Unavailable.png" alt="Jazz Unavailable" width="280"/> |

### 🏖️ Unit 2 Gmail Draft AI Output Demo Test 03 & 04

| 🟢 Unit Available Layout | 🔴 Unit Unavailable Layout |
| :---: | :---: |
| <img src="./assets/Email%20Demo%20Test%2003%20Shore%20Available.png" alt="Shore Available" width="280"/> | <img src="./assets/Email%20Demo%20Test%2004%20Shore%20Unavailable.png" alt="Shore Unavailable" width="280"/> |

