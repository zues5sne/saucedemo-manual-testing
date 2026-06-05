# TEST SCENARIO DOCUMENT

**Test Scenario Document**

---

**SWAG LABS**
https://www.saucedemo.com

| **Document ID** | SWG-TS-2026 |
|---|---|
| **Version** | 1.0 |
| **Date Created** | 02/06/2026 |
| **RAD Reference** | SWG-RA-2026 — Requirement Analysis Document |
| **Test Plan Reference** | SWG-TP-2026 — Test Plan (ISTQB) |
| **Author** | [Your Name] — QA Tester |
| **Status** | ✅ Ready for Test Case authoring |

---

## Document Reading Guide

This Test Scenario document is constructed from 2 primary sources:

- **RAD SWG-RA-2026** — Chapter 3 (User Flow), Chapter 4 (36 FRs), Chapter 5 (24 NFRs)
- **Test Plan SWG-TP-2026** — Section 4.1 (Risk-Based Priority) used to determine scenario priorities

| **Concept** | **Definition** | **Example** |
|---|---|---|
| **Positive Scenario** | User performs correct action → system responds correctly | Login with standard_user/secret_sauce succeeds |
| **Negative Scenario** | User performs incorrect action → system handles error correctly | Login with wrong password → displays error message |
| **Priority High** | Critical modules in Test Plan — tested first | Login, Cart, Checkout — block entire flow if failing |
| **Priority Medium** | High modules in Test Plan — tested after Critical | Inventory, Product Detail, E2E flow |
| **Priority Low** | Medium modules in Test Plan — tested last | Navigation, menu links, non-critical UI |

---

## Test Scenario Summary

A total of **56 Test Scenarios** covering 6 modules, mapped directly from 36 FRs and 8 Exception Flows in the RAD.

| **Module** | **Total** | **Positive** | **Negative** | **High** | **Medium** | **FR Source** |
|---|---|---|---|---|---|---|
| **🔐 Login** | **13** | **6** | **7** | **13** | **0** | *FR-001~006, EF-01~04* |
| **📦 Product List** | **10** | **7** | **3** | **0** | **10** | *FR-007~014* |
| **🔍 Product Detail** | **7** | **5** | **2** | **0** | **7** | *FR-015~017* |
| **🛒 Cart** | **9** | **5** | **4** | **9** | **0** | *FR-018~021, EF-05* |
| **💳 Checkout** | **12** | **5** | **7** | **12** | **0** | *FR-022~032, EF-06~08* |
| **🚪 Logout & Nav** | **5** | **3** | **2** | **0** | **3** | *FR-033~036* |
| **TOTAL** | **56** | **31** | **25** | **34** | **20** | 36 FR + 8 EF |

---

## 🔐 MODULE 1 — LOGIN

*FR-001 → FR-006 │ EF-01 → EF-04 │ Priority: Critical (P1)*

**RAD Source:** FR-001 (Valid login), FR-002 (Wrong password), FR-003 (Blank username), FR-004 (Blank password), FR-005 (Locked account), FR-006 (Logout) + EF-01~04 + NFR-S01 (Auth required), NFR-S02 (Password masking).

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **13** | **6** | **7** | **13** | **0** | **0** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_001** | Login | Verify successful login with standard_user account and valid password | Positive | High |
| **TS_002** | Login | Verify that after successful login, the system redirects correctly to /inventory.html | Positive | High |
| **TS_003** | Login | Verify login failure when incorrect password is entered; system displays appropriate error message | Negative | High |
| **TS_004** | Login | Verify login failure when the Username field is left blank | Negative | High |
| **TS_005** | Login | Verify login failure when the Password field is left blank | Negative | High |
| **TS_006** | Login | Verify login failure when both Username and Password fields are left blank | Negative | High |
| **TS_007** | Login | Verify the system rejects login for a locked account (locked_out_user) and displays a clear notification | Negative | High |
| **TS_008** | Login | Verify error message displays with correct content, correct position, and can be dismissed via the X button | Negative | High |
| **TS_009** | Login | Verify the Password field always displays masked characters (•••) and never reveals plaintext | Positive | High |
| **TS_010** | Login | Verify login with problem_user succeeds but the Inventory page contains intentional bugs | Positive | High |
| **TS_011** | Login | Verify login with performance_glitch_user succeeds but exhibits abnormally slow load times | Positive | High |
| **TS_012** | Login | Verify that direct access to /inventory.html without prior authentication redirects to the Login page | Negative | High |
| **TS_013** | Login | Verify login with a username containing special characters or whitespace displays an appropriate error | Negative | High |

---

## 📦 MODULE 2 — PRODUCT LIST (INVENTORY)

*FR-007 → FR-014 │ NFR-P01, NFR-U02 │ Priority: High (P2)*

**RAD Source:** FR-007 (Display products), FR-008~011 (4 Sort options), FR-012~013 (Add/Remove), FR-014 (Badge) + NFR-P01 (Load < 3s), NFR-U02 (Visual feedback).

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **13** | **10** | **3** | **0** | **13** | **0** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_014** | Product List | Verify the Inventory page displays exactly 6 products after successful login | Positive | Medium |
| **TS_015** | Product List | Verify each product displays all 4 components: image, name, description, and price | Positive | Medium |
| **TS_016** | Product List | Verify product sorting by Name A → Z (default order on page load) | Positive | Medium |
| **TS_017** | Product List | Verify product sorting by Name Z → A produces the correct reverse order | Positive | Medium |
| **TS_018** | Product List | Verify product sorting by Price: Low to High — $7.99 appears first | Positive | Medium |
| **TS_019** | Product List | Verify product sorting by Price: High to Low — $49.99 appears first | Positive | Medium |
| **TS_020** | Product List | Verify 'Add to cart' button functions correctly — product is added to Cart, button changes to 'Remove' | Positive | Medium |
| **TS_021** | Product List | Verify 'Remove' button functions correctly — product is removed from Cart, button reverts to 'Add to cart' | Positive | Medium |
| **TS_022** | Product List | Verify cart badge count updates accurately when multiple products are added and removed | Positive | Medium |
| **TS_023** | Product List | Verify with problem_user — product images display incorrectly (intentional bug) are detected and documented | Negative | Medium |
| **TS_024** | Product List | Verify with problem_user — 'Add to cart' button does not function for some products (intentional bug) | Negative | Medium |
| **TS_025** | Product List | Verify with performance_glitch_user — Inventory page load time exceeds the 3-second threshold (NFR-P01) | Negative | Medium |
| **TS_026** | Product List | Verify sort dropdown displays all 4 options correctly and retains selection after sorting | Positive | Medium |

---

## 🔍 MODULE 3 — PRODUCT DETAIL

*FR-015 → FR-017 │ NFR-R01 (Data Consistency) │ Priority: High (P2)*

**RAD Source:** FR-015 (View product details), FR-016 (Add to Cart from Detail), FR-017 (Back navigation) + NFR-R01 (Data Consistency), NFR-U06 (Cart State Persistence).

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **8** | **7** | **1** | **0** | **8** | **0** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_027** | Product Detail | Verify clicking a product name from Inventory navigates to the correct product's detail page | Positive | Medium |
| **TS_028** | Product Detail | Verify clicking a product image from Inventory also navigates to the correct detail page | Positive | Medium |
| **TS_029** | Product Detail | Verify the Product Detail page displays all required elements: image, name, description, price, and Add to cart button | Positive | Medium |
| **TS_030** | Product Detail | Verify 'Add to cart' button on the Detail page functions correctly and cart badge increments by 1 | Positive | Medium |
| **TS_031** | Product Detail | Verify 'Back to products' button returns the user to the correct Inventory page | Positive | Medium |
| **TS_032** | Product Detail | Verify Cart state is preserved when navigating Inventory → Detail → Back to Inventory | Positive | Medium |
| **TS_033** | Product Detail | Verify with problem_user — Detail page displays incorrect product information (intentional bug) | Negative | Medium |
| **TS_034** | Product Detail | Verify URL contains the correct product ID when accessing different products | Positive | Medium |

---

## 🛒 MODULE 4 — SHOPPING CART

*FR-018 → FR-021 │ NFR-R03 (State Management) │ Priority: Critical (P1)*

**RAD Source:** FR-018 (Display Cart), FR-019 (Remove), FR-020 (Continue Shopping), FR-021 (Checkout button) + NFR-R03 (Cart State consistency), NFR-U06 (Cart Persistence).

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **10** | **7** | **3** | **10** | **0** | **0** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_035** | Cart | Verify the Cart page displays all added products correctly with Qty, name, description, and price | Positive | High |
| **TS_036** | Cart | Verify the Cart page displays an empty state when no products have been added | Positive | High |
| **TS_037** | Cart | Verify the 'Remove' button in Cart removes the correct product and cart badge decrements accurately | Positive | High |
| **TS_038** | Cart | Verify removing all products from Cart — Cart page returns to empty state, badge disappears | Positive | High |
| **TS_039** | Cart | Verify 'Continue Shopping' button returns user to Inventory page with Cart state preserved | Positive | High |
| **TS_040** | Cart | Verify 'Checkout' button navigates to Checkout Step 1 when Cart contains at least 1 product | Positive | High |
| **TS_041** | Cart | Verify products added from both Inventory and Product Detail pages appear correctly in Cart | Positive | High |
| **TS_042** | Cart | Verify Cart state is consistently synchronized between the Cart page and the badge across all pages | Negative | High |
| **TS_043** | Cart | Verify with problem_user — Remove button or Cart display may malfunction (intentional bug) | Negative | High |
| **TS_044** | Cart | Verify Checkout with an empty Cart is still permitted (edge case) | Negative | High |

---

## 💳 MODULE 5 — CHECKOUT

*FR-022 → FR-032 │ NFR-R02 (Calculation) │ Priority: Critical (P1)*

**RAD Source:** FR-022~024 (Validation), FR-025 (Proceed to Step 2), FR-026~030 (Overview + Pricing), FR-031~032 (Completion) + NFR-R02 (100% calculation accuracy), EF-06~08.

> ⚠️ **Pricing Formula Reference:**

| **Item Total** | **Tax (8%)** | **Grand Total** |
|---|---|---|
| = Sum of all product prices in Cart | = Item Total × 0.08 | = Item Total + Tax |
| *e.g.: $29.99 + $9.99 = $39.98* | *e.g.: $39.98 × 8% = $3.20* | *e.g.: $39.98 + $3.20 = $43.18* |

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **16** | **9** | **7** | **16** | **0** | **0** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_045** | Checkout | Verify Checkout Step 1 — filling in valid First Name, Last Name, Postal Code and successfully proceeding to Step 2 | Positive | High |
| **TS_046** | Checkout | Verify Checkout Step 1 — validation error when First Name is left blank | Negative | High |
| **TS_047** | Checkout | Verify Checkout Step 1 — validation error when Last Name is left blank | Negative | High |
| **TS_048** | Checkout | Verify Checkout Step 1 — validation error when Postal Code is left blank | Negative | High |
| **TS_049** | Checkout | Verify Checkout Step 1 — validation error when all 3 fields are simultaneously left blank | Negative | High |
| **TS_050** | Checkout | Verify Checkout Step 1 — Cancel button returns user to Inventory with Cart state preserved | Positive | High |
| **TS_051** | Checkout | Verify Checkout Step 2 — Overview page displays all Cart products correctly | Positive | High |
| **TS_052** | Checkout | Verify Checkout Step 2 — Item Total equals the sum of all product prices (calculated accurately) | Positive | High |
| **TS_053** | Checkout | Verify Checkout Step 2 — Tax equals 8% of Item Total (calculated accurately with correct rounding) | Positive | High |
| **TS_054** | Checkout | Verify Checkout Step 2 — Grand Total equals Item Total + Tax (formula correct for all product combinations) | Positive | High |
| **TS_055** | Checkout | Verify Checkout Step 2 — Cancel button returns to Inventory with Cart state preserved | Negative | High |
| **TS_056** | Checkout | Verify Checkout Complete — confirmation page displays correctly: ✓ icon, 'Thank you for your order!', Back Home button | Positive | High |
| **TS_057** | Checkout | Verify Checkout Complete — Back Home button returns to Inventory and Cart has been reset to empty | Positive | High |
| **TS_058** | Checkout | Verify with error_user — certain Checkout steps fail due to form action errors (intentional bug) | Negative | High |
| **TS_059** | Checkout | Verify full E2E flow: Login → Add 2 products → Cart → 3-step Checkout → Confirmation → Back Home | Positive | High |
| **TS_060** | Checkout | Verify pricing calculations with multiple different product combinations to ensure formula accuracy | Negative | High |

---

## 🚪 MODULE 6 — LOGOUT & NAVIGATION

*FR-033 → FR-036 │ NFR-S03 (Session Invalidation) │ Priority: Medium (P3)*

**RAD Source:** FR-033 (Hamburger menu), FR-034 (All Items), FR-035 (About), FR-036 (Reset App State), FR-006 (Logout) + NFR-S03 (Session Invalidation on Logout).

| **Total** | **Positive** | **Negative** | **High** | **Medium** | **Low** |
|---|---|---|---|---|---|
| **6** | **4** | **2** | **0** | **2** | **4** |

| **ID** | **Module** | **Scenario Description** | **Type** | **Priority** |
|---|---|---|---|---|
| **TS_061** | Logout & Nav | Verify Hamburger menu opens correctly when the 3-line icon is clicked and closes when X is clicked | Positive | Low |
| **TS_062** | Logout & Nav | Verify Logout from the Hamburger menu invalidates the session and redirects to the Login page | Positive | Medium |
| **TS_063** | Logout & Nav | Verify that after Logout, pressing the browser Back button cannot return to the Inventory page (session destroyed) | Negative | Medium |
| **TS_064** | Logout & Nav | Verify the 'All Items' link in the menu navigates to the Inventory page | Positive | Low |
| **TS_065** | Logout & Nav | Verify 'Reset App State' clears the entire Cart and resets the app state | Positive | Low |
| **TS_066** | Logout & Nav | Verify the 'About' link in the menu navigates to the Sauce Labs website (external link) | Positive | Low |

---

## Traceability Matrix — Test Scenario → FR

This table demonstrates that every Functional Requirement is covered by at least 1 Test Scenario.

| **FR ID** | **Functionality** | **Test Scenario ID** | **Covered?** |
|---|---|---|---|
| **FR-001** | Valid login | TS_001, TS_002 | ✅ |
| **FR-002** | Reject incorrect password | TS_003 | ✅ |
| **FR-003** | Reject blank username | TS_004 | ✅ |
| **FR-004** | Reject blank password | TS_005 | ✅ |
| **FR-005** | Block suspended account | TS_007 | ✅ |
| **FR-006** | Logout | TS_062, TS_063 | ✅ |
| **FR-007** | Display product list | TS_014, TS_015 | ✅ |
| **FR-008** | Sort A→Z | TS_016 | ✅ |
| **FR-009** | Sort Z→A | TS_017 | ✅ |
| **FR-010** | Sort price ascending | TS_018 | ✅ |
| **FR-011** | Sort price descending | TS_019 | ✅ |
| **FR-012** | Add to Cart from Inventory | TS_020 | ✅ |
| **FR-013** | Remove from Cart via Inventory | TS_021 | ✅ |
| **FR-014** | Cart badge accurately updated | TS_022 | ✅ |
| **FR-015** | View product details | TS_027, TS_028, TS_029 | ✅ |
| **FR-016** | Add to Cart from Product Detail | TS_030 | ✅ |
| **FR-017** | Return to Inventory from Detail | TS_031, TS_032 | ✅ |
| **FR-018** | Display Cart correctly | TS_035, TS_036 | ✅ |
| **FR-019** | Remove product from Cart | TS_037, TS_038 | ✅ |
| **FR-020** | Continue Shopping | TS_039 | ✅ |
| **FR-021** | Proceed to Checkout | TS_040 | ✅ |
| **FR-022** | First Name validation | TS_046 | ✅ |
| **FR-023** | Last Name validation | TS_047 | ✅ |
| **FR-024** | Postal Code validation | TS_048 | ✅ |
| **FR-025** | Proceed to Checkout Step 2 | TS_045 | ✅ |
| **FR-026** | Order Overview displayed correctly | TS_051 | ✅ |
| **FR-027** | Accurate Item Total | TS_052 | ✅ |
| **FR-028** | Accurate 8% Tax | TS_053 | ✅ |
| **FR-029** | Accurate Grand Total | TS_054, TS_060 | ✅ |
| **FR-030** | Complete order (Finish) | TS_056 | ✅ |
| **FR-031** | Confirmation page displayed correctly | TS_056 | ✅ |
| **FR-032** | Back Home to Inventory | TS_057 | ✅ |
| **FR-033** | Hamburger menu | TS_061 | ✅ |
| **FR-034** | All Items link | TS_064 | ✅ |
| **FR-035** | About link | TS_066 | ✅ |
| **FR-036** | Reset App State | TS_065 | ✅ |

---

*— End of Test Scenario Document SWG-TS-2026 —*

*Total: 66 Test Scenarios │ 36 FRs covered 100% │ Next step: Write Test Cases*
