**E-commerce Sales and Customer Analytics**







**Project Description**



This project analyzes online retail transaction data to understand sales performance, customer behavior, and product trends. The objective is to generate actionable business insights that help improve revenue performance, customer retention strategies, and product decision-making.





**Objectives**



**The main objectives of this project are:**



* Analyze overall sales performance and revenue trends over time
* Identify key countries and products contributing to business growth
* Perform product-level analysis to understand revenue concentration using Pareto Analysis
* Analyze customer value through revenue contribution and purchasing behavior
* Segment customers using RFM (Recency, Frequency, Monetary) analysis
* Identify opportunities to improve customer retention and support targeted marketing strategies





**Dataset Information**



Source: Kaggle Online Retail II UCI Dataset

Size: 1000000+ rows and 8 columns

Columns: Invoice, Stock Code, Description, Quantity, Invoice Date, Price, Customer ID and Country.



The original dataset covers a two-year period (December 2009 – December 2011). For this analysis, a continuous six-month period (December 2009 – May 2010) was selected to ensure efficient processing and focused analysis, resulting in approximately 200,000+ transaction records.



**The analysis focuses on:**



* Products
* Sales transactions
* Discounts
* Postage
* Returned/cancelled transactions



**The following categories were excluded from the analysis:**



* Administrative
* Inventory loss
* Financial charges
* Gift vouchers



Customer IDs are anonymized identifiers from the publicly available dataset. No personally identifiable customer information is included.





**Data Source**



Data Source: Online Retail II UCI Dataset — Kaggle



Publisher: Miyabon



License: CC0: Public Domain



Note: Attribution not required under the license; credit provided as a professional courtesy.





**Tools Used**



SQL | Microsoft Excel | Power BI





**Data Cleaning Process**



**The following data preparation steps were performed:**



Removed records with missing values in critical fields.

Replaced missing values in supporting fields with "Unknown" where applicable.

Removed duplicate records using a unique key created from Invoice, Stock Code, Quantity, and Price.

Standardized data formats for consistency.

Checked for invalid values, outliers, and data quality issues.

Applied text normalization and case standardization.





**Data Transformation**



**New calculated fields were created to support analysis:**



Invoice Time — extracted time-based information from invoice dates.

Revenue — calculated as Quantity × Price.

Category — created for product-level analysis.





**Analysis Performed**



**The following analyses were conducted:**



**Sales Performance Analysis**



* Calculated total revenue generated during the analysis period.
* Analyzed monthly revenue trends to identify seasonal patterns.
* Compared revenue contribution across countries.



**Product Performance Analysis**



* Identified top-performing products by revenue.
* Performed Pareto Analysis to determine products contributing to 80% of total revenue.
* Evaluated product concentration and key revenue drivers.



**Customer Behavior Analysis**



* Calculated total unique customers and average revenue per customer.
* Identified high-value customers based on revenue contribution.
* Performed RFM analysis to segment customers into groups such as:

&#x20;  1. Champions

&#x20;  2. Loyal Customers

&#x20;  3. At Risk Customers

&#x20;  4. New Customers





**Key Insights**



* The business generated approximately £4.0 million in revenue from 2,685 unique customers during the six-month analysis period.
* Average revenue per customer was approximately £1,490, highlighting the value of existing customers.
* Sales peaked in December 2009, indicating strong seasonal demand, followed by lower revenue in early 2010 and recovery in March 2010.
* The United Kingdom was the dominant revenue market, contributing the majority of total sales.
* Revenue was concentrated among a smaller group of products, with approximately 24.2% of products contributing 80% of total revenue.
* Customer segmentation identified a strong base of Champions and Loyal Customers, while also highlighting At Risk customers requiring retention strategies.





**Recommendations**



**Based on the analysis, the following recommendations were identified:**



* Continue strengthening customer retention strategies in the UK market.
* Explore growth opportunities in international markets such as EIRE, Netherlands, and Germany.
* Prioritize high-performing products in merchandising and product strategy.
* Use customer segmentation to create personalized marketing campaigns.
* Develop loyalty initiatives for Champions and Loyal Customers.
* Launch targeted win-back campaigns for At Risk customers.
* Plan marketing activities around seasonal demand patterns.





**Dashboard Access**



The Power BI dashboard file (.pbix) is available upon request. Preview screenshots are included in this repository.





**Conclusion**



This project demonstrates how sales and customer transaction data can be transformed into actionable business insights. Through revenue analysis, product performance evaluation, and RFM customer segmentation, the analysis identifies key revenue drivers, customer segments, and opportunities for business improvement.



The findings highlight the importance of focusing on high-performing products, strengthening customer relationships, and using data-driven strategies to support sustainable business growth.

