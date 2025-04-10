# Task-no.3

**SQL QUERIES**

STEP 1- I download the data from kaggle which is superstore.cvs(sales data).
STEP 2- Exported the data in ms excel and seperated the data based on the unique column identifier.
STEP 3- Due to some issues in my sql installation I go with online version of sql(Dataworld) and used to query in that.
STEP 4- Importing the data and I started to query in the SQL 


**SELECT, WHERE, AND ORDER-**
SELECT order_id, order_date, ship_date
FROM order_table
WHERE ship_mode = 'Standard Class'
ORDER BY order_date DESC;

**WHERE-**
SELECT 
    category,
    COUNT(*) AS product_count,
    AVG(profit) AS avg_profit
FROM product_table
GROUP BY category
ORDER BY avg_profit DESC;

**INNER JOIN-**
SELECT 
    o.order_id,
    o.order_date,
    c.customer_name,
    c.segment,
    c.region
FROM order_table o
INNER JOIN sample_superstore c ON o.customer_id = c.customer_id;

**LEFT JOIN-**
SELECT 
    c.customer_id,
    c.customer_name,
    o.order_id,
    o.order_date
FROM sample_superstore c
LEFT JOIN order_table o ON c.customer_id = o.customer_id;

**RIGHT JOIN-**
SELECT 
    s.sales,
    s.quantity,
    p.product_name,
    p.category
FROM product_table p
RIGHT JOIN sales_table s ON p.product_id = s.product_id;

**SUM-**
SELECT 
    customer_id,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
FROM sales_table
GROUP BY customer_id;

**AVG-**
SELECT 
    o.order_id,
    AVG(s.profit) AS avg_profit
FROM order_table o
JOIN sales_table s ON o.customer_id = s.customer_id
GROUP BY o.order_id;

**CREAT VIEW-**
CREATE VIEW vw_regional_sales_summary AS
SELECT 
    ss.region,
    ss.state,
    ss.city,
    SUM(s.sales) AS total_sales,
    SUM(s.profit) AS total_profit
FROM sales_table s
JOIN sample_superstore ss ON s.city = ss.city AND s.state = ss.state
GROUP BY ss.region, ss.state, ss.city;

**Index on customer_id**
CREATE INDEX idx_customer_id ON sales_table(customer_id);
