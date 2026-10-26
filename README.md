# BBD-Capstone-Project

Big Billion Days Regional Performance Review

Project Overview
End-to-end, traceable analytics pipeline for Flipkart’s Big Billion Days (BBD) review. This repository integrates SQL data extraction, spreadsheet reconciliation, an executive dashboard specification, and an AI-audit verification log.

Environment & Tech Stack
- **SQL Dialect & Engine**: MySQL 8.0 (ANSI SQL compliant)
- **Data Reconciliation Layer**: Google Sheets / Microsoft Excel
- **Data Visualization**: Tableau Public (Specification-ready design)

---

Executive Summary (Top 3 Findings)
1. **Regional Leadership**: **South** led overall revenue generation at **₹108,000**, outperforming **Central** (₹65,000) by 66.1%.
2. **Category Concentration**: **Electronics** dominated performance across all territories, generating **₹240,000** (69.3% of total revenue: ₹346,200).
3. **Sales Trajectory**: Peak volume materialized in **October 2026** (₹145,000), followed by a steep deceleration in **November 2026** (₹89,200).

Repository Structure & File Mapping

| File Path | Description | Project Phase |
| :--- | :--- | :--- |
| `README.md` | Executive overview, environment specs, and repository guide | Overview |
| `sql/00_schema_and_seed.sql` | DDL schema creation and raw transactional seed scripts | Part A |
| `sql/q01.sql` ... `sql/q13.sql` | Modular SQL scripts answering core business questions 1–13 | Part A |
| `results/query_results.md` | Audit-verified SQL outputs and formatted result tables | Part A |
| `data/orders_enriched.csv` | Initial fact table export prior to spreadsheet cleaning | Part B |
| `data/orders_clean.csv` | Standardized, 13-column cleaned fact dataset | Part B |
| `docs/spreadsheet_notes.md` | Data cleaning formulas, pivot outputs, and 1:1 reconciliation | Part B |
| `docs/dashboard_spec.md` | Tableau dashboard layout, container specs, and narrative | Part C |
| `docs/ai_log.md` | AI prompt log, error resolution, and verification steps | Part D |

Key Business Assumptions
Revenue Isolation:: All financial metrics strictly filter for completed orders (`status = 'completed'`). Pending/disputed orders are tracked separately as pipeline risk.
Data Integrity :Missing transaction values were dynamically computed via `quantity * unit_price`.
String Preservation: Temporal attributes are strictly enforced as text (`YYYY-MM`) across all layers to prevent spreadsheet date-type corruption.
