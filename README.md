# 🧪 SauceDemo Manual Testing Portfolio

> **Manual Functional Testing** project for [Swag Labs](https://www.saucedemo.com) — a demo e-commerce application by Sauce Labs.  
> This project demonstrates end-to-end QA skills including test planning, test design, execution, and bug reporting.

---

## 📋 Project Overview

| Field | Detail |
|---|---|
| **Website Under Test** | https://www.saucedemo.com |
| **Application Type** | Single Page Application (SPA) — React |
| **Testing Type** | Manual Functional Testing |
| **Tester** | Nguyễn Long Vũ |
| **Test Period** | 02/06/2026 — 09/06/2026 |
| **Environment** | Chrome 124 / Windows 11 / 1920×1080 |

---

## 📊 Test Results Summary

| Metric | Result |
|---|---|
| **Total Test Cases** | 66 |
| **Passed** | 65 |
| **Failed** | 1 |
| **Pass Rate** | 98.5% |
| **Bugs Found** | 1 confirmed bug |
| **Overall Status** | ✅ PASSED with 1 minor defect |

### Results by Module

| Module | Total TC | Pass | Fail | Pass Rate |
|---|---|---|---|---|
| 🔐 Login | 13 | 12 | 1 | 92.3% |
| 📦 Product List | 13 | 13 | 0 | 100% |
| 🔍 Product Detail | 8 | 8 | 0 | 100% |
| 🛒 Shopping Cart | 10 | 10 | 0 | 100% |
| 💳 Checkout | 16 | 16 | 0 | 100% |
| 🚪 Logout & Navigation | 6 | 6 | 0 | 100% |
| **TOTAL** | **66** | **65** | **1** | **98.5%** |

---

## 🐛 Bugs Found

### Confirmed Bug — Requires Fix

| Field | Detail |
|---|---|
| **Bug ID** | BUG-001 |
| **Title** | Unauthenticated user can access `/inventory.html` directly without login |
| **Severity** | High |
| **Status** | Open |
| **TC Reference** | TC_012 |
| **GitHub Issue** | [Issue #2](https://github.com/zues5sne/saucedemo-manual-testing/issues/2) |

**Steps to Reproduce:**
1. Open browser — do NOT login
2. Navigate directly to `https://www.saucedemo.com/inventory.html`
3. Page loads successfully without any authentication

**Expected:** Redirect to Login page  
**Actual:** Inventory page accessible without login ❌

---

## 📁 Repository Structure

```
saucedemo-manual-testing/
│
├── README.md                         ← You are here
│
├── docs/
│   ├── RAD.md                        ← Requirement Analysis Document
│   ├── TEST_PLAN.md                  ← Test Plan (ISTQB standard)
│   └── TEST_SCENARIO.md              ← 66 Test Scenarios across 6 modules
│
├── test-cases/
│   └── [Google Sheets — link below]  ← 66 Test Cases with Execution Results
│
├── bug-reports/
│   └── BUG-001.md                    ← Detailed bug report with steps
│
└── test-summary/
    └── TEST_SUMMARY_REPORT.md        ← Final test summary and recommendations
```

---

## 📄 Documents

| Document | Description | Link |
|---|---|---|
| 📋 Requirement Analysis (RAD) | System analysis, 36 FR, 24 NFR, User Flow | [View](./docs/RAD.md) |
| 📝 Test Plan | ISTQB standard — Scope, Strategy, Risks, Schedule | [View](./docs/TEST_PLAN.md) |
| 🗂️ Test Scenario | 66 scenarios across 6 modules | [View](./docs/TEST_SCENARIO.md) |
| ✅ Test Cases | 66 TC with Steps, Expected & Actual Result, Status | https://docs.google.com/spreadsheets/d/1GUGHixPVe79Ps2o31WBmLK5bxv0GZFHXjZ4ORwXpC8I/edit?usp=sharing |
| 🐛 Bug Report | BUG-001 detailed report | [View](./bug-reports/BUG-001.md) |
| 📊 Test Summary | Final results, metrics, recommendations | [View](./test-summary/TEST_SUMMARY_REPORT.md) |

---

## 🔍 Modules Tested

### 1. 🔐 Login
- Valid login with 6 different test accounts
- Invalid credentials — error message validation
- Locked account handling
- Password masking
- Direct URL access (security check)

### 2. 📦 Product List (Inventory)
- 6 products display correctly
- 4 sort options: Name A-Z, Z-A, Price Low-High, High-Low
- Add to Cart / Remove from Cart
- Cart badge count accuracy

### 3. 🔍 Product Detail
- Navigation from Inventory to Detail page
- All product information displayed correctly
- Add to Cart from Detail page
- Back navigation — cart state preserved

### 4. 🛒 Shopping Cart
- Products display correctly with Qty, name, price
- Remove individual and all items
- Continue Shopping — cart preserved
- Checkout navigation

### 5. 💳 Checkout (3 Steps)
- **Step 1:** Form validation (First Name, Last Name, Postal Code)
- **Step 2:** Order Overview — pricing formula verified
  - Item Total = sum of all products
  - Tax = Item Total × 8%
  - Grand Total = Item Total + Tax
- **Step 3:** Order Confirmation page
- Full E2E Happy Path (TC_059)
- Pricing verified with 3 product combinations (TC_060)

### 6. 🚪 Logout & Navigation
- Hamburger menu open/close
- Logout — session invalidated
- Browser Back button blocked after logout
- Reset App State
- External links

---

## 🧪 Test Accounts Used

| Username | Type | Purpose |
|---|---|---|
| `standard_user` | Normal | Happy path & baseline testing |
| `locked_out_user` | Locked | Error handling testing |
| `problem_user` | Buggy UI | Visual & functional bug detection |
| `performance_glitch_user` | Slow | Performance observation |
| `error_user` | Form errors | Checkout error testing |
| `visual_user` | CSS broken | Visual regression testing |

**Password for all accounts:** `secret_sauce`

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Google Chrome 124 | Primary test browser |
| Firefox / Edge | Cross-browser testing |
| Google Sheets | Test Case management & execution |
| GitHub Issues | Bug tracking |
| Snipping Tool | Screenshot evidence |
| Browser DevTools | Performance observation |

---

## 🔑 Key Findings

### ✅ What Works Well
- Full E2E Happy Path completes without issues — Login → Browse → Cart → Checkout → Confirmation
- All 4 sort options return correct product order
- Cart state synchronized consistently across all pages
- Pricing formula (Item Total + 8% Tax = Grand Total) is 100% accurate
- Session properly invalidated on Logout

### ⚠️ Issues Found
- **Security Bug (High):** Unauthenticated access to `/inventory.html` — no redirect to Login
- Intentional bugs confirmed in `problem_user` (images, Add to Cart), `error_user` (form actions), `performance_glitch_user` (load time ~5s)

### 💡 Personal Notes
During testing, I discovered that:
- **TC_012** required 2 re-runs before confirming it was a real bug, not a test mistake
- **TC_050** — initially wrote incorrect Expected Result (`/inventory.html`); corrected to `/cart.html` after actual testing
- **TC_043** — expected `problem_user` Cart to fail, but it worked normally; bugs were in Inventory & Product Detail instead
- **TC_058** — found 3 specific bugs with `error_user`: Last Name input redirects to Zip field, validation bypass, and Finish button unresponsive

---

## 📈 Exit Criteria Status

| Criterion | Status |
|---|---|
| 100% TC Executed | ✅ 66/66 |
| Pass Rate ≥ 95% | ✅ 98.5% |
| 0 Blocker/Critical bugs | ✅ Met |
| All 36 FR covered | ✅ 36/36 |
| E2E Happy Path passes | ✅ TC_059 PASS |
| Pricing formula verified | ✅ 3 combos verified |
| All bugs logged | ✅ BUG-001 on GitHub Issues |
| Test Summary completed | ✅ Done |

---

## 📌 How to Review This Portfolio

1. Start with **[RAD](./docs/RAD.md)** to understand the system
2. Review **[Test Plan](./docs/TEST_PLAN.md)** for testing strategy
3. Check **[Test Scenarios](./docs/TEST_SCENARIO.md)** for coverage overview
4. Open **[Test Cases (Google Sheets)]([<!-- -->](https://docs.google.com/spreadsheets/d/1GUGHixPVe79Ps2o31WBmLK5bxv0GZFHXjZ4ORwXpC8I/edit?usp=sharing))** to see detailed execution
5. Review **[BUG-001](./bug-reports/BUG-001.md)** for the confirmed defect
6. Read **[Test Summary](./test-summary/TEST_SUMMARY_REPORT.md)** for final conclusions

---

*Manual Testing Portfolio — Nguyễn Long Vũ — 2026*  
*Swag Labs | saucedemo.com | ISTQB Foundation Level approach*
