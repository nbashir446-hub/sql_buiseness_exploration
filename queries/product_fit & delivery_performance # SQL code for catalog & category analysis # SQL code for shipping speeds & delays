USE magist;
SELECT * from customers;
SELECT count(*) AS orders_count from orders;

Are orders actually delivered?

SELECT order_status,COUNT(*) as orders from orders group by order_status;

Is Magist have a user growth?

SELECT YEAR(order_purchase_timestamp) AS year_, MONTH(order_purchase_timestamp) AS month_, COUNT(customer_id)
FROM orders GROUP BY year_, month_ ORDER BY year_, month_;

SELECT COUNT(DISTINCT product_id) AS product_count FROM products;

How many products are in the product table?

SELECT product_category_name,COUNT(DISTINCT product_id) AS n_products
FROM products GROUP BY product_category_name ORDER BY COUNT(product_id) DESC;

SELECT COUNT(DISTINCT product_id) AS n_products FROM order_items;

SELECT MIN(price) AS cheapest_product, MAX(price) AS most_expensive_product FROM order_items;
SELECT MIN(payment_value) AS lowest, MAX(payment_value) AS highest FROM order_payments;
SELECT * FROM products;
SELECT DISTINCT(product_category_name) AS catagories FROM products;
USE magist;

-- How many tech products for each seller per tech product category?
SELECT s.seller_id, COUNT(p.product_id), p.product_category_name
FROM sellers s
JOIN order_items oi
ON s.seller_id = oi.seller_id
JOIN products p
ON oi.product_id = p.product_id
WHERE p.product_category_name IN ('electronicos', 'informatica_acessorios','pcs', 'telefonia')
GROUP BY s.seller_id, p.product_category_name;

-- How many tech products for each seller per tech product category?
SELECT s.seller_id, COUNT(p.product_id), p.product_category_name
FROM sellers s
JOIN order_items oi ON s.seller_id = oi.seller_id
JOIN products p ON oi.product_id = p.product_id
WHERE product_category_name IN ('electronicos', 'informatica_acessorios','pcs', 'telefonia')
GROUP BY s.seller_id, p.product_category_name;
2.1.1

SELECT * FROM product_category_name_translation;
SELECT product_category_name_english AS tech_products, product_category_name FROM product_category_name_translation
WHERE product_category_name_english
IN ('audio', 'electronics', 'computer accessories', 'pc gamers', 'computers', 'tablets_printing_image','telephony')
GROUP BY product_category_name ORDER BY tech_products;

2.1.2


SELECT COUNT(DISTINCT oi.order_id) AS tech_products_sold
FROM order_items oi
LEFT JOIN products p
          USING (product_id)
LEFT JOIN product_category_name_translation pt
          USING (product_category_name)
WHERE product_category_name_english = "audio"
OR product_category_name_english =  "electronics"
OR product_category_name_english =  "computers_accessories"
OR product_category_name_english =  "pc_gamer"
OR product_category_name_english =  "computers"
OR product_category_name_english =  "tablets_printing_image"
OR product_category_name_english =  "telephony";

2.1.3

SELECT COUNT(DISTINCT(oi.product_id)) AS tech_products_sold, product_category_name_english, ROUND(AVG(price), 2) as average_price
FROM order_items oi
LEFT JOIN products p 
	USING (product_id)
LEFT JOIN product_category_name_translation pt
	USING (product_category_name)
WHERE product_category_name_english = "audio"
OR product_category_name_english =  "electronics"
OR product_category_name_english =  "computers_accessories"
OR product_category_name_english =  "pc_gamer"
OR product_category_name_english =  "computers"
OR product_category_name_english =  "tablets_printing_image"
OR product_category_name_english =  "telephony"
GROUP BY product_category_name_english
ORDER BY tech_products_sold DESC;


percentage:

SELECT COUNT(DISTINCT(product_id)) AS products_sold
FROM order_items;
SELECT 3390 / 32951;
10.29%


2.1.3
SELECT ROUND(AVG(price), 2)
FROM order_items;

2.1.4

SELECT COUNT(oi.product_id), 
	CASE 
		WHEN price > 1000 THEN "Expensive"
		WHEN price > 100 THEN "Mid-range"
		ELSE "Cheap"
	END AS "price_range"
FROM order_items oi
LEFT JOIN products p
	ON p.product_id = oi.product_id
LEFT JOIN product_category_name_translation pt
	USING (product_category_name)
WHERE pt.product_category_name_english IN ("audio", "electronics", "computers_accessories", "pc_gamer", "computers", "tablets_printing_image", "telephony")
GROUP BY price_range
ORDER BY 1 DESC;


2.2.1
SELECT timestampdiff(MONTH, MIN(order_purchase_timestamp),MAX(order_purchase_timestamp))
FROM orders;

2.2.2

SELECT COUNT(DISTINCT(seller_id)) FROM sellers;

SELECT COUNT(DISTINCT(seller_id)) AS Tech_sellers FROM sellers
LEFT JOIN  order_items USING (seller_id)
LEFT JOIN products USING (product_id)
LEFT JOIN product_category_name_translation pt USING (product_category_name)
WHERE pt.product_category_name_english IN ("audio", "electronics", "computers_accessories", "pc_gamer", "computers", "tablets_printing_image", "telephony");

SELECT 454/3095;
14.67%


2.2.3

SELECT SUM(oi.price) AS total FROM order_items oi
LEFT JOIN orders o USING (order_id)
WHERE o.order_status NOT IN ('unavailable','canceled');

SELECT 13494400.74/3095/25;
174.40

SELECT SUM(oi.price) AS total FROM order_items oi
LEFT JOIN orders o USING (order_id)
LEFT JOIN products p USING (product_id)
LEFT JOIN product_category_name_translation pt USING (product_category_name)
WHERE o.order_status NOT IN ('unavailable','canceled')
AND pt.product_category_name_english IN ("audio", "electronics", "computers_accessories", "pc_gamer", "computers", "tablets_printing_image", "telephony");

SELECT 1666211.18/454/25;
avg = 146.80

SELECT AVG(DATEDIFF(order_delivered_customer_date,order_purchase_timestamp)) FROM orders;

-- What’s the average time between the order being placed and the product being delivered?
SELECT AVG(DATEDIFF(order_delivered_customer_date, order_purchase_timestamp))
FROM orders;
	-- 12.5035
    
-- SELECT DATEDIFF(order_delivered_customer_date, order_purchase_timestamp)
-- FROM orders;

--- SELECT DATEDIFF('2008-05-17 11:31:31','2008-04-28 11:34:50');

-- How many orders are delivered on time vs orders delivered with a delay?
SELECT 
	CASE 
		WHEN DATE(order_delivered_customer_date) <= DATE(order_estimated_delivery_date) THEN 'On time'
		ELSE 'Delayed'
    END AS delivery_status, 
COUNT(order_id) AS orders_count
FROM orders
WHERE order_status = 'delivered'
GROUP BY delivery_status;






-- Is there any pattern for delayed orders, e.g. big products being delayed more often?
SELECT
	CASE 
		WHEN DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) > 100 THEN "> 100 day Delay"
        WHEN DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) >= 8 AND DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) < 100 THEN "1 week to 100 day delay"
		WHEN DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) > 3 AND DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) < 8 THEN "3-7 day delay"
		WHEN DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) > 1 THEN "1 - 3 days delay"
		ELSE "<= 1 day delay"
	END AS "delay_range", 
AVG(product_weight_g) AS weight_avg,
MAX(product_weight_g) AS max_weight,
MIN(product_weight_g) AS min_weight,
SUM(product_weight_g) AS sum_weight,
COUNT(*) AS product_count 
FROM orders a
LEFT JOIN order_items b
	ON a.order_id = b.order_id
LEFT JOIN products c
	ON b.product_id = c.product_id
WHERE DATEDIFF(order_estimated_delivery_date, order_delivered_customer_date) > 0
GROUP BY delay_range
ORDER BY weight_avg DESC;
