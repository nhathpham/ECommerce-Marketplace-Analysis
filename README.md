# Brazilian-ECommerce-Analysis
An Analysis of Order Ratings, Reviews, Sales, and Customer Relationship on a Brazilian E-Commerce Website

<h2>Problem Introduction: </h2>
- In the past few years, the growth of online marketplaces and digital marketing has generated a high volume of data on consumer behaviors and e-commerce products. Analyzing this data would provide enterprises with insights into better business decisions. Here, we work with data from Olist, a Brazilian department store platform that connects small merchants to customers1. With Brazil being the largest e-commerce market in Latin America2 , our analysis attempts to help Olist leverage their data resources to raise their service quality, optimize business strategies, and attract more customers.<br />

- The datasets are provided by Olist on Kaggle.com3. It contains anonymized records of 100k orders made on the platform from 2016 to 2018. Data is divided into eight tables, each with specific aspect like orders, products, sellers, and customers. As seen from the database schema (Figure 1), each observation on the main orders data table represents one order, and using other datasets, we can connect those orders to gain additional information on order status, product attributes, price, freight, type of payments, location of sellers and buyers, reviews written by customers, and much more.<br />

![Brazilian_ECommerce_Analysis_Proposal](https://user-images.githubusercontent.com/87089936/143927648-f652469f-7ab8-462a-bc5f-f0cc5a034e94.jpg)

-The project aims to develop a comprehensive, multi-level analysis that includes:<br />
(1) Machine learning models to explore different features of an order that would impact review scores<br />
(2) Forecast of monthly sales volumes by product category<br />
(3) Customer segmentation analysis based on churn probability, and machine learning models to classify customers into categories based on their buying behavior<br />
(4) Sentiment analysis of product reviews (textual data) to discern customer’s preferences, likes and dislikes<br />

<h2>Proposed plan: </h2>
- Data processing: Due to the nature of the data with eight tables composed of over 600k rows; we cleaned and loaded each table into an Amazon Web Services MySQL instance (Figure 1) to ensure the data is consistent among all members of the group during the project. Some tables provided were not in our desired format or tidy and therefore required pre-processing to ensure the accuracy of data loaded into our database.<br />

- Data visualization and modeling: We will use pandas and NumPy to tidy and preprocess the data, and scikit-learn to train a logistic model to predict a “negative” or “positive” review score given a variety of engineered features such as delivery time, freight value, price. We will find the most important feature by plotting input feature weights on bar plot using matplotlib and seaborn. For the sentiment analysis, we will use Natural Language Toolkit (NLTK) to preprocess the text data and perform predictive analysis using logistic regression. We will create bar plots using seaborn to visualize the impact of each word on the review score. For the customer segmentation analysis, we will quantitatively rank customers based on their Recency, Frequency, Monetary (RFM) values, and use K-Means Clustering to segment customers based on their purchasing habits.<br />

- Anticipated challenges:<br />
o Product order data is imbalanced, with 57.7% of total orders having 5-score ratings and 11.5% having 1-score ratings. This will cause biases to machine learning models and impact correlation between features. We will combine and relabel 1,2,3 scores as “negative” scores and 4,5 scores as “positive” scores and utilize over-sampling/under-sampling to deal with class imbalance.<br />
o Since data is available for a 2-year timeframe only (Oct 2016-Sept 2018), it will be difficult to verify and forecast seasonality in sales. To address this, we will look at month over month trends instead of year over year trends.<br />
o Limited data on returning customers (3.3% of all customers) and on orders with multiple products (3.6% of all orders) will make it difficult to analyze buyer's behavior for clustering and recommendation tasks. We will look at a variety of customer characteristics such as geolocation and spending and perform different segmentation methods to create a more holistic analysis.<br />
<h2>Preliminary results: </h2>
- When assessing the relationship between review scores and delay of order deliveries (Figure 2), we observe that most orders were delivered on time or early across different review scores. However, the proportion of orders with delay among orders with review score 1 is higher than that among orders with higher scores. This indicates a strong relation between an order’s review score and order’s delivery delay, where a delay is likely to result in a “negative” review. The graph of average review scores by delivery time (number of days from time of purchase to delivery) shows that orders with longer delivery have lower review scores, strengthening the reasoning that deliver time strongly impacts customer experience.<br />

![Brazilian_ECommerce_Analysis_Proposal2](https://user-images.githubusercontent.com/87089936/143927647-5d58f4f7-eb21-4d03-a616-8723f0ed1b9b.jpg)


- Historical sales data showed some upward trend with an extreme jump at the end of November 2017, which was a Black Friday. As can be seen in Figure 4, of the top 3 product categories (based on order volumes) have different seasonality, but all generally recorded a surge in sales during some major holiday periods in Brazil (New Year, Independence Day (Sept 7), Mother’s Day (2nd Sunday of May), Free-shipping Day (last Friday of April))4. Based on this information, we will create a separate model for each product category and sum it up for overall sales forecast.<br />

![Brazilian_ECommerce_Analysis_Proposal3](https://user-images.githubusercontent.com/87089936/143927646-16facb66-5cd9-4d83-a14d-c90405807577.jpg)

![Brazilian_ECommerce_Analysis_Proposal4](https://user-images.githubusercontent.com/87089936/143927644-26350426-9a12-4a69-b338-0afc52f6dd9a.jpg)
