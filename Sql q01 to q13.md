Sql/q01 \-- What are the details of all pending orders in ascending order of order ID?  
SELECT  
  o.order\_id,  
  o.customer\_id,  
  o.item,  
  o.amount  
FROM orders o  
WHERE o.status \= 'pending'  
ORDER BY o.order\_id ASC;

Sql/q02 \-- Which orders have a missing (NULL) amount value?  
SELECT  
  o.order\_id,  
  o.customer\_id,  
  o.item,  
  o.status  
FROM orders o  
WHERE o.amount IS NULL  
ORDER BY o.order\_id ASC;

sql/q03 \-- What are the five largest completed orders by amount?  
SELECT  
  o.order\_id,  
  o.customer\_id,  
  o.item,  
  o.amount  
FROM orders o  
WHERE o.status \= 'completed'  
ORDER BY o.amount DESC, o.order\_id ASC  
LIMIT 5;

sql/q04 \-- Which target customers aged 25 to 40 belong to the North or West regions?  
SELECT  
  c.customer\_id,  
  c.first\_name,  
  c.last\_name,  
  c.region,  
  c.age  
FROM customers c  
WHERE c.region IN ('North', 'West')  
  AND c.age BETWEEN 25 AND 40  
ORDER BY c.age ASC, c.customer\_id ASC;

sql/q05 \-- What are the headline performance metrics for completed orders?  
SELECT  
  COUNT(o.order\_id) AS total\_orders,  
  SUM(o.amount) AS total\_revenue,  
  AVG(o.amount) AS avg\_order\_value,  
  MIN(o.amount) AS min\_order\_value,  
  MAX(o.amount) AS max\_order\_value  
FROM orders o  
WHERE o.status \= 'completed';

sql/q06 \-- How are orders and monetary amounts distributed across different order statuses?  
SELECT  
  o.status,  
  COUNT(o.order\_id) AS number\_of\_orders,  
  SUM(o.amount) AS total\_amount  
FROM orders o  
GROUP BY o.status  
ORDER BY number\_of\_orders DESC;

sql/q07 \-- Which product items generated over 20,000 INR in completed revenue?  
SELECT  
  o.item,  
  COUNT(o.order\_id) AS number\_of\_orders,  
  SUM(o.amount) AS revenue  
FROM orders o  
WHERE o.status \= 'completed'  
GROUP BY o.item  
HAVING SUM(o.amount) \> 20000  
ORDER BY revenue DESC;

sql/q08 \-- What is the demographic customer count and age distribution by region?  
SELECT  
  c.region,  
  COUNT(c.customer\_id) AS number\_of\_customers,  
  AVG(c.age) AS average\_age,  
  MIN(c.age) AS min\_age,  
  MAX(c.age) AS max\_age  
FROM customers c  
GROUP BY c.region  
ORDER BY c.region ASC;

sql/q09 \-- What is the complete order-level fact table containing customer and rep details?  
SELECT  
  o.order\_id,  
  o.order\_month,  
  c.first\_name,  
  c.last\_name,  
  c.region,  
  r.rep\_name,  
  o.item,  
  o.quantity,  
  o.amount,  
  o.status  
FROM orders o  
JOIN customers c ON o.customer\_id \= c.customer\_id  
JOIN reps r ON c.rep\_id \= r.rep\_id  
ORDER BY o.order\_id ASC;

sql/q10 \-- Which registered customers have never placed any order?  
SELECT  
  c.customer\_id,  
  c.first\_name,  
  c.last\_name,  
  c.region  
FROM customers c  
LEFT JOIN orders o ON c.customer\_id \= o.customer\_id  
WHERE o.order\_id IS NULL  
ORDER BY c.customer\_id ASC;

sql/q11 \-- What are the regional and monthly sales metrics for completed orders?  
SELECT  
  c.region,  
  o.order\_month,  
  COUNT(o.order\_id) AS number\_of\_orders,  
  COUNT(DISTINCT c.customer\_id) AS number\_of\_customers,  
  SUM(o.amount) AS total\_revenue,  
  AVG(o.amount) AS average\_revenue  
FROM orders o  
JOIN customers c ON o.customer\_id \= c.customer\_id  
WHERE o.status \= 'completed'  
GROUP BY c.region, o.order\_month  
ORDER BY c.region ASC, o.order\_month ASC;

sql/q12  \-- How are product items classified into contribution tiers based on completed revenue?  
SELECT  
  o.item,  
  SUM(o.amount) AS total\_revenue,  
  CASE  
    WHEN SUM(o.amount) \>= 60000 THEN 'High'  
    WHEN SUM(o.amount) \>= 15000 THEN 'Medium'  
    ELSE 'Low'  
  END AS contribution\_tier  
FROM orders o  
WHERE o.status \= 'completed'  
GROUP BY o.item  
ORDER BY total\_revenue DESC;

sql/q13 \-- How did sales reps perform against their monthly target each month?  
SELECT  
  r.rep\_name,  
  o.order\_month,  
  r.monthly\_target,  
  SUM(o.amount) AS revenue,  
  CASE  
    WHEN SUM(o.amount) \< r.monthly\_target THEN 'Below Target'  
    WHEN SUM(o.amount) \>= r.monthly\_target AND SUM(o.amount) \< 1.1 \* r.monthly\_target THEN 'On Target'  
    ELSE 'Above Target'  
  END AS performance\_tier  
FROM orders o  
JOIN customers c ON o.customer\_id \= c.customer\_id  
JOIN reps r ON c.rep\_id \= r.rep\_id  
WHERE o.status \= 'completed'  
GROUP BY r.rep\_name, o.order\_month, r.monthly\_target  
ORDER BY r.rep\_name ASC, o.order\_month ASC;  
