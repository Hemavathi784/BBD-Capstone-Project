# AI-Assisted Analysis and Human-in-the-Loop Verification Log

## Task 1: Five-Part Prompt for Part A (q13)

* Role: You are an expert SQL Data Analyst working on MySQL database systems.  
* Task: Write a MySQL query to calculate revenue tiers for sales representatives based on their total sales amount from completed orders.  
* Context: Use the real tables reps, customers, and orders. The schema joins orders to reps via rep\_id and customers via customer\_id. The dialect is standard MySQL.  
* Constraints: Filter for status \= 'completed' orders only. Categorize reps into three tiers: Tier 1 (\> 50,000), Tier 2 (20,000 to 50,000), and Tier 3 (\< 20,000). Do NOT use WITH clauses or stored procedures.  
* Format: Output raw MySQL code only with inline comments.

---

## Task 2: Inspection of Scenario D1

Below is the audit table of defects identified in the assistant's response:

| Defect / Issue | Defect Classification | Correct Clause / Fix |
| ----- | ----- | ----- |
| Table sales does not exist in schema | fake method/function | Query the real table orders joined with reps |
| Column region\_name and total\_sales do not exist | fake method/function | Use reps.region and orders.amount |
| WHERE SUM(total\_sales) \> 80000 aggregate filter in WHERE | logic error | Move aggregate filtering to HAVING SUM(orders.amount) \> 80000 |
| "North revenue grew 38% month over month" | phantom statistic | Contradicted by data; actual MoM growth is \-22.8% |

---

## Task 3: Verification of Scenario D1

* Corrected Query Output (sql/d1\_corrected.sql):  
  * North: 119,300  
  * South: 82,500  
* Actual MoM Growth Calculation for North:  
  * North 2026-09 Revenue \= 62,000  
  * North 2026-10 Revenue \= 47,800  
  * MoM Change \= ((47800 \- 62000\) / 62000\) \* 100 \= \-22.8%  
* Comparison: The assistant's claim of \+38% growth is factually false and contradicted by actual database records (-22.8%).

---

## Task 4: Human-in-the-Loop Protocol Execution

* Specification: Specified explicit requirements for regional performance review filtering for completed orders with revenue over 80,000.  
* Execution: Ran the assistant's suggested SQL query and verified it failed due to non-existent tables and syntax errors on aggregate WHERE filtering.  
* Inspection: Inspected schema mapping and identified 4 major defects including hallucinated table/column names and a fabricated growth metric.  
* Verification: Constructed and executed sql/d1\_corrected.sql against real seed data, returning North (119300) and South (82500), and verified North's MoM growth as \-22.8%.  
* Decision: Explicitly REJECT the original assistant answer due to schema hallucinations and a fabricated 38% statistic. ACCEPT the corrected version (sql/d1\_corrected.sql) verified directly against the database seed data.

---

## Task 5: Prompt and Diagnosis for Scenario D2

* Five-Part Prompt:  
  * Role: You are a Spreadsheet Automation Expert.  
  * Task: Diagnose and fix a \#N/A lookup error in Microsoft Excel.  
  * Context: Lookup cell G2 on orders tab contains " Smart Watch" (leading space). Range A1:C10 on products tab has item names in column A and unit prices in column C.  
  * Constraints: Fix the formula so it handles whitespace dynamically without modifying source data manually.  
  * Format: Provide the root cause analysis and the exact repaired formula.  
* Root Cause: The lookup key in cell G2 has a leading whitespace (" Smart Watch"), which fails to match the exact string "Smart Watch" in products\!$A$2:$A$10.  
* Repaired Formula: \=VLOOKUP(TRIM(G2), products\!$A$2:$C$10, 3, FALSE)

---

## Task 6: Skeptical-Analyst Check on Part C

* Skeptical Analyst Prompt: "Act as a skeptical senior business analyst and challenge my recommendation to reallocate marketing budget to the Central region. Identify unstated assumptions and demand data evidence proving causation rather than mere correlation."  
* Unstated Assumptions & Data Checks:  
  1. *Assumption 1:* Lower sales in Central region (65,000) is caused by under-marketing rather than poor product-market fit or lower population density. *Verification:* Check conversion rates per website visitor by region.  
  2. *Assumption 2:* Reallocating budget away from top-performing South region won't reduce overall revenue. *Verification:* Compare customer acquisition cost (CAC) and customer lifetime value (LTV) between Central and South.  
  3. *Assumption 3:* Sales reps in Central region have equal closing capacity as other regions. *Verification:* Check individual rep performance metrics in q08 and q13 for Central reps.

