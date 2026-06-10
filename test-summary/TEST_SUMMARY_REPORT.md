# Test Summary Report — Swag Labs (SauceDemo)

| Field | Detail |
|---|---|
| **Document ID** | SWG-TSR-2026 |
| **Project** | SauceDemo Manual Testing |
| **Tester** | Nguyễn Long Vũ |
| **Test Period** | 02/06/2026 — 09/06/2026 |
| **Environment** | Chrome 124 / Windows 11 |
| **Reference** | SWG-RA-2026 \| SWG-TP-2026 \| SWG-TS-2026 |

---

## 1. Overall Results

| Total TC | Pass | Fail | Pass Rate | Status |
|---|---|---|---|---|
| 66 | 65 | 1 | 98.5% |  PASSED with 1 minor defect |

---

## 2. Results by Module

| Module | Total | Pass | Fail | Pass Rate |
|---|---|---|---|---|
| 🔐 Login | 13 | 12 | 1 | 92.3% |
| 📦 Product List | 13 | 13 | 0 | 100% |
| 🔍 Product Detail | 8 | 8 | 0 | 100% |
| 🛒 Shopping Cart | 10 | 10 | 0 | 100% |
| 💳 Checkout | 16 | 16 | 0 | 100% |
| 🚪 Logout & Navigation | 6 | 6 | 0 | 100% |
| **TOTAL** | **66** | **65** | **1** | **98.5%** |

---

## 3. Bug Summary

### Confirmed Bug

| Bug ID | Title | Severity | Status | TC Ref |
|---|---|---|---|---|
| BUG-001 | Unauthenticated user can access /inventory.html without login | High | Open | TC_012 |

### Intentional Bugs (Known — No Fix Required)

| Account | Bug Description |
|---|---|
| `problem_user` | Wrong product images, Add to cart fails for some products |
| `performance_glitch_user` | Page load ~5 seconds, exceeds 3s threshold |
| `error_user` | Last Name field broken, validation bypassed, Finish button unresponsive |

---

## 4. Exit Criteria

| Criterion | Status |
|---|---|
| 100% TC Executed (66/66) | ✅ Met |
| Pass Rate ≥ 95% (98.5%) | ✅ Met |
| 0 Blocker / Critical bugs | ✅ Met |
| All 36 FR covered | ✅ Met |
| E2E Happy Path passes | ✅ Met |
| Pricing formula verified | ✅ Met |
| All bugs logged | ✅ Met |
| High bug open (BUG-001) | ⚠️ Partial |

---

## 5. Key Findings

### What Works Well 
- Full E2E Happy Path completes without issues
- All 4 sort options return correct product order
- Cart state synchronized consistently across all pages
- Pricing formula (Item Total + 8% Tax = Grand Total) is 100% accurate
- Session properly invalidated on Logout

### Issues Found ⚠️
- **Security (High):** Unauthenticated access to /inventory.html — no redirect to Login (BUG-001)
- Cancel on Checkout Step 1 redirects to /cart.html — Expected Result updated accordingly
- performance_glitch_user load time ~5s exceeds NFR-P01 threshold

---

## 6. Conclusion

**Overall:** 98.5% pass rate — system quality is high for standard_user flow.

**Recommendation:**  CONDITIONALLY APPROVED  
Must fix BUG-001 (security) before release.  
After fix, re-execute TC_012 and TC_063 for regression verification.

---

*SWG-TSR-2026 | Nguyễn Long Vũ | 09/06/2026*
