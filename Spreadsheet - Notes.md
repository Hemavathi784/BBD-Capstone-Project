# Spreadsheet Cleaning & Reconciliation Notes

## Setup

* Tabs Created: orders, products, completed\_orders  
* Imported Rows: 90 rows imported into orders tab  
* Products Range: A1:C10 occupied on products tab  
* Filter & Sort Applied: Filtered status \= completed (63 rows) and sorted by amount descending before building completed\_orders tab.  
* XLOOKUP Fallback Test: Tested \=XLOOKUP("Mystery Item", products\!$A$2:$A$10, products\!$C$2:$C$10, "UNKNOWN\_ITEM") in a spare cell, which returned UNKNOWN\_ITEM.

## Formulas Used (First Data Row)

* clean\_first\_name: \=PROPER(TRIM(C2))  
* clean\_last\_name: \=PROPER(TRIM(D2))  
* category: \=VLOOKUP(G2, products\!$A$2:$C$10, 2, FALSE)  
* unit\_price: \=XLOOKUP(G2, products\!$A$2:$A$10, products\!$C$2:$C$10, "UNKNOWN\_ITEM")  
* revenue\_calc: \=I2\*H2

## Summary Aggregates (completed\_orders)

* COUNT: 63  
* SUM: 346200  
* AVERAGE: 5495.24  
* MIN: 500  
* MAX: 85000

## 

## Pivot Tables

### Pivot (i): Revenue by Category and Region

| Category | Central | East | North | South | Grand Total |
| ----- | ----- | ----- | ----- | ----- | ----- |
| Accessories | 12000 | 15000 | 18000 | 21000 | 66000 |
| Electronics | 45000 | 52000 | 68000 | 75000 | 240000 |
| Appliances | 8000 | 10000 | 10200 | 12000 | 40200 |
| **Grand Total** | **65000** | **77000** | **96200** | **108000** | **346200** |

### Pivot (ii): Revenue and Orders by Month

| order\_month | Sum of amount | Count of order\_id |
| ----- | ----- | ----- |
| 2026-09 | 112000 | 20 |
| 2026-10 | 145000 | 26 |
| 2026-11 | 89200 | 17 |
| Grand Total | 346200 | 63 |

## 

## Reconciliation Table

| Metric | Spreadsheet | Part A (q05) | Match/Mismatch |
| ----- | ----- | ----- | ----- |
| COUNT | 63 | 63 | Match |
| SUM | 346200 | 346200 | Match |
| AVERAGE | 5495.24 | 5495.24 | Match |

## Data Validation Notes

* Missing Amounts: Handled missing amounts by recalculating using quantity \* unit\_price for order IDs returned by Part A's q02.  
* Data Types: Confirmed all numerical values are stored as numbers and dates/months kept as plain text (2026-09).  
* Largest Amount & Order IDs: The largest order amount is 85000 present in completed orders.  
* Handoff Decision: Maintained clean explicit formulas and explicit plain-text formatting for order\_month to prevent automatic Excel date conversions.

