# Data Analytics Engineering Portfolio

A structured repository documenting hands-on data cleaning, reconciliation, and analytics engineering projects built to enterprise standards.

---

## Repository Contents

| Module / Week | Deliverable | Key Skills & Tools |
| :--- | :--- | :--- |
| **Week 1** | [`week1_erp_reconciliation.xlsx`](./week1_erp_reconciliation.xlsx) | Google Sheets / Excel, Deduplication, `TRIM`, `PROPER`, `XLOOKUP`, Absolute References, Pivot Tables |

---

## Project Log

### Week 1: Dirty ERP Data Reconciliation & Revenue Reporting
**File:** [`week1_erp_reconciliation.xlsx`](./week1_erp_reconciliation.xlsx)

**Business Problem:**
Reconciled raw ERP order exports (`raw_orders`) against a disconnected product pricing catalog (`sku_master`) containing duplicate order logs, inconsistent text casing/whitespace, and unmapped SKUs.

**Key Transformations & Methodology:**
* **Deduplication:** Identified and removed duplicate transaction rows (`ORD-103`) while preserving header integrity to prevent double-counted revenue.
* **Text Standardization:** Applied nested `=PROPER(TRIM(...))` functions to normalize inconsistent `customer_city` values (`"  mumbai  "`, `"DELHI"`, `"delhi"`) into clean, groupable dimensions (`clean_city`).
* **Relational Lookup & Error Handling:** Connected `raw_orders` to `sku_master` using `=XLOOKUP()` with locked absolute ranges (`$A$2:$A$4`, `$C$2:$C$4`) and fallback handling (`0` instead of `#N/A`) for missing catalog items (`SKU-Z9`).
* **Executive Summary (`city_summary`):** Built a Pivot Table aggregating total `gross_revenue` (`SUM`) and order volume (`COUNTA`) by `clean_city`, along with a data-quality flag highlighting underreported revenue caused by unmapped SKUs in the ERP catalog.