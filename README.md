# **Customer-Churn-Analysis**

Customer churn analysis is the process of identifying and understanding why customers stop using a company's products or services. This analysis is crucial for both retail and commercial segments as it helps businesses predict and mitigate customer churn, ultimately improving customer retention and profitability.

## **Key Components of Customer Churn Analysis**
1.	**Data Collection**: Gather data on customer behavior, transactions, and interactions. This can include purchase history, customer feedback, and engagement metrics.
2.	**Segmentation:** Divide customers into segments based on their behavior and characteristics. Common methods include the RFM (Recency, Frequency, Monetary) model and K-Means clustering
3.	**Churn Prediction:** Use statistical models and machine learning algorithms to predict which customers are likely to churn. This involves analyzing patterns and trends in the data
4.	**Root Cause Analysis:** Identify the reasons behind customer churn. This can involve analyzing customer feedback, market trends, and competitive actions.
5.	**Mitigation Strategies:** Develop strategies to retain customers. This can include personalized marketing, loyalty programs, improved customer service, and targeted promotions.

## **Benefits of Customer Churn Analysis**

•	**Improved Customer Retention**: By understanding why customers leave, businesses can take proactive steps to retain them.

•	**Cost Savings**: Retaining existing customers is often more cost-effective than acquiring new ones.

•	**Enhanced Customer Experience**: Identifying pain points allows businesses to improve their products and services.

•	**Informed Decision-Making**: Data-driven insights help businesses allocate resources more effectively and make strategic decisions.

## **The Impact of Customer Churn on Businesses**
Customer churn significantly impacts companies, especially Software-as-a-Service (SaaS) businesses, due to high customer acquisition costs. Churn affects Business-to-Business (B2B) and Business-to-Consumer (B2C) businesses differently, with B2C experiencing higher rates due to easier subscription changes. B2B churn is more impactful due to fewer, high-value customers. Churn can demoralize staff and distract from serving existing customers. There are two types of churn: voluntary (customer choice) and involuntary (external factors). Companies should measure churn rates regularly and use metrics like Customer Satisfaction (CSAT), Net Promoter Score (NPS), and Customer Effort Score (CES) to gauge customer satisfaction. Predictive and preventive churn models, survival analysis, and anomaly detection help forecast and mitigate churn. Reducing churn involves identifying at-risk customers, investing in customer success, providing excellent service, fair pricing, and strong loyalty programs. Artificial Intelligence (AI) can enhance churn management through better data analysis, predictive analytics, and improved customer support.

# **Maths Behind Customer Survival Analysis**

In survival analysis, the probability of surviving at least until time \( t \) is defined in terms of the probability density function \( f(t) \) and the cumulative distribution function \( F(t) \). The survival function \( S(t) \) is given by:

$$
Pr(T > t) = S(t) = 1 - F(t)
$$

### Hazard Functions:
- **Cumulative Hazard Function**: The cumulative hazard at time \( t \) is defined as:
  $$
  H(t) = -\ln(S(t))
  $$

- **Instantaneous Hazard Function**: The instantaneous hazard at time \( t \) is the derivative of the cumulative hazard:
  $$
  h(t) = \frac{dH(t)}{dt}
  $$
  Alternatively, it can also be expressed as:
  $$
  h(t) = \frac{f(t)}{S(t)}
  $$

### Likelihood Function:
The likelihood function for survival analysis is defined as:

$$
l(\beta) = \prod_{i=1}^{n} h(t_i)^{d_i} S(t_i)
$$

#### Key Components:
- **\( d_i \)**: A censoring indicator variable:
  - \( d_i = 1 \) if the event is observed for individual \( i \).
  - \( d_i = 0 \) if the event is censored for individual \( i \).
- **\( h(t_i) \)**: The hazard function for individual \( i \) at time \( t \).
- **\( H(t_i) \)**: The cumulative hazard for individual \( i \) at time \( t \).
- **\( S(t_i) \)**: The survival probability for individual \( i \) at time \( t \).

#### Interpretation:
- If \( d_i = 0 \) (censored), the contribution to the likelihood is the survival probability \( S(t) \).
- If \( d_i = 1 \) (event observed), the contribution is the density function \( f(t) = h(t)S(t) \).

### Log-Likelihood Function:
The log of the likelihood function is given by:

$$
\log l(\beta) = \sum_{i=1}^n \left[ d_i \log(h(t_i)) - H(t_i) \right]
$$

where \( \log \) is the natural logarithm.

### Notes:
- The likelihood function accounts for both observed events and censored data, making it a fundamental tool in survival analysis.
- The log-likelihood is often used for optimization and parameter estimation in survival models.


## **Kaplan-Meier method**

The Kaplan-Meier method calculates the probability of survival at time 𝑡  as:

$$ S(t) = \prod_{i=1}^{t-1} (1 - \frac{d_i}{n_i}) $$

where,
- 𝑆(𝑡) is the probability of survival until time 𝑡, 
- $𝑑_𝑖$  is the number of units that experienced the event at time 𝑡,  
- $𝑛_𝑖$  is the number of units at risk of experiencing the event at time 𝑡.  

$𝑛_𝑖$ decreases with time, as units experience the event or are censored. $\frac{d_i}{n_i}$ is the probability of experiencing the event at time 𝑖 and $(1− \frac{d_i}{n_i})$ is the probability of surviving at time 𝑖. 

Note that this method does not use any parameters, it only depends on the data on time and censoring.

# Method 2: Log-Rank Test

The **Log-Rank Test** is a non-parametric method used to compare survival curves between different groups. It assumes that the hazards of the groups are proportional. Under the null hypothesis, the probability of an event occurring is the same across all groups at every time point.

### Key Concepts:
- **Null Hypothesis**: The survival times of all groups come from the same distribution.
- **Test Statistic**: The log-rank test compares the observed number of events in each group to the expected number of events, proportional to the group size at each event time.

### Log-Rank Test Statistic:
For group \( j \), the test statistic \( k_j \) follows a \( \chi^2 \) distribution and is calculated as:

$$
k_j = \frac{(O_j - E_j)^2}{\text{var}(O_j - E_j)}
$$

where:
- \( O_j - E_j \) is the difference between the observed and expected number of events in group \( j \):
  $$
  O_j - E_j = \sum_i (o_{ij} - e_{ij})
  $$
- \( \text{var}(O_j - E_j) \) is the variance of the difference:
  $$
  \text{var}(O_j - E_j) = o_i \frac{n_{ij}}{n_i} \left(1 - \frac{n_{ij}}{n_i}\right) \frac{(n_i - o_i)}{(n_i - 1)}
  $$

#### Definitions:
- \( o_{ij} \): Observed number of events in group \( j \) at time \( i \).
- \( e_{ij} \): Expected number of events in group \( j \) at time \( i \), calculated as:
  $$
  e_{ij} = \frac{n_{ij}}{n_i} o_i
  $$
- \( n_{ij} \): Number of units at risk in group \( j \) at time \( i \).
- \( n_i \): Total number of units at risk across all groups at time \( i \).
- \( o_i \): Total observed number of events across all groups at time \( i \).

### Comparing Multiple Groups:
When comparing \( k \) groups:
1. Calculate pairwise log-rank test statistics for \( k-1 \) groups, forming a vector \( \mathbf{Z} \) with \( k-1 \) elements.
2. The test statistic for the hypothesis that there is no difference in survival times across \( k \) groups is:
   $$
   \text{logrankstatistic} = \mathbf{Z} \Sigma^{-1} \mathbf{Z}'
   $$
   where:
   - \( \Sigma^{-1} \) is the inverse of the \( (k-1) \times (k-1) \) variance-covariance matrix of \( \mathbf{Z} \).
   - The diagonal elements of \( \Sigma \) are the variances of \( k_j \).
   - The off-diagonal elements are the covariances \( \text{covar}(k_{jg}) \), calculated as:
     $$
     \text{covar}(k_{jg}) = o_i \frac{n_{ij} n_{ig}}{n_i^2} \frac{(n_i - o_i)}{(n_i - 1)}
     $$

### Interpretation:
- Rejecting the null hypothesis indicates that the survival times of the groups do not come from the same distribution.
- The test does not specify which group(s) differ.

### Applications:
The log-rank test is widely used to compare survival curves in medical research, engineering, and social sciences. A statistically significant log-rank test statistic allows us to reject the null hypothesis, suggesting differences in survival times across groups.
