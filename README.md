SQL ASSIGNMENT

Instructions:-

1.Download the data files for this Assignment. Your first task is to create tables from the data files. In order to do so, please follow the steps given below:
i. Open MySQL Workbench
ii. Connect to your database using the connection you have created
iii. Create a database named Superstores
iv. In the “Navigator” pane on the left-hand side, you will find the created database
v. Right click on the superstores
vi. You will see the option called “Table Data Import Wizard”. Click on it.
vii. Follow the wizard to create tables by providing the .csv data files that you have downloaded.
viii. You need to follow the “Table Data Import Wizard” for each data file given for this assignment.
Task 1:- Understanding the Data
1. Describe the data in hand in your own words.
2. Identify and list the Primary Keys and Foreign Keys for this dataset provided to you(In case you don’t find either primary or foreign key, then specially mention this in your answer)
Task 2:- Basic & Advanced Analysis
1. Write a query to display the Customer_Name and Customer Segment using alias name “Customer Name", "Customer Segment" from table Cust_dimen.
2. Write a query to find all the details of the customer from the table cust_dimen order by desc.
3. Write a query to get the Order ID, Order date from table orders_dimen where ‘Order Priority’ is high. 4. Find the total and the average sales (display total_sales and avg_sales)
5. Write a query to get the maximum and minimum sales from maket_fact table.
6. Display the number of customers in each region in decreasing order of no_of_customers. The result should contain columns Region, no_of_customers.
7. Find the region having maximum customers (display the region name and max(no_of_customers)
8. Find all the customers from Atlantic region who have ever purchased ‘TABLES’ and the number of tables purchased (display the customer name, no_of_tables purchased)
9. Find all the customers from Ontario province who own Small Business. (display the customer name, no of small business owners)
10. Find the number and id of products sold in decreasing order of products sold (display product id, no_of_products sold)
11. Display product Id and product sub category whose produt category belongs to Furniture and Technlogy. The result should contain columns product id, product sub category.
12. Display the product categories in descending order of profits (display the product category wise profits i.e. product_category, profits)?
13. Display the product category, product sub-category and the profit within each subcategory in three columns.
14. Display the order date, order quantity and the sales for the order.
15. Display the names of the customers whose name contains the
i) Second letter as ‘R’
ii) Fourth letter as ‘D’
16. Write a SQL query to to make a list with Cust_Id, Sales, Customer Name and their region where sales are between 1000 and 5000.
17. Write a SQL query to find the 3rd highest sales.
18. Where is the least profitable product subcategory shipped the most? For the least profitable product sub-category, display the region-wise no_of_shipments and the profit made in each region in decreasing order of profits (i.e. region, no_of_shipments, profit_in_each_region)
→ Note: You can hardcode the name of the least profitable product subcategory



---------------------------------------------------------------------------------------------------------------------------------
Soluation
---------------------------------------------------------------------------------------------------------------------------------
create datebase Superstores;

use Superstores;

/** Import all the files from the forlers**/

SELECT * FROM superstores.cust_dimen;
SELECT * FROM superstores.market_fact;
SELECT * FROM superstores.orders_dimen;
SELECT * FROM superstores.prod_dimen;
SELECT * FROM superstores.shipping_dimen;

/*Identify and list the Primary Keys and Foreign Keys for this dataset provided to you(In case you don’t find either primary or foreign key, then specially mention this in your answer)*/

-- changing datatype in existing column
alter table market_fact modify column Cust_id varchar(100);

-- making primary key
alter table cust_dimen add constraint primary key (Cust_id);


-- 1. Write a query to display the Customer_Name and Customer Segment using alias name “Customer Name", "Customer Segment" from table Cust_dimen.
select Customer_Name as CustomerName, Customer_Segment as CustomerSegment from cust_dimen;

-- Write a query to find all the details of the customer from the table cust_dimen order by desc.
select * from cust_dimen order by Cust_id desc;

-- Write a query to get the Order ID, Order date from table orders_dimen where ‘Order Priority’ is high.
select Order_ID, Order_Date from orders_dimen where Order_Priority = "high";

-- Find the total and the average sales (display total_sales and avg_sales)
select count(sales) as total_sales, avg(sales) as avg_sales from market_fact;

-- Write a query to get the maximum and minimum sales from maket_fact table.
select max(sales) as max, min(sales)as min from market_fact;

/*Display the number of customers in each region in decreasing order of no_of_customers. 
The result should contain columns Region, no_of_customers.*/
select Region, count(*) as no_of_customers
from cust_dimen group by region order by no_of_customers desc;

-- Find the region having maximum customers (display the region name and max(no_of_customers)
select Region, count(Cust_id) as no_of_customers
from cust_dimen group by region order by no_of_customers desc limit 1;

-- Find all the customers from Atlantic region who have ever purchased ‘TABLES’ 
-- and the number of tables purchased (display the customer name, no_of_tables purchased)
select c.Customer_Name, count(*) as no_of_tables_purchased from 
cust_dimen c 
join 
market_fact m on c.Cust_id = m.Cust_id 
join 
prod_dimen p on m.Prod_id = p.Prod_id 
where c.Region = 'Atlantic' and p.Product_Sub_Category = "TABLES" group by c.Customer_Name;

-- Find all the customers from Ontario province who own Small Business.
-- (display the customer name, no of small business owners)
select Customer_Name, count(*) as no_of_small_business_owners from cust_dimen 
where Province = 'Ontario' and Customer_Segment ='SMALL BUSINESS' group by Customer_Name;

-- Find the number and id of products sold in decreasing order of products sold 
-- (display product id, no_of_products sold)
select Prod_id, count(*) as no_of_products_sold from market_fact 
group by Prod_id order by no_of_products_sold desc;

-- Display product Id and product sub category whose produt category belongs to Furniture and Technlogy. 
-- The result should contain columns product id, product sub category.
select Prod_id, Product_Sub_Category from 
prod_dimen where Product_Category in('FURNITURE' and 'TECHNOLOGY');

-- Display the product categories in descending order of profits
-- (display the product category wise profits i.e. product_category, profits)?
select p.product_category, sum(m.profit) as total_profit from market_fact m join prod_dimen p 
on m.Prod_id = p.Prod_id group by p.product_category order by total_profit desc;

-- Display the product category,
-- product sub-category and the profit within each subcategory in three columns.
select p.Product_Category, p.Product_Sub_Category, sum(m.profit) as total_profit 
from market_fact m join prod_dimen p 
on m.Prod_id = p.Prod_id group by p.Product_Category, p.Product_Sub_Category;

-- Display the order date, order quantity and the sales for the order.
select o.Order_Date, m.Order_Quantity , m.Sales 
from market_fact m join orders_dimen o on m.Ord_id = o.Ord_id;

-- Display the names of the customers whose name contains the
-- i) Second letter as ‘R’
-- ii) Fourth letter as ‘D’
SELECT Customer_Name FROM superstores.cust_dimen where 
Customer_Name like "_r%" and  Customer_Name like "___d%";

-- Write a SQL query to make a list with Cust_Id, Sales,
-- Customer Name and their region where sales are between 1000 and 5000.
select c.Cust_id, c.Customer_Name, c.Region, m.Sales 
from cust_dimen c join market_fact m on c.Cust_id = m.Cust_id
where  m.Sales >=1000 and m.Sales <=5000;

-- Write a SQL query to find the 3rd highest sales.
SELECT sales FROM market_fact order by sales desc limit 2,1;

-- Where is the least profitable product subcategory shipped the most? For the least profitable product sub-category, display the region-wise no_of_shipments and the profit made in each region in decreasing order of profits (i.e. region, no_of_shipments, profit_in_each_region)
SELECT c.Region AS Region, COUNT(m.Ship_id) AS `No of Shipments`, ROUND(SUM(m.Profit),2) AS Profit_in_each_region
FROM market_fact m 
JOIN cust_dimen c ON m.Cust_id = c.Cust_id
JOIN prod_dimen p ON m.Prod_id = p.Prod_id
WHERE p.Product_Sub_Category = (SELECT p.Product_Sub_Category 
FROM market_fact m 
JOIN prod_dimen p ON m.Prod_id = p.Prod_id
GROUP BY p.Product_Sub_Category
ORDER BY SUM(m.Profit)
LIMIT 1) GROUP BY c.Region ORDER BY SUM(m.Profit);
