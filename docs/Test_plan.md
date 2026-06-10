# TEST PLAN — SWAG LABS (SauceDemo)

https://www.saucedemo.com

---

**SWAG LABS — SauceDemo**

| **Document ID** | SWG-TP-2026 |
|---|---|
| **Version** | 1.0 |
| **Date** | 02/06/2026 |
| **Based on** | SWG-RA-2026 (Approved) |
| **Prepared by** | QA Team |
| **Reviewed by** | Senior QA / PM |
| **Status** | APPROVED |


---

## 1. PROJECT OVERVIEW

Swag Labs (saucedemo.com) is a demo e-commerce web application developed and maintained by Sauce Labs — a leading software testing platform company. The application is intentionally designed as a realistic testing environment that simulates a complete online shopping flow from login to order completion.

A key characteristic of Swag Labs is that it deliberately integrates various types of bugs through separate test accounts, allowing testers to practice bug detection, analysis, and reporting skills in a near-real-world environment.

| **System Information** | **Details** |
|---|---|
| **Application Name** | Swag Labs (SauceDemo) |
| **URL** | https://www.saucedemo.com |
| **Application Type** | Single Page Application (SPA) — React |
| **Platform** | Web Browser (Desktop) |
| **Authentication** | Session-based (username + password) |
| **Backend** | API-driven (RESTful) |
| **Project Code** | SWG-TP-2026 |
| **RAD Reference** | SWG-RA-2026 — Approved 02/06/2026 |

### 1.1 Test Accounts Available

| **Username** | **Password** | **Account Type** | **Purpose / Characteristics** |
|---|---|---|---|
| **standard_user** | secret_sauce | Standard | Normal operation — Happy path testing |
| **locked_out_user** | secret_sauce | Locked Account | Blocked login — error handling for suspended accounts |
| **problem_user** | secret_sauce | Bug Account | Multiple intentional UI/UX bugs — visual bug detection |
| **performance_glitch_user** | secret_sauce | Performance | Abnormal slow loading — performance & timeout handling |
| **error_user** | secret_sauce | Form Error | Some form actions fail — error state in checkout |
| **visual_user** | secret_sauce | Visual Bug | Broken layout, CSS issues — visual regression testing |

---

## 2. TEST OBJECTIVES

The primary objectives of this test plan are aligned with the 36 Functional Requirements (FR) and 24 Non-Functional Requirements (NFR) identified in the Requirements Analysis Document SWG-RA-2026.

### 2.1 Functional Objectives

- Verify that all 6 user account types authenticate correctly per FR-001 to FR-006, including valid login, invalid credentials, and locked account scenarios.

- Confirm that the Product Inventory page displays all 6 products with correct information (name, image, description, price) and that all 4 sort options function correctly per FR-007 to FR-014.

- Validate the Add to Cart and Remove from Cart functionality from both Inventory and Product Detail pages, and that the cart badge updates accurately per FR-012 to FR-017.

- Ensure the Shopping Cart accurately reflects all added products with correct quantity, description, and pricing per FR-018 to FR-021.

- Verify the complete 3-step Checkout flow including form validation (FR-022 to FR-025), financial calculation accuracy — Item Total, Tax (8%), and Grand Total (FR-026 to FR-030) — and Order Confirmation (FR-031 to FR-032).

- Confirm Navigation and Hamburger Menu functions correctly including Logout session invalidation and Reset App State per FR-033 to FR-036.

### 2.2 Non-Functional Objectives

- **Performance:** Verify page load times meet defined thresholds (Login < 2s, Inventory < 3s, Cart updates < 1s) per NFR-P01 to NFR-P06.

- **Security:** Ensure authentication is required for all pages, session is invalidated on logout, and no sensitive data is exposed in URLs per NFR-S01 to NFR-S04.

- **Compatibility:** Confirm the application functions correctly across Chrome 120+, Firefox 120+, and Edge 120+ per NFR-C01 to NFR-C02.

- **Usability:** Validate that error messages are clear, UI feedback is immediate, and cart state persists across navigation per NFR-U01 to NFR-U06.

- **Reliability:** Confirm data consistency between pages, calculation accuracy is 100%, and error messages are consistent per NFR-R01 to NFR-R04.

---

## 3. SCOPE

### 3.1 In Scope

The following modules and test types are included in this test effort, with minimum and target test case counts derived from the RAD Section 6.1:

| **Module** | **Test Types** | **Focus Area** | **Min TC** | **Target TC** | **Priority** |
|---|---|---|---|---|---|
| Login | Functional, Negative, Boundary | 6 account types, form validation, error messages | 12 | 15 | P1 — Critical |
| Inventory | Functional, UI Verification | 6 products, 4 sort options, Add/Remove, badge count | 10 | 15 | P1 — Critical |
| Product Detail | Functional, Navigation | Product info display, Add to Cart, Back nav | 5 | 8 | P2 — High |
| Shopping Cart | Functional, State Management | Display, Remove, Continue Shopping, Checkout | 8 | 12 | P1 — Critical |
| Checkout | Functional, Negative, Calculation | 3-step flow, validation, price calc, E2E | 15 | 20 | P1 — Critical |
| Navigation | Functional | Hamburger menu, Logout, Reset State | 5 | 8 | P2 — High |
| Cross-browser | Compatibility | Chrome, Firefox, Edge — main flows | 5 | 10 | P3 — Medium |
| E2E Flow | Integration | Happy path end-to-end per user account type | 3 | 5 | P2 — High |
| **TOTAL** | | | **63** | **93** | |

### 3.2 Out of Scope

The following areas are explicitly excluded from this test effort:

| **Item** | **Reason** | **Note** |
|---|---|---|
| Automation Testing (Selenium/Cypress/Playwright) | This is a Manual Testing project | Can be added as a separate portfolio project |
| Performance / Load Testing | Requires specialized tools (JMeter, k6) | Log observations in Bug Report if slowness detected |
| Security / Penetration Testing | Outside manual testing scope | Basic security tested per NFR-S requirements only |
| API Testing (Postman) | Not within Manual UI Testing scope | Can supplement for portfolio value |
| Mobile Responsive Testing | Application not optimized for mobile | Note any issues discovered incidentally |
| Database Testing | No database access available | N/A for demo application |
| Payment Gateway Integration | Demo application — no real payment | N/A — simulated checkout only |

---

## 4. TEST STRATEGY

The test strategy is risk-based, derived from the Risk Analysis in RAD Section 6.3. Testing effort is proportional to the business impact and probability of failure of each component.

### 4.1 Risk-Based Test Priority

| **Risk Area** | **Risk Level** | **Priority** | **Business Impact** | **Mitigation Strategy** |
|---|---|---|---|---|
| **Checkout Flow** | **Critical** | **P1** | Calculation errors cause financial losses | Test all price combinations first; verify 8% tax formula across all cart combinations |
| **Login Authentication** | **Critical** | **P1** | Auth failure blocks entire system | Test all 6 account types before any other module; prioritize FR-001 and FR-005 |
| **Cart State Management** | **High** | **P2** | Data loss causes cart abandonment | Verify cart persistence across all navigation paths; test Add/Remove consistency |
| **Problem_user Bugs** | **High** | **P2** | Multiple injected bugs need cataloging | Dedicate separate test pass with problem_user to document all intentional defects |
| **Sort Functionality** | **Medium** | **P3** | Incorrect sort causes UX confusion | Validate all 4 sort options with boundary values and specific expected sequences |
| **Navigation / Logout** | **Medium** | **P3** | Logout failure = session security risk | Verify session invalidation with browser back button after logout |

### 4.2 Test Approach

- **Black-box testing** is the primary approach — test cases are derived from requirements and expected behavior, not source code.

- **Equivalence Partitioning** and **Boundary Value Analysis** applied to login fields, checkout form fields, and price calculations.

- **State Transition Testing** applied to cart management (Add/Remove/Reset) and user session (Login/Logout).

- **Error Guessing** applied to known problematic areas: problem_user account, empty cart checkout, and direct URL access.

- **Exploratory Testing** reserved for visual_user and problem_user accounts to catalog intentional UI defects.

---

## 5. TEST LEVELS

| **Level** | **Scope** | **Description** | **Responsible** |
|---|---|---|---|
| **Component Testing** | Individual modules | Login form validation, Sort dropdown, Cart badge count — each function tested independently | QA Tester |
| **Integration Testing** | Module interactions | Cart state between Inventory → Cart → Checkout pages; Add to Cart from Product Detail syncs with Inventory badge | QA Tester |
| **System Testing** | End-to-end system | Full purchase flow: Login → Browse → Add to Cart → Checkout → Order Completion; all user account types | QA Lead |
| **Acceptance Testing** | Business requirements validation | Verify all 36 FRs and 24 NFRs are met; all Critical and High priority requirements pass acceptance criteria | QA Lead / PM |

---

## 6. TEST TYPES

| **Test Type** | **Priority** | **Coverage** | **Test Basis** |
|---|---|---|---|
| **Functional Testing** | **Critical** | All 36 FRs across 6 modules | FR-001 to FR-036 in RAD Section 4 |
| **Negative Testing** | **Critical** | All 8 Exception Flows + form validation | EF-01 to EF-08, FR-002 to FR-005, FR-022 to FR-024 |
| **Boundary Value Analysis** | **High** | Login fields, form inputs, price calc | NFR-R02, FR-022 to FR-024 — empty/space/special chars |
| **User Account Testing** | **High** | All 6 account types with distinct behaviors | RAD Section 1.3 — 6 test accounts |
| **Regression Testing** | **High** | Core flows after bug fixes | Happy Path, Cart State, Auth flows |
| **Compatibility Testing** | **Medium** | Chrome, Firefox, Edge — critical flows only | NFR-C01, NFR-C02 |
| **Performance Observation** | **Medium** | Load times — standard vs glitch user | NFR-P01 to NFR-P06 |
| **Security Testing (Basic)** | **Medium** | Auth required, session management, URL | NFR-S01 to NFR-S04 |
| **Visual / UI Testing** | **Medium** | Layout, consistent UI, visual_user account | NFR-U03, visual_user account characteristics |
| **Exploratory Testing** | **Low** | problem_user and visual_user edge cases | RAD Section 6.3 — intentional bugs cataloging |

---

## 7. ENTRY CRITERIA

The following conditions must be met before test execution begins. Entry Criteria are derived from Critical and High priority requirements in the RAD.

### 7.1 Environment & Access

- The application at https://www.saucedemo.com is accessible and responsive.

- All 6 test accounts (standard_user, locked_out_user, problem_user, performance_glitch_user, error_user, visual_user) with password `secret_sauce` are verified as functional.

- Test environment (browsers: Chrome 120+, Firefox 120+, Edge 120+) is configured and available.

### 7.2 Documentation & Preparation

- RAD (SWG-RA-2026) has been reviewed, approved, and signed off.

- This Test Plan (SWG-TP-2026) is reviewed and approved by QA Lead.

- Test Case document template is ready and test cases for Critical priority modules (Login, Cart, Checkout) are completed.

- Bug Report template and tracking system (GitHub Issues / Jira / Notion) is set up.

### 7.3 Baseline

- Smoke test of the Happy Path (Login → Add to Cart → Checkout Complete) passes successfully with standard_user.

- Minimum 63 test cases drafted and reviewed before execution begins.

---

## 8. EXIT CRITERIA

Testing is considered complete when the following conditions are satisfied:

### 8.1 Test Execution

- 100% of planned test cases (minimum 63, target 93) have been executed at least once.

- All Critical priority test cases (Login, Cart, Checkout — minimum 35 TCs) show **PASS** status.

- Overall test case pass rate is **≥ 95%** across all modules.

### 8.2 Defect Criteria

- **Zero (0)** open Critical severity bugs remain unresolved or unacknowledged.

- **Zero (0)** open High severity bugs in the core purchase flow (Login → Add to Cart → Checkout Complete).

- All intentional bugs in problem_user and visual_user accounts are documented in Bug Report with correct severity classification.

- All open defects are triaged with severity, priority, and reproduction steps documented.

### 8.3 Coverage

- All 36 Functional Requirements (FR-001 to FR-036) are covered by at least one test case.

- All 8 Exception Flows (EF-01 to EF-08) are verified.

- All 6 test account types have been exercised through the Happy Path at minimum.

- Compatibility testing completed on Chrome, Firefox, and Edge.

### 8.4 Documentation

- Test Summary Report is drafted and approved.

- All Bug Reports are complete with steps to reproduce, severity, expected vs. actual results, and screenshots.

---

## 9. TEST ENVIRONMENT

| **Category** | **Component** | **Details / Version** |
|---|---|---|
| **Application** | URL | https://www.saucedemo.com |
| **Application** | Type | Single Page Application (React) — Production Live Demo |
| **Browser** | Chrome | Version 120+ (Primary Browser — All test types) |
| **Browser** | Firefox | Version 120+ (Compatibility Testing — Core flows) |
| **Browser** | Edge | Version 120+ (Compatibility Testing — Core flows) |
| **Browser** | Safari | Best effort only — not primary test target |
| **Operating System** | Windows | Windows 10 / Windows 11 |
| **Operating System** | macOS | Ventura / Sonoma (if available) |
| **Screen Resolution** | Primary | 1920×1080 (Full HD) |
| **Screen Resolution** | Secondary | 1366×768 (minimum supported) |
| **Network** | Connection | Standard broadband connection for standard_user tests |
| **Test Data** | Accounts | 6 test accounts — see RAD Section 1.3 |
| **Test Data** | Products | 6 products ranging $7.99 to $49.99 — fixed dataset |
| **Bug Tracking** | Tool | GitHub Issues / Notion / Excel (per team preference) |
| **Screenshots** | Tool | Browser built-in screenshot or LightShot / Snipping Tool |

---

## 10. DELIVERABLES

| **#** | **Deliverable** | **Document ID** | **Timing** | **Description** |
|---|---|---|---|---|
| **1** | **Requirements Analysis Document (RAD)** | SWG-RA-2026 | Before Testing — DONE | System requirements, user flows, acceptance criteria — source document for this Test Plan |
| **2** | **Test Plan (this document)** | SWG-TP-2026 | Before Testing — DONE | Test strategy, scope, criteria, schedule, and resources |
| **3** | **Test Scenario Document** | SWG-TS-2026 | Before Execution | High-level test scenarios mapped from FR/NFR, organized by module |
| **4** | **Test Case Document** | SWG-TC-2026 | Before Execution | Detailed test cases with steps, test data, expected results (min 63, target 93 TCs) |
| **5** | **Bug Report Log** | SWG-BR-2026 | During Execution | All defects found with ID, severity, priority, steps to reproduce, screenshots |
| **6** | **Test Execution Report** | SWG-ER-2026 | During / After Execution | Daily pass/fail counts, blocked items, execution progress |
| **7** | **Test Summary Report** | SWG-SR-2026 | After Execution | Overall quality assessment, coverage, open defects, go/no-go recommendation |

---

## 11. RISKS AND MITIGATION

| **#** | **Risk Description** | **Likelihood** | **Impact** | **Mitigation Strategy** |
|---|---|---|---|---|
| **1** | Demo application URL becomes unavailable or inaccessible during testing period | Low | Critical | Verify site accessibility before each test session; schedule testing during business hours; have backup screenshots of UI |
| **2** | Intentional bugs in problem_user confuse testers into logging false positives | High | Medium | Pre-brief all testers on the 6 account types and their characteristics; document expected behavior per account type |
| **3** | Financial calculation verification error — wrong expected values calculated by tester | Medium | High | Provide calculation reference table ($29.99+$9.99=$39.98; 8% tax=$3.20; Total=$43.18) in test case document |
| **4** | Browser version updates break compatibility assumptions during test period | Low | Medium | Lock browser versions at test start; document exact versions used in environment setup |
| **5** | Test cases cover only happy path, missing critical negative and boundary scenarios | Medium | High | Mandate test case review checkpoint; require minimum negative/boundary ratio of 30% total test cases |
| **6** | Testing time overrun due to underestimated exploratory work on problem_user bugs | Medium | Medium | Time-box exploratory testing to max 20% of total effort; document findings in a separate bug catalog |
| **7** | Tester unfamiliar with e-commerce domain misses business logic errors in checkout calculations | Low | High | Include business context briefing; provide worked examples of all calculation scenarios in test data document |
| **8** | Single tester introduces bias — may miss bugs consistent with their own mental model of the system | Medium | Medium | Arrange peer review of at least P1/P2 test cases; consider pair testing for Checkout module |

---

## 12. SCHEDULE

Estimated schedule based on 93 target test cases across 6 modules. Timeline assumes 1 QA Tester working approximately 4 hours/day on this project. Adjust based on actual team availability.

| **#** | **Phase** | **Activities** | **Duration** | **Effort** | **Deliverable** |
|---|---|---|---|---|---|
| **1** | Planning & Review | Read RAD, review scope, set up environment, configure browser versions, verify test accounts | 1 day | 4h | SWG-TP-2026 (this document) |
| **2** | Test Design — Critical | Write Test Scenarios & Test Cases for Login, Inventory, Cart, Checkout (P1 modules — 47 TCs) | 3 days | 12h | SWG-TC-2026 (partial) |
| **3** | Test Design — All | Write Test Cases for Product Detail, Navigation, Cross-browser, E2E (remaining 46 TCs) | 2 days | 8h | SWG-TC-2026 (complete) |
| **4** | Test Case Review | Peer review of all test cases; update based on feedback; finalize test data | 1 day | 4h | Reviewed & signed-off TC |
| **5** | Execution — P1 Modules | Execute Login, Cart, Checkout test cases; log defects; retest fixed bugs | 3 days | 12h | SWG-BR-2026, SWG-ER-2026 |
| **6** | Execution — P2/P3 | Execute Inventory, Product Detail, Navigation, E2E, Cross-browser test cases | 3 days | 12h | SWG-BR-2026 (continued) |
| **7** | Exploratory Testing | Time-boxed exploration with problem_user & visual_user; catalog intentional bugs | 1 day | 4h | Bug Catalog (appended to BR) |
| **8** | Regression Testing | Re-execute Critical test cases after any environment changes or bug fixes | 1 day | 4h | Updated SWG-ER-2026 |
| **9** | Test Closure | Compile Test Summary Report; review exit criteria; obtain sign-off | 1 day | 4h | SWG-SR-2026 |
| **TOTAL** | | | **16 days** | **64h** | Complete Test Artifacts |

---

## 13. RESOURCE PLANNING

### 13.1 Human Resources

| **Role** | **Count** | **Responsibility** | **Required Skills** |
|---|---|---|---|
| **QA Tester (Manual)** | 1 | Test case design, execution, bug reporting, test summary | Manual testing fundamentals, ISTQB foundation, browser DevTools, bug reporting tools |
| **QA Lead / Reviewer** | 1 (part) | Review test plan & cases, triage defects, approve exit criteria | ISTQB intermediate, e-commerce domain knowledge, defect management |
| **Project Manager** | 1 (part) | Schedule coordination, stakeholder updates, final sign-off | Project coordination, risk assessment |

### 13.2 Tool Resources

| **Category** | **Tool** | **License** | **Purpose** |
|---|---|---|---|
| **Browser** | Chrome 120+ | Free | Primary test browser — all test types |
| **Browser** | Firefox 120+ | Free | Compatibility testing |
| **Browser** | Microsoft Edge 120+ | Free | Compatibility testing |
| **Test Design** | Excel / Google Sheets | Free | Test case documentation and tracking |
| **Bug Tracking** | GitHub Issues | Free (public repo) | Bug logging and portfolio visibility — recommended for GitHub portfolio |
| **Bug Tracking** | Notion / Jira | Free / Paid | Alternative bug tracking if GitHub Issues not preferred |
| **Screenshots** | Snipping Tool / LightShot | Free | Evidence capture for bug reports |
| **Documentation** | Google Docs / Word | Free / Paid | Test plan, scenarios, and summary report |
| **Mind Mapping** | XMind / Miro | Free tier | Test coverage mapping and scenario visualization (optional) |

### 13.3 GitHub Portfolio Recommendations

For maximum portfolio impact on GitHub, organize the project repository as follows:

- **Repository name:** `saucedemo-manual-testing-portfolio`
- **README.md:** Project overview, tech stack used, test artifacts list, and key findings summary
- **Folder `/docs`:** RAD, Test Plan (this document), Test Scenarios, Test Cases
- **Folder `/bug-reports`:** Individual bug report files or consolidated Bug Report Log
- **Folder `/test-execution`:** Execution report with pass/fail evidence
- Use **GitHub Issues** for live bug tracking with labels: `Critical`, `High`, `Medium`, `Low`
- Add **GitHub Project Board** (Kanban) to track test execution progress visually

---

## 14. APPROVAL & SIGN-OFF

| **Role** | **Name** | **Signature** | **Date** |
|---|---|---|---|
| **QA Tester** | _____________________ | _____________________ | _____ / _____ / 2026 |
| **QA Lead / Reviewer** | _____________________ | _____________________ | _____ / _____ / 2026 |
| **Project Manager** | _____________________ | _____________________ | _____ / _____ / 2026 |

---

