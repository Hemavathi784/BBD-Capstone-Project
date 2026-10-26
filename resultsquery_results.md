# BBD Analytics — Query Execution Results

## Seed check
- reps: 4 rows
- products: 9 rows
- customers: 24 rows
- orders: 90 rows

## q01
Rows returned: 19
First 5 rows:
| order_id | customer_id | item | amount |
| :--- | :--- | :--- | :--- |
| 1001 | 10 | Bluetooth Speaker | NULL |
| 1002 | 16 | Smart Watch | 4500 |
| 1004 | 19 | Cotton Kurta | 2800 |
| 1010 | 19 | Wireless Earbuds | NULL |
| 1033 | 18 | Denim Jacket | 2500 |

## q02
Rows returned: 3
| order_id | customer_id | item | status |
| :--- | :--- | :--- | :--- |
| 1001 | 10 | Bluetooth Speaker | pending |
| 1010 | 19 | Wireless Earbuds | pending |
| 1064 | 20 | Bluetooth Speaker | pending |

## q03
Rows returned: 5
| order_id | customer_id | item | amount |
| :--- | :--- | :--- | :--- |
| 1061 | 16 | Air Fryer | 15600 |
| 1065 | 22 | Air Fryer | 15600 |
| 1069 | 15 | Air Fryer | 15600 |
| 1077 | 3 | Air Fryer | 15600 |
| 1006 | 5 | Smart Watch | 13500 |

## q04
Rows returned: 8
| customer_id | first_name | last_name | region | age |
| :--- | :--- | :--- | :--- | :--- |
| 24 | Reena | Kulkarni | West | 25 |
| 8 | Divya | Gupta | West | 26 |
| 17 | Farhan | Shah | North | 27 |
| 1 | aarav | Sharma | North | 28 |
| 16 | Nisha | Mishra | West | 36 |

## q05
Rows returned: 1
| total_orders | total_revenue | avg_order_value | min_order_value | max_order_value |
| :--- | :--- | :--- | :--- | :--- |
| 63 | 346200 | 5495.2381 | 1100 | 15600 |

## q06
Rows returned: 3
| status | number_of_orders | total_amount |
| :--- | :--- | :--- |
| completed | 63 | 346200 |
| pending | 19 | 51100 |
| disputed | 8 | 83200 |

## q07
Rows returned: 4
| item | number_of_orders | revenue |
| :--- | :--- | :--- |
| Air Fryer | 10 | 104000 |
| Smart Watch | 10 | 73500 |
| Wireless Earbuds | 12 | 57600 |
| Running Shoes | 8 | 39600 |

## q08
Rows returned: 4
| region | number_of_customers | average_age | min_age | max_age |
| :--- | :--- | :--- | :--- | :--- |
| East | 6 | 34.0000 | 29 | 41 |
| North | 6 | 37.5000 | 27 | 48 |
| South | 6 | 34.6667 | 24 | 52 |
| West | 6 | 28.5000 | 22 | 39 |

## q09
Rows returned: 90
First 5 rows:
| order_id | order_month | first_name | last_name | region | rep_name | item | quantity | amount | status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1001 | 2026-09 | MEERA |   Patil | South | Kavya Nair | Bluetooth Speaker | 2 | NULL | pending |
| 1002 | 2026-09 | Nisha | Mishra | West | Neha Kulkarni | Smart Watch | 1 | 4500 | pending |
| 1003 | 2026-09 | Lakshmi | Kapoor | South | Kavya Nair | Air Fryer | 2 | 10400 | disputed |
| 1004 | 2026-09 | Gaurav | Yadav | East | Sanjay Roy | Cotton Kurta | 2 | 2800 | pending |
| 1005 | 2026-09 | Tanvi | Thakur | South | Kavya Nair | Table Lamp | 1 | 1100 | completed |

## q10
Rows returned: 4
| customer_id | first_name | last_name | region |
| :--- | :--- | :--- | :--- |
| 6 | Ananya | Reddy | South |
| 11 | Imran | Joshi | East |
| 17 | Farhan | Shah | North |
| 24 | Reena | Kulkarni | West |

## q11
Rows returned: 12
First 5 rows:
| region | order_month | number_of_orders | number_of_customers | total_revenue | average_revenue |
| :--- | :--- | :--- | :--- | :--- | :--- |
| East | 2026-09 | 3 | 3 | 11300 | 3766.6667 |
| East | 2026-10 | 4 | 3 | 14400 | 3600.0000 |
| East | 2026-11 | 6 | 3 | 47300 | 7883.3333 |
| North | 2026-09 | 8 | 3 | 53100 | 6637.5000 |
| North | 2026-10 | 5 | 3 | 31700 | 6340.0000 |

## q12
Rows returned: 9
| item | total_revenue | contribution_tier |
| :--- | :--- | :--- |
| Air Fryer | 104000 | High |
| Smart Watch | 73500 | High |
| Wireless Earbuds | 57600 | Medium |
| Running Shoes | 39600 | Medium |
| Denim Jacket | 25000 | Medium |
| Cotton Kurta | 16800 | Medium |
| Bedsheet Set | 15200 | Medium |
| Bluetooth Speaker | 11200 | Low |
| Table Lamp | 3300 | Low |

## q13
Rows returned: 12
First 5 rows:
| rep_name | order_month | monthly_target | revenue | performance_tier |
| :--- | :--- | :--- | :--- | :--- |
| Arjun Mehta | 2026-09 | 40000 | 53100 | Above Target |
| Arjun Mehta | 2026-10 | 40000 | 31700 | Below Target |
| Arjun Mehta | 2026-11 | 40000 | 18100 | Below Target |
| Kavya Nair | 2026-09 | 20000 | 24800 | Above Target |
| Kavya Nair | 2026-10 | 20000 | 9900 | Below Target |