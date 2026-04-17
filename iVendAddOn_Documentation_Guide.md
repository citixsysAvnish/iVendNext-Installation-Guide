# What Prompt to Write for Each Document

**For:** iVendAddOn Development Team
**Updated:** 2026-03-25

Your `docs/` folder for any feature should have these files, generated in this order. Below is the exact prompt to type into Claude for each one.

---

## Document Order

```
1. BRD  →  2. PRD  →  3. IMPL  →  4. UT  →  5. QA  → 6. PR → 7. ReleaseNote
                                       ↓         ↓
                                    4.1 UT-RESULT  5.1 QA-RESULT  →  6. PR-RESULT
```

Each document feeds into the next. Always generate them in order.

---

## 1. BRD — Business Requirements Document

**When:** You have a feature idea or a feature to port from another system.
**Input:** Your knowledge of the business need. Optionally, an existing spec from another product.

### Prompt to type:

> I need to build a **[feature name]** feature for iVendAddOn POS. Here's what it should do:
>
> [Describe the feature in your own words — 3-5 sentences. What problem does it solve? Who needs it? If porting from another system, mention that.]
>
> Create a BRD (Business Requirements Document) for this. Include business objectives, scope, stakeholders, functional requirements, validation rules with error messages, non-functional requirements, acceptance criteria (numbered AC-01 to AC-XX), and a glossary. Save it as `docs/[feature_folder]/1. BRD-[FeatureName]-iVendAddOn.md`

**Example (Barcode Masking):**

> I need to build a **Barcode Masking** feature for iVendAddOn POS. Many retailers use barcodes that embed price, quantity, or weight inside the barcode itself (common in grocery, deli, pharmacy). Right now when these are scanned, the embedded data is ignored and the cashier has to manually type the price. I want the system to automatically decode the embedded data from the barcode at scan time. This is being ported from iVend Retail Windows for feature parity.
>
> Create a BRD for this. Include business objectives, scope, stakeholders, functional requirements, validation rules with error messages, non-functional requirements, acceptance criteria (numbered AC-01 to AC-XX), and a glossary. Save it as `docs/bar_code_masking/1. BRD-BarCode-Masking-iVendAddOn.md`

---

## 2. PRD — Product Requirements Document

**When:** BRD is done.
**Input:** The BRD you just created.

### Prompt to type:
 
You are a business analyst creating a Product Requirements Document (PRD)

for an iVend Retail add-on project.
 
Read the requirement document provided at: [PATH TO REQUIREMENT FILE]
 
Create a concise, customer-friendly PRD and save it as:

[OUTPUT FILE PATH]
 
---
 
DOCUMENT HEADER

Include a header table at the top with these fields:

  - Customer      : [Customer Name]

  - Project       : [Project Code, e.g. CXS.A1CC – CRD005]

  - Platform      : [e.g. iVend Retail 6.6 (Management Console + Point of Sale)]

  - Prepared by   : CitiXsys Custom Development Team

  - Document date : [Today's date]

  - Version       : 1.0

  - Status        : Draft — Pending Customer Approval
 
---
 
TABLE OF CONTENTS

After the header, add a numbered Table of Contents listing all sections

in the document.
 
---
 
SECTIONS TO INCLUDE (in this order):
 
1. Original Requirement (Verbatim)

   - Copy the full content from the source document exactly as written.

   - Do not rephrase, summarise, or omit anything.

   - Include all clarification notes, updates, and examples from the source.
 
2. Overview

   - Brief summary of what the feature does and why it is needed.

   - Keep it business-friendly — no technical terms.
 
3. Scope

   - In Scope  : List all capabilities included in this delivery.

   - Out of Scope : List anything explicitly excluded or removed.

     If nothing is excluded, write:

     "All scenarios mentioned under In Scope are part of this requirement.

      Any other scenarios are considered out of scope."
 
4. Business Scenarios / User Flows

   - Describe how the feature will be used in real business terms.

   - Write as step-by-step flows (e.g. manager sets up promotion,

     cashier processes a sale, etc.).
 
5. Functional Requirements

   - List what the system must do, in plain business language.

   - Group by area if needed (e.g. Setup, POS Behaviour).

   - Number each requirement (FR-01, FR-02, ...).
 
6. Worked Examples

   - Include only if the feature involves calculations or conditional logic.

   - Use realistic sample data with clear inputs and expected outputs.
 
7. Screen Details

   - Include only for features that have a user interface (MC or POS).

   - For each screen provide:

       - Screen name and menu path

       - Fields with their purpose and whether they are mandatory

       - Action buttons and what they do

       - All messages and alerts shown to the user
 
8. Impact Analysis

   - List all previously delivered add-ons and features for this customer.

   - For each, state whether this new feature has any impact and explain why.

   - Also cover impact on iVend configuration, SAP/ERP, and master data.
 
9. Data Requirements

   - List the key data the feature needs to store or work with.

   - Present as named groups (e.g. Promotion Header, Slabs, Store Mapping)

     with a table of fields and their business purpose.

   - Keep it high-level — no database or technical terms.
 
10. Validation Rules

    - List only the important business rules that affect what a user can or

      cannot save/do.

    - Number each rule (V-01, V-02, ...).
 
11. Dependencies & Assumptions

    - Dependencies: What must be in place before this feature can work.

    - Assumptions: What has been agreed or taken for granted during design.
 
12. UAT Scenarios

    - List the key test cases the customer must validate.

    - Present as a table: Test Case ID | Scenario | Steps | Expected Result.

    - After the last test case, add this note exactly:

      "These are the UAT scenarios required to be validated by the customer.

       If the customer has any additional UAT scenarios, they must be

       communicated and agreed upon before SOW finalization."
 
13. Estimation

    - Provide a high-level effort estimate broken down by component.

    - Present as a table: Component | Estimated Hours.

    - Include a Total row at the bottom.

    - Add a note: "Any scope changes after sign-off will be estimated

      separately."
 
---
 
STRICT RULES:

- Do NOT include any technical details (no code, no database schema,

  no architecture, no API references).

- Keep all language simple and business-oriented.

- The document must be suitable for customer review and sign-off.

- Keep it structured, concise, and easy to read.

- Use Markdown formatting throughout.
 
---

## 3. IMPL — Implementation Plan

**When:** PRD is done and approved.
**Input:** The BRD + PRD + your project's CLAUDE.md.

### Prompt to type:

> Read the BRD and PRD in `docs/[feature_folder]/`. Also read the project CLAUDE.md for coding conventions.
>
> Create an Implementation Plan that a developer can follow step-by-step to build this feature. Break it into phases (Phase 1, Phase 2, etc.). For each phase, give exact file paths to create or modify, class/method names, field lists, validation logic, and error message constants.
>
> Include a testing section with: Group A (automated unit tests — table of UT-XX IDs), Group B (API tests — manual with curl examples), Group C (Desk UI tests — manual), Group D (integration tests — manual), Group E (offline tests — manual), Group F (edge cases — table of EC-XX IDs).
>
> End with a deployment checklist and rollback plan.
>
> Save it as `docs/[feature_folder]/3. IMPL-[FeatureName]-iVendAddOn.md`

---

## 4. UT — Unit Test Specification

**When:** IMPL is done. Tests are written.
**Input:** The IMPL testing section + the actual test code file.

### Prompt to type:

> Read the IMPL at `docs/[feature_folder]/3. IMPL-[FeatureName]-iVendAddOn.md` (testing section) and the actual test file at `[path to test_*.py]`.
>
> Create a Unit Test Specification document. For each test, list: Test ID, method name, description, setup, expected result. Group them by test class. Add an IMPL traceability section showing which IMPL test IDs map to which actual tests, noting any deviations.
>
> Save it as `docs/[feature_folder]/4. UT-[FeatureName]-iVendAddOn.md`

---

## 4.1 UT-RESULT — Unit Test Results

**When:** After running unit tests.
**Input:** Just tell Claude to run the tests.

### Prompt to type:

> Run the unit tests for [DocType Name] and save the results to `docs/[feature_folder]/4.1 UT-[FeatureName]-iVendAddOn-RESULT.md`. Each run should be timestamped and appended — never overwrite previous runs. Include a summary table (total/passed/failed/time) and per-test results.

---

## 5. QA — QA Test Plan

**When:** IMPL is done. Code is written.
**Input:** The IMPL (manual test groups) + PRD (acceptance criteria) + source code.

### Prompt to type:

> Read the IMPL at `docs/[feature_folder]/3. IMPL-[FeatureName]-iVendAddOn.md` and the PRD at `docs/[feature_folder]/2. PRD-[FeatureName]-iVendAddOn.md`. Also read the source code for this feature.
>
> Create a QA Test Plan for manual testing. Organize into sections: Form UI, Validation Rules, Integration with other DocTypes, Dialogs, End-to-End Online, End-to-End Offline, Negative/Edge Cases, API Endpoints, Deletion/Disable, Related Features, and Permissions. Each test case needs: ID, description, step-by-step instructions, expected result, and which PRD acceptance criterion it covers.
>
> End with a traceability matrix mapping every PRD AC (AC-01 to AC-XX) to at least one QA test case. Target 80-120 test cases total.
>
> Save it as `docs/[feature_folder]/5. QA-[FeatureName]-iVendAddOn.md`

---

## 5.1 QA-RESULT — QA Test Results

**When:** After a QA tester executes the QA test cases.
**Input:** The tester's results (or Claude drives the browser via the automated test script).

### Prompt to type:

> Using the QA test script already saved at `docs/[feature_folder]/qa_[feature]_test.py`, execute all test cases against the live site (only those marked as fully automated — I am expecting [N] test cases that you identified as fully automated).
>
> **Setup & Access**
> - URL: http://refactor.iVendAddOn.com:8001
> - Login: administrator / Pass@123
> - The bench is already running
> - The script uses Playwright in headed mode — set `DISPLAY=:10` before running
>
> **Starting State**
> The script handles its own clean slate automatically via `full_cleanup()` at startup:
> - Unassigns `custom_[field]` from all CLD Items
> - Deletes all [DocType] records whose name starts with `CLD`
> - Deletes all Item records whose `item_code` starts with `CLD`
>
> Do not manually pre-clean anything — let the script do it.
>
> **Execution**
> Run the script from its permanent location:
> ```bash
> cd /home/frappe/MNJ-BENCH
> DISPLAY=:10 python apps/iVendAddOn_pos/docs/[feature_folder]/qa_[feature]_test.py
> ```
> Do not copy the script to `/tmp/` or run it from anywhere else.
>
> **Output**
> On completion, log all test results in `docs/[feature_folder]/5.1 QA-[FeatureName]-iVendAddOn-RESULT.md`. Each QA round is timestamped and appended — never overwrite previous runs. For each test: ID, result (PASS/FAIL/BLOCKED), and notes if failed. Include a summary with pass rate. List any defects raised.

**Example (Barcode Masking):**

> Using the QA test script already saved at `docs/bar_code_masking/qa_barcode_mask_test.py`, execute all barcode masking test cases against the live site (only those marked as fully automated — I am expecting 92 test cases that you identified as fully automated).
>
> **Setup & Access**
> - URL: http://refactor.iVendAddOn.com:8001
> - Login: administrator / Pass@123
> - The bench is already running
> - The script uses Playwright in headed mode — set `DISPLAY=:10` before running
>
> **Starting State**
> The script handles its own clean slate automatically via `full_cleanup()` at startup:
> - Unassigns `custom_barcode_mask` from all CLD Items
> - Deletes all Barcode Mask records whose name starts with `CLD`
> - Deletes all Item records whose `item_code` starts with `CLD`
>
> Do not manually pre-clean anything — let the script do it.
>
> **Execution**
> Run the script from its permanent location:
> ```bash
> cd /home/frappe/MNJ-BENCH
> DISPLAY=:10 python apps/iVendAddOn_pos/docs/bar_code_masking/qa_barcode_mask_test.py
> ```
> Do not copy the script to `/tmp/` or run it from anywhere else.
>
> **Output**
> On completion, log all test results in `docs/bar_code_masking/5.1 QA-BarCode-Masking-iVendAddOn-RESULT.md`.

---

## 6. PR-RESULT — PR Review Results

**When:** PR is created and ready for review.
**Input:** The PR number or branch name.

### Prompt to type:

> Review PR #[number] and save the results to `docs/[feature_folder]/6. PR-[FeatureName]-iVendAddOn-RESULT.md`. Each review is timestamped and appended — never overwrite. List critical issues, important issues, medium issues, positive observations, and a verdict (Approve/Request Changes). Only report issues with confidence >= 80%.

---

## 7. RN — Release Notes

**When:** Feature is complete, tested, and ready to ship.
**Input:** The PRD + IMPL.

### Prompt to type:

> Read the PRD and IMPL in `docs/[feature_folder]/`. Create release notes. Include: what's new (new DocTypes, POS changes, offline support), how to set up (numbered steps), key business rules in plain English, known limitations, technical notes for IT admins (migration, cache, custom fields), and upgrade instructions (bench commands). Keep it to 1-2 pages.
>
> Save it as `docs/[feature_folder]/8. RN-[FeatureName]-iVendAddOn.md`

---

## 8. UM — User Manual

**When:** Feature is complete and tested.
**Input:** The BRD + PRD.

### Prompt to type:

> Read the BRD and PRD in `docs/[feature_folder]/`. Create a user manual for store managers and cashiers. Write step-by-step instructions with "Go to...", "Click...", "Enter..." language. Include: creating the configuration (with a worked example using real data), testing before going live, assigning to items, what happens at the POS, disabling/deleting, troubleshooting table (Problem → Cause → Solution), and a field description reference table.
>
> Save it as `docs/[feature_folder]/9. UM-[FeatureName]-iVendAddOn.md`

---
## File Naming

```
[Order]. [Type]-[FeatureName]-iVendAddOn.md

Examples:
  1. BRD-GiftCard-iVendAddOn.md
  2. PRD-GiftCard-iVendAddOn.md
  3. IMPL-GiftCard-iVendAddOn.md
  4. UT-GiftCard-iVendAddOn.md
  4.1 UT-GiftCard-iVendAddOn-RESULT.md
  5. QA-GiftCard-iVendAddOn.md
  5.1 QA-GiftCard-iVendAddOn-RESULT.md
  6. PR-GiftCard-iVendAddOn-RESULT.md
  7. RN-GiftCard-iVendAddOn.md
  9. UM-GiftCard-iVendAddOn.md
```

---

## Tips

- **Always generate in order** — each doc builds on the previous one
- **Give Claude the previous docs as input** — it produces much better output
- **Review each doc before moving to the next** — errors compound
- **The BRD prompt is the most important** — everything else flows from it. Spend time describing the feature well.
- **For UT-RESULT and QA-RESULT** — always append, never overwrite. You want the history.
- **Run PR review multiple times** — fix issues between rounds until you get a clean "Approve"
