**1. Count Total Records**



**Question:**



How many records are available in the dataset?



**SQL Query:**



select count(\*) from ecommerce;



**Output:**



count

248089



**Query Explanation:**



This query counts the total number of rows in the Ecommerce table using COUNT(\*). It provides a quick overview of dataset size and helps verify that the data has been loaded correctly before performing further analysis.





**2. Find Duplicate Records**



**Question:**



Are there any duplicate transactions in the dataset?



**SQL Query:**



select \*, count(\*)

from ecommerce

group by invoice, stockcode, description, quantity, invoicedate, invoicetime, price, customerid, country, revenue, category

having count(\*) > 1;



**Output:**



invoice	stockcode	description	quantity	invoicedate	invoicetime	price	customerid	country	revenue	category	count

NULL	NULL	NULL	NULL	NULL	NULL	NULL	NULL	NULL	NULL	NULL	34166



**Query Explanation:**



This query groups all transaction-level columns and counts occurrences of each unique combination. The HAVING COUNT(\*) > 1 condition filters only duplicate records. This helps in identifying data quality issues and ensures accuracy in further analysis.





**3. Total Revenue**



**Business Question:**



What is the total revenue generated from sales transactions?



**SQL Query:**



SELECT

&#x20;   ROUND(SUM(Revenue), 2) AS Total\_Revenue

FROM Ecommerce

WHERE Category = 'Sales';



**Output:**



total\_revenue

4001425.59



**Query Explanation:**



This query calculates total revenue by summing the Revenue column for records where Category = 'Sales'. The ROUND() function formats the result to two decimal places for cleaner reporting.





**4. Monthly Revenue Trend**



**Business Question:**



How has revenue changed over time on a monthly basis?



**SQL Query:**



SELECT

&#x20;   DATE\_TRUNC('month', InvoiceDate)::DATE AS month,

&#x20;   SUM(Revenue) AS monthly\_revenue

FROM Ecommerce

WHERE Category = 'Sales'

GROUP BY 1

ORDER BY 1;



**Output:**



month	monthly\_revenue

01-12-2009	798329.56

01-01-2010	612447.42

01-02-2010	538109.67

01-03-2010	762105.98

01-04-2010	646690.93

01-05-2010	643742.03



**Query Explanation:**



This query uses DATE\_TRUNC('month', InvoiceDate) to group revenue by month. It then sums revenue for each month and orders the results chronologically, allowing analysis of trends, seasonality, and growth patterns over time.





**5. Revenue by Country**



**Business Question:**



Which countries generate the highest revenue?



**SQL Query:**



SELECT

&#x20;   Country,

&#x20;   ROUND(SUM(Revenue),2) AS Revenue

FROM Ecommerce

WHERE Category='Sales'

GROUP BY Country

ORDER BY Revenue DESC;



**Sample Output:**



country	revenue

United Kingdom	3431300.05

EIRE	163127.79

Netherlands	114223.5

Germany	73115.06

France	49714.62

Denmark	37389.34

Sweden	30789.41

Spain	14859.4

Switzerland	13263.62

Channel Islands	9198.39



**Query Explanation:**



This query aggregates revenue at the country level using GROUP BY Country. The results are sorted in descending order to highlight the top-performing markets.





**6. Top 10 Products by Revenue**



**Business Question:**



Which products generate the highest revenue?



**SQL Query:**



SELECT

&#x20;   Description AS Product,

&#x20;   ROUND(SUM(Revenue),2) AS Revenue

FROM Ecommerce

WHERE Category='Sales'

GROUP BY Description

ORDER BY Revenue DESC

LIMIT 10;



**Output:**



product	revenue

WHITE HANGING HEART T-LIGHT HOLDER	76210.86

REGENCY CAKESTAND 3 TIER	31020.08

ASSORTED COLOUR BIRD ORNAMENT	26466.23

PARTY BUNTING	25350.01

JUMBO BAG RED WHITE SPOTTY 	25024.12

DOOR MAT UNION FLAG	20747.04

TEA TIME CAKE STAND IN GIFT BOX	18622.36

EDWARDIAN PARASOL NATURAL	18559.29

EDWARDIAN PARASOL BLACK	17602.17

ENGLISH ROSE DESIGN QUILTED THROW	17227.96



**Query Explanation:**



This query groups data by product description and calculates total revenue for each product. It then sorts the results in descending order and returns the top 10 products. This helps identify best-performing products and supports business decision-making.





**7. Pareto Analysis (80/20 Rule)**



**Business Question:**



Which products contribute the majority of total revenue?



**SQL Query:**



WITH ProductRevenue AS

(

&#x20;   SELECT

&#x20;       Description,

&#x20;       SUM(Revenue) AS Revenue

&#x20;   FROM Ecommerce

&#x20;   WHERE Category='Sales'

&#x20;   GROUP BY Description

),



RunningRevenue AS

(

&#x20;   SELECT

&#x20;       Description,

&#x20;       Revenue,



&#x20;       SUM(Revenue) OVER

&#x20;       (

&#x20;           ORDER BY Revenue DESC

&#x20;       ) AS Cumulative\_Revenue,



&#x20;       SUM(Revenue) OVER () AS Total\_Revenue



&#x20;   FROM ProductRevenue

)



SELECT

&#x20;   Description,

&#x20;   ROUND(Revenue,2) AS Revenue,

&#x20;   ROUND(Cumulative\_Revenue,2) AS Running\_Revenue,



&#x20;   ROUND(

&#x20;       (Cumulative\_Revenue/Total\_Revenue)\*100,

&#x20;       2

&#x20;   ) AS Cumulative\_Percentage



FROM RunningRevenue

ORDER BY Revenue DESC;



Sample Output:



description	revenue	running\_revenue	cumulative\_percentage

WHITE HANGING HEART T-LIGHT HOLDER	76210.86	76210.86	1.9

REGENCY CAKESTAND 3 TIER	31020.08	107230.94	2.68

ASSORTED COLOUR BIRD ORNAMENT	26466.23	133697.17	3.34

PARTY BUNTING	25350.01	159047.18	3.97

JUMBO BAG RED WHITE SPOTTY 	25024.12	184071.3	4.6

DOOR MAT UNION FLAG	20747.04	204818.34	5.12

TEA TIME CAKE STAND IN GIFT BOX	18622.36	223440.7	5.58

EDWARDIAN PARASOL NATURAL	18559.29	241999.99	6.05

EDWARDIAN PARASOL BLACK	17602.17	259602.16	6.49

ENGLISH ROSE DESIGN QUILTED THROW	17227.96	276830.12	6.92



**Query Explanation:**



This analysis uses two CTEs. The first calculates total revenue per product. The second uses window functions to compute cumulative revenue and total revenue across all products. Finally, the cumulative percentage is calculated to identify how a small number of products contribute to a large portion of total revenue, following the Pareto Principle.





**8. Average Revenue per Customer**



**Business Question:**



What is the average revenue generated per customer?



**SQL Query:**



SELECT



&#x20;   COUNT(DISTINCT CustomerID) AS Total\_Customers,



&#x20;   ROUND(

&#x20;       SUM(Revenue) /

&#x20;       COUNT(DISTINCT CustomerID),

&#x20;       2

&#x20;   ) AS Avg\_Revenue\_Per\_Customer



FROM Ecommerce



WHERE Category='Sales';



**Output:**



total\_customers	avg\_revenue\_per\_customer

2685	1490.29



**Query Explanation:**



This query calculates total revenue and divides it by the number of distinct customers. It provides a high-level metric of customer value across the dataset.





**9. High-Value Customers**



**Business Question:**



Who are the top revenue-generating customers?



**SQL Query:**



SELECT



&#x20;   CustomerID,



&#x20;   ROUND(SUM(Revenue),2) AS Revenue,



&#x20;   COUNT(DISTINCT Invoice) AS Orders



FROM Ecommerce



WHERE Category='Sales'



AND CustomerID IS NOT NULL

&#x20;

AND CustomerID <> 'Unknown'



GROUP BY CustomerID



ORDER BY Revenue DESC



LIMIT 10;



**Output:**



customerid	revenue	orders

18102	154566.35	45

14646	105343.13	31

14156	102500.47	39

13694	96414.76	69

14911	49573.96	56

17511	36307.7	        10

15311	35085.04	68

13902	34023.26	5

15061	31248.08	31

16754	29864.98	14



**Query Explanation:**



This query filters out missing or unknown customers, then calculates total revenue and number of orders per customer. The results are sorted in descending order of revenue to identify the top 10 high-value customers.





**10. RFM Customer Segmentation**



**Business Question:**



How can customers be segmented based on purchasing behavior?



**SQL Query:**



WITH max\_date AS (

&#x20;   SELECT MAX(InvoiceDate) AS max\_dt

&#x20;   FROM Ecommerce

),



rfm AS (

&#x20;   SELECT

&#x20;       CustomerID,



&#x20;       (SELECT max\_dt FROM max\_date) - MAX(InvoiceDate) AS recency,

&#x20;       COUNT(DISTINCT Invoice) AS frequency,

&#x20;       SUM(Revenue) AS monetary



&#x20;   FROM Ecommerce

&#x20;   WHERE Category = 'Sales'

&#x20;   GROUP BY CustomerID

),



scored AS (

&#x20;   SELECT \*,

&#x20;       NTILE(5) OVER (ORDER BY recency DESC) AS r\_score,

&#x20;       NTILE(5) OVER (ORDER BY frequency) AS f\_score,

&#x20;       NTILE(5) OVER (ORDER BY monetary) AS m\_score

&#x20;   FROM rfm

)



SELECT \*,

CASE

&#x20;   WHEN r\_score >= 4 AND f\_score >= 4 AND m\_score >= 4 THEN 'Champions'

&#x20;   WHEN r\_score >= 4 AND f\_score >= 3 THEN 'Loyal Customers'

&#x20;   WHEN r\_score <= 2 AND f\_score >= 4 THEN 'At Risk'

&#x20;   WHEN r\_score = 5 THEN 'New Customers'

&#x20;   ELSE 'Others'

END AS segment

FROM scored;



**Sample Output:**



customerid	recency	frequency	monetary	r\_score	f\_score	m\_score	segment

16887	180	1	219.82	1	2	2	Others

14865	180	1	31.2	1	1	1	Others

16763	180	1	352.85	1	2	2	Others

17804	180	1	124.95	1	1	1	Others

17984	180	1	212.63	1	2	2	Others

13748	180	1	173.1	1	1	1	Others

17592	180	1	148.3	1	1	1	Others

14654	180	1	246.86	1	2	2	Others

15362	180	1	310.75	1	2	2	Others

17056	180	1	128.6	1	1	1	Others





**Query Explanation:**



This query performs RFM analysis using multiple CTEs. It first determines the most recent transaction date, then calculates:



Recency: days since last purchase

Frequency: number of orders

Monetary: total revenue



It then applies NTILE(5) window functions to score each metric and classifies customers into segments such as Champions, Loyal Customers, At Risk, New Customers, and Others. This helps in understanding customer behavior and designing targeted retention strategies.

