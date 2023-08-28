# **Airline Customer Segmentation Based on LRFMC Model Using K-Means**
- Tools: Python
- Dataset: Rakamin Academy
- TODO Notebook: [View](https://github.com/faizns/Airline-Customer-Segmentation-LRFMC-Model-using-KMeans/blob/4655776d6d4c07363ad286a7bc065a85f3b7a55f/Airline-Customer-Segmentation-LRFMC-Model-using-KMeans.ipynb)

---

## 📂 **Introduction**
### Problem Statement
- With the expansion of airline networks, competition among airline companies has intensified. Common issues in this industry include **customer attrition** and a decrease in competitiveness.
- In the era of information, marketing focus has shifted from being *product-based* to **customer-based**. One approach is **customer segmentation**, allowing airlines to differentiate high-value and low-value customers and provide personalized services and marketing strategies for each group. The goal is to **maximize profits** by effectively allocating resources.

### Objectives
1. Perform customer **segmentation** using airline customer data based on the LRFMC Model using K-Means.
2. Analyze the **characteristics** of each resulting cluster.
3. Provide **business insights** based on the analysis.

---

## 📂 **Exploratory Data Analysis**
### Dataset
- The dataset contains 62988 rows and 23 features (**15 numerical, 8 categorical**).
- There are **7.51% missing values** (WORK_PROVINCE, WORK_CITY, SUM_YR_1, AGE, SUM_YR_2, WORK_COUNTRY).
- No **duplicate data** is present.

### Summary
- Most features are **positively skewed**, with mean > median.
- Outliers are present in all numerical features.
- There are **0 values** in features such as EXCHANGE_COUNT, avg_discount, Points_Sum, Point_NotFlight, SUM_YR_1, SUM_YR_2, AVG_INTERVAL, and MAX_INTERVAL.
- About **77%** of airline customers are **male**.
- The majority, **92%**, of customers are from **China**.
- About **29%** are from **Guangdong province** and **15%** are from **Guangzhou city**.

## 📂 **Pre-processing**
### Handling Missing Values
- Based on observations, there are anomalous values of 0 in ticket prices (SUM_YR_1, SUM_YR_2), avg_discount, and total distance traveled (SEG_KM_SUM) that are greater than 0. **Data with empty or 0 ticket prices might be due to customers not having flight history**. Such data points are removed.
- Irrelevant, negligible, and redundant features are removed, such as MEMBER_NO, WORK_CITY, WORK_PROVINCE, WORK_COUNTRY, AGE, GENDER.
- After these steps, the remaining missing values are reduced to 1.1%, and the remaining data points with missing values are dropped.

### Feature Selection
- The LRFMC model is used for customer segmentation. L stands for loyalty, R for recency, F for frequency, M for monetary, and C for category (discount). These factors are used to segment customers based on their loyalty, travel frequency, monetary spending, and discount usage. Six features related to the LRFMC model are selected: **FFP_DATE, LOAD_TIM, FLIGHT_COUNT, AVG_DISCOUNT, SEG_KM_SUM, LAST_TO_END**.
- The specific calculation method is as follows:
- todo [Insert Table 1 – Feature Calculation based on LRFMC]


### Handling Outliers
- Outliers are managed using the **Interquartile Range (IQR)** method.
- todo [Insert Figure 2 – Distribution of LRFMC Features After Removing Outliers]

### Feature Standardization
- Standardization is performed using the **StandardScaler** to ensure all features have comparable scales.
- todo [Insert Figure 3 – Distribution of LRFMC features after Standardization]

## 📂 **Modeling**

### Finding Optimal K
The K-Means algorithm is a clustering method based on centroids (clustering centers). Enter the number of clustering K and the database containing N data objects, and output K-clusters that meet the minimum standard error sum of squares.

To determine the optimal number of clusters in the dataset, a K-cluster analysis was performed using the Elbow Method and Silhouette Plot.

- todo [Insert Figure 4 – Elbow Method Graph with Distortion Score]

Based on the Elbow Method and Silhouette Plot, the optimal K value is determined to be **5**.

- todo [Insert Figure 5 – Silhouette Plot Graph]

Based on the results of the Silhouette Plot, it shows K omptimal 5. To determine the optimal K value in the Silhouette Plot, two factors can be considered, namely the average coefficient is as large as possible, but still smaller than the maximum score for each cluster member, and considering cluster thicknesses that are similar to one another. The thickness of this cluster indicates a balanced composition.

### Result
After finding the optimal K, the K-Means model is fitted with **n_clusters=5**, and dimensionality reduction is performed using **PCA**. The resulting clusters are visualized in the following graph:

- todo [Insert iFigure 5 – Clustering of Customer Segmentation]


## 📂 **Interpretation**
### Percentage of Customers
- todo [Insert Figure 6 – Percentage of Total Customers for Each Cluster]

The highest percentage of customers is in **cluster 3** with **25.96%**, and the lowest is in **cluster 0** with **16.10%**.

### Analysis of Cluster Characteristics Based on LRFMC
[Insert Figure 7 – Cluster Patterns and Characteristics based on LRFMC]

[Insert Table 2 – Cluster Feature Evaluation and Analysis]

**Interpretation and Recommendations:**
1. Cluster 0 - **Hibernating**
    - Customers who have been members for a moderate duration but do not use the airline frequently, with low frequency and monetary values and high recency.
    - **Business Recommendation:**
         - Send "We Miss You" email marketing to these customers, offering special vouchers or discount codes for upcoming flights within a specified time frame.
...

2. Cluster 1 - **Loyal Customers**
    - Customers who have been long-time members and have moderate flight activity, moderate recency, and usage of the airline.
    - **Business Recommendation:**
         - Send "Thank You for Flying with Us" emails and provide voucher/discount codes for their next flights.
         - Provide loyalty points/rewards for each airline booking that can be redeemed for discount vouchers or affiliated products.

3. Cluster 2 - **Potential Loyalists - The Champions**
    - Customers with very high flight activity and long distances traveled. They have the potential to contribute significantly to the company's revenue. They also have low recency and have been members for a considerable time.
     - **Business Recommendation:**
         - Build a strong customer relationship through onboarding support, such as providing a Flight Booking Assistant.
         - Provide souvenirs or merchandise.
         - Offer discounts for purchasing multiple flights at once.
         - Provide special discounts/rewards for flying with friends.
         - Provide points/rewards for each airline booking.

**References**
[1] Tao, Y.: Analysis Method for Customer Value of Aviation Big Data Based on LRFMC Model. ICPCSEE 2020, CCIS 1257. 89-100(2020)
[2] Wang, P. & Chen, T.: Data Value Mining: A Case Study of Airline Customer Data. IJRES 2022, 05-13(2022)
[3] [https://clevertap.com/blog/rfm-analysis/](https://clevertap.com/blog/rfm-analysis/)
[4] [https://www.moengage.com/blog/rfm-analysis-using-rfm-segments/](https://www.moengage.com/blog/rfm-analysis-using-rfm-segments/)

