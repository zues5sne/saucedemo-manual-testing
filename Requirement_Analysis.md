# REQUIREMENT ANALYSIS DOCUMENT

**System Requirements Analysis Document**

---

**SWAG LABS**
https://www.saucedemo.com

| **Version** | 1.0 |
|---|---|
| **Date Created** | 02/06/2026 |
| **Analyzed by** | BA Team + Senior QA |
| **Project Code** | SWG-RA-2026 |
| **Status** | Approved |

---

## 1. SYSTEM OVERVIEW

### 1.1 System Description

Swag Labs (saucedemo.com) is a demo e-commerce web application developed and maintained by Sauce Labs — a leading software testing platform company. The application is specifically designed as a realistic testing environment, fully simulating the online shopping flow from login to order completion.

A key characteristic of Swag Labs is that the system deliberately integrates various types of bugs through separate test accounts, enabling testers to practice bug detection, analysis, and reporting skills in a near-real-world environment.

### 1.2 Technical Information

| **Field** | **Details** |
|---|---|
| **URL** | https://www.saucedemo.com |
| **Application Type** | Single Page Application (SPA) — React |
| **Platform** | Web Browser (Desktop) |
| **Supported Browsers** | Chrome, Firefox, Edge, Safari |
| **Authentication** | Session-based (username + password) |
| **Backend** | API-driven (RESTful) |
| **Status** | Live — Publicly accessible, no registration required |

### 1.3 Available Test Accounts

| **Username** | **Password** | **Account Type** | **Characteristics / Test Purpose** |
|---|---|---|---|
| **standard_user** | secret_sauce | Standard Account | Normal operation — used for happy path testing |
| **locked_out_user** | secret_sauce | Locked Account | Blocked login — tests error handling for suspended accounts |
| **problem_user** | secret_sauce | Bug Account | Multiple intentional UI/UX bugs — tests visual bug detection skills |
| **performance_glitch_user** | secret_sauce | Performance Account | Abnormally slow loading — tests performance & timeout handling |
| **error_user** | secret_sauce | Form Error Account | Some form actions fail — tests error states in checkout |
| **visual_user** | secret_sauce | Visual Bug Account | Broken layout, CSS issues — tests visual regression |

---

## 2. CORE FEATURES & TEST MODULES

### 2.1 High-Level Module Overview

Swag Labs is divided into 6 core modules with the following dependency flow:

| **M1** | **M2** | **M3** | **M4** | **M5** | **M6** |
|---|---|---|---|---|---|
| **Login** | **Inventory** | **Product Detail** | **Cart** | **Checkout** | **Navigation** |
| User authentication | Browse & filter products | View product details | Manage shopping cart | 3-step payment | Navigation & menu |

### 2.2 Detailed Module Descriptions

#### MODULE 1 — Login / Authentication

| **Field** | **Details** |
|---|---|
| **Description** | Handles user authentication — the sole entry point to the entire system |
| **URL** | `/` (root) — redirects to `/inventory.html` after login |
| **UI Components** | Username input, Password input, LOGIN button, Error message container |
| **Functionality** | Valid login, Reject invalid login, Account lockout, Form validation, Error display |
| **Criticality** | Critical — the entire system is inaccessible if login fails |
| **Test Complexity** | Medium — multiple account types, multiple negative cases |

#### MODULE 2 — Product Inventory

| **Field** | **Details** |
|---|---|
| **Description** | Displays all products after successful login |
| **URL** | `/inventory.html` |
| **UI Components** | Product grid (6 items), Sort dropdown, Add to cart buttons, Cart badge, Header, Hamburger menu |
| **Functionality** | Display 6 products, Sort by name A-Z/Z-A and price Low-High/High-Low, Add/Remove to cart, Badge count |
| **Product Data** | Sauce Labs Backpack ($29.99), Bike Light ($9.99), Bolt T-Shirt ($15.99), Fleece Jacket ($49.99), Onesie ($7.99), Test.allTheThings() T-Shirt ($15.99) |
| **Criticality** | High — primary page with the most user interaction |

#### MODULE 3 — Product Detail

| **Field** | **Details** |
|---|---|
| **Description** | Displays detailed information for each product when clicked |
| **URL** | `/inventory-item.html?id={product_id}` |
| **UI Components** | Product image, Product name, Description, Price, Add to Cart button, Back button |
| **Functionality** | View product details, Add/Remove to Cart, Navigate back to Inventory |
| **Criticality** | Medium — limited complex logic; primarily tests display and navigation |

#### MODULE 4 — Shopping Cart

| **Field** | **Details** |
|---|---|
| **Description** | Displays and manages products added by the user |
| **URL** | `/cart.html` |
| **UI Components** | Cart item list (Qty, Name, Description, Price), Remove button, Continue Shopping button, Checkout button |
| **Functionality** | View cart items, Remove items, Navigate via Continue Shopping / Checkout |
| **Criticality** | High — bridge between browsing and checkout; failures block the entire purchase flow |
| **Special Note** | Swag Labs does **NOT** support quantity increment/decrement — Qty is always 1 |

#### MODULE 5 — Checkout (3-Step Payment)

| **Field** | **Details** |
|---|---|
| **Description** | 3-step checkout process: Information → Review → Completion |
| **Step 1 — URL** | `/checkout-step-one.html` — Form: First Name, Last Name, Zip/Postal Code |
| **Step 2 — URL** | `/checkout-step-two.html` — Order Overview: products, prices, tax, total |
| **Step 3 — URL** | `/checkout-complete.html` — Confirmation page |
| **Pricing Formula** | Item Total = sum of product prices │ Tax = 8% × Item Total │ Grand Total = Item Total + Tax |
| **Criticality** | Critical — this is the core business flow; failures directly impact revenue |
| **Test Complexity** | Highest — validation, calculations, state management, E2E flow |

#### MODULE 6 — Navigation & Hamburger Menu

| **Field** | **Details** |
|---|---|
| **Description** | Hidden navigation menu, opened via the hamburger icon (top-left) |
| **UI Components** | Menu overlay, All Items link, About link, Logout link, Reset App State link, Close (X) button |
| **Functionality** | All Items → `/inventory.html` │ About → Sauce Labs website │ Logout → clears session, returns to Login │ Reset App State → clears cart |
| **Criticality** | Medium — rarely fails, but Logout and Reset are critical flows |

---

## 3. BUSINESS FLOWS & USER FLOWS

### 3.1 Business Flow — Core Business Processes

From a Business Analyst perspective, Swag Labs simulates the fundamental e-commerce business flow:

| **Step** | **Business Activity** | **Description** | **Success Condition** |
|---|---|---|---|
| **BF-01** | **Authentication** | User provides credentials. System verifies and grants access based on account type. | Valid session created. Redirect to Inventory. |
| **BF-02** | **Product Discovery** | User browses the product list, filters/sorts to find suitable products. | Products displayed correctly, sort order accurate. |
| **BF-03** | **Product Selection** | User views product details and decides to add to cart. | Product correctly added to Cart, badge updated. |
| **BF-04** | **Cart Management** | User reviews and edits the cart before checkout. | Cart accurately reflects user selections. |
| **BF-05** | **Customer Information Entry** | User provides required information for order processing. | Validation passes, proceeds to next step. |
| **BF-06** | **Order Review** | System presents full order information for final user confirmation. | Information accurate, total calculated correctly. |
| **BF-07** | **Order Completion** | User confirms the order. System processes and notifies result. | Confirmation page displayed, cart reset to empty. |

### 3.2 User Flow — Detailed User Journey

#### Happy Path (Standard Success Flow)

This is the primary flow that testers must ensure works flawlessly 100% of the time:

| **#** | **User Action** | **System Response** | **URL / State** |
|---|---|---|---|
| **1** | Access https://www.saucedemo.com | Login page displayed with Username & Password form | `saucedemo.com/` — Unauthenticated |
| **2** | Enter standard_user / secret_sauce, click LOGIN | Authentication successful, automatic redirect | → `/inventory.html` — Authenticated |
| **3** | View list of 6 products | Inventory page fully loaded: images, names, prices, Add to cart buttons | `/inventory.html` — Cart: 0 |
| **4** | Click 'Add to cart' on Sauce Labs Backpack ($29.99) | Button changes to 'Remove', cart badge shows '1' | `/inventory.html` — Cart: 1 |
| **5** | Click on Sauce Labs Bike Light name to view details | Product Detail page loads with full product info | `/inventory-item.html?id=0` — Cart: 1 |
| **6** | Click 'Add to cart' in Product Detail | Button changes to 'Remove', cart badge shows '2' | `/inventory-item.html` — Cart: 2 |
| **7** | Click Cart icon in header | Cart page loads with 2 selected products | `/cart.html` — Cart: 2 |
| **8** | Review cart, click 'Checkout' | Redirects to customer information form | `/checkout-step-one.html` |
| **9** | Enter First Name: Nguyen, Last Name: Van A, Postal: 70000, click Continue | Validation passes, advances to Overview | `/checkout-step-two.html` |
| **10** | Review Order Overview — verify Item Total: $39.98, Tax: $3.20, Total: $43.18 | All information displayed correctly | `/checkout-step-two.html` |
| **11** | Click 'Finish' | Order completed, Confirmation page displayed | `/checkout-complete.html` — Cart: 0 |
| **12** | Click 'Back Home' | Returns to Inventory with empty cart | `/inventory.html` — Cart: 0 |

#### Alternative Flows

| **Flow ID** | **Scenario** | **Trigger** | **Expected Outcome** |
|---|---|---|---|
| **AF-01** | Remove item from Cart | Click Remove on Cart page | Item removed, badge decremented; if cart empty, Checkout still accessible (displays empty cart) |
| **AF-02** | Remove item from Inventory after adding | Click Remove on Inventory page | Item removed from Cart, badge decremented, button reverts to 'Add to cart' |
| **AF-03** | Return to Inventory from Cart | Click 'Continue Shopping' | Returns to Inventory, cart state preserved |
| **AF-04** | Cancel Checkout from Overview | Click 'Cancel' at Step 2 | Returns to Inventory, cart state preserved |
| **AF-05** | Add then Remove all items, then Checkout | Empty cart when clicking Checkout | Proceeds to checkout-step-one with empty cart, can continue to completion |

#### Exception Flows (Negative Cases)

| **Flow ID** | **Error Scenario** | **Trigger** | **Expected Outcome** |
|---|---|---|---|
| **EF-01** | Login with incorrect password | Enter wrong password, click LOGIN | Error: 'Username and password do not match any user in this service' |
| **EF-02** | Login with blank username | Leave username empty, click LOGIN | Error: 'Username is required' |
| **EF-03** | Login with blank password | Leave password empty, click LOGIN | Error: 'Password is required' |
| **EF-04** | Locked account login attempt | Login with locked_out_user | Error: 'Sorry, this user has been locked out' |
| **EF-05** | Checkout with blank First Name | Leave First Name empty, click Continue | Error: 'First Name is required' |
| **EF-06** | Checkout with blank Last Name | Leave Last Name empty, click Continue | Error: 'Last Name is required' |
| **EF-07** | Checkout with blank Postal Code | Leave Postal Code empty, click Continue | Error: 'Postal Code is required' |
| **EF-08** | Direct URL access without authentication | Enter /inventory.html in browser without login | Redirect to Login page |

---

## 4. FUNCTIONAL REQUIREMENTS (FR)

A total of **36 Functional Requirements** have been identified, covering all 6 modules of the system.

| **FR ID** | **Module** | **Title** | **Description & Acceptance Criteria** | **Priority** |
|---|---|---|---|---|
| **FR-001** | Login | **Valid Login** | System allows login when valid username and password are provided ✓ AC: Enter standard_user/secret_sauce → redirect to /inventory.html within 3 seconds | **Critical** |
| **FR-002** | Login | **Reject Incorrect Password** | System displays error message when password does not match; denies access ✓ AC: Error message appears, user remains on Login page | **Critical** |
| **FR-003** | Login | **Reject Blank Username** | System validates and notifies when username is left empty ✓ AC: Error: 'Username is required' displayed immediately on Login click | **High** |
| **FR-004** | Login | **Reject Blank Password** | System validates and notifies when password is left empty ✓ AC: Error: 'Password is required' displayed immediately on Login click | **High** |
| **FR-005** | Login | **Block Suspended Account** | System recognizes and rejects a locked account with a clear message ✓ AC: Login with locked_out_user → Error: 'Sorry, this user has been locked out' | **Critical** |
| **FR-006** | Login | **Logout** | User can securely log out; session is fully destroyed ✓ AC: Click Logout → returns to Login page; browser back button cannot access Inventory | **High** |
| **FR-007** | Inventory | **Display Product List** | Inventory page displays all 6 products with image, name, description, price, and Add to cart button ✓ AC: After login, 6 products displayed with complete information | **Critical** |
| **FR-008** | Inventory | **Sort by Name A→Z** | Sort products alphabetically from A to Z (default) ✓ AC: Order: Backpack → Bike Light → Bolt → Fleece → Onesie → T-shirt | **High** |
| **FR-009** | Inventory | **Sort by Name Z→A** | Sort products alphabetically from Z to A ✓ AC: Reverse order of A→Z | **High** |
| **FR-010** | Inventory | **Sort by Price Ascending** | Sort products by price from low to high ✓ AC: $7.99 → $9.99 → $15.99 → $15.99 → $29.99 → $49.99 | **High** |
| **FR-011** | Inventory | **Sort by Price Descending** | Sort products by price from high to low ✓ AC: $49.99 → $29.99 → $15.99 → $15.99 → $9.99 → $7.99 | **High** |
| **FR-012** | Inventory | **Add Product to Cart** | User clicks Add to cart → product is added to Cart ✓ AC: Button changes to 'Remove', cart badge increments by 1 | **Critical** |
| **FR-013** | Inventory | **Remove Product from Cart via Inventory** | User clicks Remove → product is removed from Cart ✓ AC: Button reverts to 'Add to cart', cart badge decrements by 1 | **High** |
| **FR-014** | Inventory | **Cart Badge Accurately Updated** | Badge on Cart icon accurately reflects the number of items in Cart at all times ✓ AC: Add 3 items → badge shows 3; remove 1 → badge shows 2 | **High** |
| **FR-015** | Product Detail | **View Product Details** | Click on product name/image → navigates to the correct product's detail page ✓ AC: Correct URL, complete: image, name, description, price, Add to Cart button | **Medium** |
| **FR-016** | Product Detail | **Add to Cart from Product Detail** | User can Add to Cart from the detail page ✓ AC: Same behavior as FR-012 | **High** |
| **FR-017** | Product Detail | **Return to Inventory** | Back button returns user to Inventory ✓ AC: Click Back → /inventory.html, cart state unchanged | **Medium** |
| **FR-018** | Cart | **Display Cart Items** | Cart correctly displays all added products with Qty, name, description, price ✓ AC: All added products displayed correctly — no more, no less | **Critical** |
| **FR-019** | Cart | **Remove Product from Cart** | Click Remove on Cart page → product immediately removed ✓ AC: Product disappears from list, badge decrements, button on Inventory reverts | **High** |
| **FR-020** | Cart | **Continue Shopping** | Continue Shopping button returns user to Inventory ✓ AC: Click → Inventory, cart state preserved | **Medium** |
| **FR-021** | Cart | **Proceed to Checkout** | Checkout button navigates to Checkout Step 1 ✓ AC: Click → /checkout-step-one.html | **Critical** |
| **FR-022** | Checkout Step 1 | **First Name Required Validation** | System prevents proceeding if First Name is empty ✓ AC: Error: 'First Name is required' | **Critical** |
| **FR-023** | Checkout Step 1 | **Last Name Required Validation** | System prevents proceeding if Last Name is empty ✓ AC: Error: 'Last Name is required' | **Critical** |
| **FR-024** | Checkout Step 1 | **Postal Code Required Validation** | System prevents proceeding if Postal Code is empty ✓ AC: Error: 'Postal Code is required' | **Critical** |
| **FR-025** | Checkout Step 1 | **Proceed to Overview on Valid Form** | When all fields are filled correctly → redirect to Checkout Step 2 ✓ AC: Redirect → /checkout-step-two.html | **Critical** |
| **FR-026** | Checkout Step 2 | **Display Correct Order Overview** | Order summary page displays all products, prices, tax, and total correctly ✓ AC: All Cart products displayed correctly | **Critical** |
| **FR-027** | Checkout Step 2 | **Accurate Item Total Calculation** | Item Total = sum of all product prices in Cart ✓ AC: 2 items: $29.99 + $9.99 = $39.98 | **Critical** |
| **FR-028** | Checkout Step 2 | **Accurate Tax Calculation** | Tax = 8% × Item Total ✓ AC: Tax on $39.98 = $3.20 | **Critical** |
| **FR-029** | Checkout Step 2 | **Accurate Grand Total Calculation** | Grand Total = Item Total + Tax ✓ AC: $39.98 + $3.20 = $43.18 | **Critical** |
| **FR-030** | Checkout Step 2 | **Complete Order** | Finish button completes the transaction and navigates to Confirmation ✓ AC: → /checkout-complete.html, cart reset to 0 | **Critical** |
| **FR-031** | Checkout Complete | **Display Confirmation Page** | Page displays checkmark icon, 'Thank you for your order!' heading ✓ AC: All elements appear correctly | **Critical** |
| **FR-032** | Checkout Complete | **Return to Home** | Back Home button returns user to Inventory with empty cart ✓ AC: → /inventory.html, cart badge not displayed | **High** |
| **FR-033** | Navigation | **Open/Close Hamburger Menu** | Hamburger icon → opens menu overlay; X → closes menu ✓ AC: Menu slides in/out smoothly | **Medium** |
| **FR-034** | Navigation | **All Items Link** | All Items in menu → navigates to Inventory ✓ AC: → /inventory.html | **Medium** |
| **FR-035** | Navigation | **About Link** | About in menu → Sauce Labs website ✓ AC: Opens Sauce Labs page (may open in new tab) | **Low** |
| **FR-036** | Navigation | **Reset App State** | Reset App State → clears entire cart, resets app state ✓ AC: Cart back to 0, all Add to cart buttons return to initial state | **Medium** |

---

## 5. NON-FUNCTIONAL REQUIREMENTS (NFR)

### 5.1 Performance Requirements

| **NFR ID** | **Criterion** | **Description** | **Acceptance Threshold** | **Priority** |
|---|---|---|---|---|
| **NFR-P01** | **Page Load Time** | Time to load Inventory page after successful login | < 3 seconds on 4G connection | **High** |
| **NFR-P02** | **Login Response Time** | Time to process and respond after clicking LOGIN | < 2 seconds | **Critical** |
| **NFR-P03** | **Add to Cart Response** | Time to update badge and button state after clicking Add to Cart | < 1 second (instantaneous from UX perspective) | **High** |
| **NFR-P04** | **Sort Response Time** | Time to reorder list after changing Sort option | < 1 second | **Medium** |
| **NFR-P05** | **Checkout Processing** | Time to process and navigate between Checkout steps | < 2 seconds per step | **High** |
| **NFR-P06** | **Performance User Tolerance** | Maximum acceptable load time for performance_glitch_user | < 8 seconds (may be slower than standard but must complete) | **Medium** |

### 5.2 Usability Requirements

| **NFR ID** | **Criterion** | **Description & Acceptance Criteria** |
|---|---|---|
| **NFR-U01** | **Error Message Clarity** | All error messages must be clear, specific, and indicate the exact error. Generic messages such as 'Error occurred' are not acceptable. |
| **NFR-U02** | **Visual Feedback** | Every user action must have immediate visual feedback: button color/text change, badge update, loading indicator if needed. |
| **NFR-U03** | **Consistent UI** | Interface must be consistent across all pages: same fonts, colors, and header layout. |
| **NFR-U04** | **Intuitive Navigation** | Users should be able to complete the full purchase flow without instructions. |
| **NFR-U05** | **Error Recovery** | After encountering an error, users can correct and continue without losing previously entered data. |
| **NFR-U06** | **Cart State Persistence** | Cart state must be maintained when navigating between pages within the same session. |

### 5.3 Security Requirements

| **NFR ID** | **Criterion** | **Description & Acceptance Criteria** |
|---|---|---|
| **NFR-S01** | **Authentication Required** | All pages (except Login) require authentication. Direct access to /inventory.html without login must redirect to Login. |
| **NFR-S02** | **Password Masking** | Password input must always display masked characters (•••) — plaintext must never be visible. |
| **NFR-S03** | **Session Invalidation on Logout** | After Logout, session is fully destroyed. Browser back button cannot return to authenticated pages. |
| **NFR-S04** | **No Sensitive Data in URL** | Sensitive information (passwords, session tokens) must not appear in the URL bar. |

### 5.4 Compatibility Requirements

| **NFR ID** | **Criterion** | **Description & Acceptance Criteria** |
|---|---|---|
| **NFR-C01** | **Browser Compatibility** | Fully functional on Chrome 120+, Firefox 120+, Edge 120+. Safari is best effort. |
| **NFR-C02** | **OS Compatibility** | Functional on Windows 10/11, macOS Ventura/Sonoma. |
| **NFR-C03** | **Screen Resolution** | Layout must not break at 1366×768 and 1920×1080 resolutions. |
| **NFR-C04** | **JavaScript Required** | Application is an SPA and requires JavaScript enabled. When JS is disabled, a clear message must be displayed. |

### 5.5 Reliability Requirements

| **NFR ID** | **Criterion** | **Description & Acceptance Criteria** |
|---|---|---|
| **NFR-R01** | **Data Consistency** | Products added to Cart from any page (Inventory/Product Detail) must be consistently synchronized. |
| **NFR-R02** | **Calculation Accuracy** | Pricing formulas (Item Total, Tax, Grand Total) must be 100% accurate with no incorrect rounding. |
| **NFR-R03** | **State Management** | Cart state must be consistent across all pages within the same session. |
| **NFR-R04** | **Error Message Consistency** | The same error condition must always display the same error message, consistent across test runs. |

---

## 6. TEST SCOPE

### 6.1 In Scope

| **Module** | **Test Types** | **Focus Area** | **Min TC** | **Target TC** |
|---|---|---|---|---|
| **Login** | Functional, Negative, Boundary | All account types, form validation, error messages | **12** | **15** |
| **Inventory** | Functional, UI Verification | 6 products, 4 sort options, Add/Remove, badge count | **10** | **15** |
| **Product Detail** | Functional, Navigation | Product info, Add to Cart, Back navigation | **5** | **8** |
| **Shopping Cart** | Functional, State Management | Display products, Remove, Continue Shopping, Checkout | **8** | **12** |
| **Checkout** | Functional, Negative, Calculation | 3-step flow, validation, pricing calculations, E2E flow | **15** | **20** |
| **Navigation** | Functional | Hamburger menu, Logout, Reset State | **5** | **8** |
| **Cross-browser** | Compatibility | Chrome, Firefox, Edge — core flows | **5** | **10** |
| **E2E Flow** | Integration | Happy path end-to-end per user account type | **3** | **5** |
| **TOTAL** | | | **63** | **93** |

### 6.2 Out of Scope

| **Item Excluded** | **Reason** | **Notes** |
|---|---|---|
| Automation Testing (Selenium, Cypress, etc.) | This is a Manual Testing project | Can be added as a separate project |
| Performance / Load Testing | Requires specialized tools (JMeter, k6) | Log observations in Bug Report if slowness detected |
| Security / Penetration Testing | Outside manual testing scope | Basic security tested per NFR-S requirements only |
| API Testing (Postman) | Not within Manual UI Testing scope | Can supplement for portfolio value |
| Mobile Responsive Testing | Application not optimized for mobile | Note any issues discovered incidentally |
| Database Testing | No database access | N/A for demo application |
| Payment Gateway Integration | Demo application — no real payment | N/A — simulated checkout only |

---

*— End of Requirement Analysis Document SWG-RA-2026 —*
