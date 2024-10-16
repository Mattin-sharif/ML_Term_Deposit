# Banking on Behaviour: Predictive modelling for a Retail Banking Term Deposit Campaign

## Introduction and Background

In the dynamic landscape of retail banking, the understanding of customer preferences and behaviors stands as a significant factor for crafting effective marketing strategies. This report delves into a recent telephone marketing initiative undertaken by bank to target customers to subscribe to term deposits. Term deposits, explained by Investopedia, represent financial investments held at an institution for a predetermined period, providing a secure avenue for both the bank to garner stable funds and customers seeking reliable investment channels (Scholnick, 1999).

The dataset from this campaign, comprising 40,969 observations across 22 variables, emerges as a robust source of insights. Encompassing an array of factors - from client demographics to economic indicators, it offers an invaluable opportunity to distinguish the factors shaping customer investment decisions and shaping training materials for customer service representatives (Ilham et al., 2019).

Aligned with existing literature on customer behavior in financial services, this study hypothesizes several hypotheses. Rony (2021) underscore the significance of demographic factors in banking preferences, while de Lima Lemos et al. (2019) emphasize the impact of economic indicators on investment choices. Building upon these insights and latest research work by Qingyang (2023), our analysis scrutinizes five hypotheses:

H1 - Demographic Influence: Customer age significantly affects their likelihood of subscribing to term deposits.
H2 - Demographic Influence: Customer marital status significantly affects their likelihood of subscribing to term deposits.
H3 - Employment Influence: The occupation of clients is a key determinant in the subscription decision.
H4 - Loan Status: The presence of personal loans influences customer willingness to subscribe to term deposits.
H5 - Marketing Contact Efficiency: The method and frequency of contact during the marketing campaign play a significant role in the subscription decision.

Furthermore, the objective is to unravel the patterns and correlations within these factors, providing a data-driven foundation to enhance our understanding of customer behavior in the context of term deposits. This report will document the methodology, findings, and implications of this analysis, aiming to contribute valuable insights for the bank's strategic marketing endeavors (Rony (2021); de Lima Lemos et al. (2019)).

## Methodology

In this section, a comprehensive approach was undertaken in preparing and analysing the dataset to extract meaningful insights into customer subscription behaviour for term deposits. The methodology is structured into four key stages: Data Preparation, Exploratory Data Analysis (EDA), correlation analysis followed by Logistic regression modelling (Al-Jarrah et al., 2015).

### Data Preparation

The initial step in our analysis involved meticulous data preparation using the tidyverse package in R. The dataset, comprising 40,969 customer records and 22 variables, underwent rigorous cleaning and transformation. Essential functions such as mutate_if, select, and summary were employed to address issues like missing values, outliers, and data quality concerns. Categorical representation for relevant features was facilitated using the as.factor function to align with subsequent analytical requirements. Moreover, the target variable ‘subscribed’ was transformed into 0 for ‘no’ and 1 for ‘yes’, subsequently for better bivariate analysis later in the EDA. Variable ‘pdays’ was converted to categorical feature based on if the customer was contacted or not.
The summary of the data frame is a followed:

![image](https://github.com/user-attachments/assets/65fcd5d1-2bfc-4d6c-be23-ad11465c4071)

Figure 1: summary statistics after Addressing Data Quality Issues

### Addressing Data Quality Issues

A rigorous data quality check was conducted in R as addressing data quality concerns was essential to strengthen the dataset against biases and anomalies (Gupta et al., 2021). The base R functions, such as summary and boxplot, were instrumental in detecting and addressing outliers in the 'age' and ‘campign’ variables.

![image](https://github.com/user-attachments/assets/fcea811f-0f1b-44f4-b0a9-913949c3d8ae)

Figure 2 : Boxplot of Age

![image](https://github.com/user-attachments/assets/b14634b2-8864-4550-9766-a294d63bce61)

Figure 3: Boxplot of Campaign
The filter function from dplyr was employed to remove observations with missing values in 'marital_status,' enhancing dataset completeness.
![image](https://github.com/user-attachments/assets/2f853cc3-944a-46ef-8612-08fda8c27c7e)

Figure 4: summary Statistics of marital_status

Removal of the 'credit_default' and ‘previous_contracts’ variables were achieved using the select function, optimizing the model's generalizability. Additionally, potential overestimation concerns led to the exclusion of the 'contact_duration' variable. The dataset's integrity was further strengthen by addressing data quality issues, such as inconsistencies in the ‘month’ and ‘day_of_week’ variables, which were resolved and transformed into ordered factors

![image](https://github.com/user-attachments/assets/416b93b2-f201-460e-b76c-53566756026c)

Figure 5: Distribution of previous contract

### Exploratory Data Analysis (EDA)

Exploratory Data Analysis played a pivotal role in unravelling patterns and relationships within the dataset, facilitated by the ggplot2 library (Thanos, 2023). The ggplot2 function was extensively used for visualizations, including bar charts, histograms, and boxplots. Specifically, functions such as geom_bar, geom_histogram, and geom_boxplot were employed to visualize the distribution of variables, providing a visual narrative for hypothesis testing and model construction

### Visualization Techniques

Visualization emerged as a powerful tool in our analytical task, implemented using ggplot2 library (Ito, 2013). The facet_grid, and lab functions enriched the visual narratives, aiding in the interpretation and communication of complex patterns. Bar charts stacked bar charts, boxplots, and histograms provided nuanced descriptions of relationships between variables, and distribution of numerical features.

![image](https://github.com/user-attachments/assets/9d56ac19-0a3c-43c6-b055-25a52e6a1b26)

Figure 6: Distribution of education levels

![image](https://github.com/user-attachments/assets/921540ae-ed4e-4e8f-8737-0ca3c8ad71f7)

Figure 7: Distribution of Age

![image](https://github.com/user-attachments/assets/9168616a-a0c6-4986-b8f2-748852b9fd99)

Figure 8: Number of subscriptions per month

![image](https://github.com/user-attachments/assets/6890a631-b737-4fe4-b0d2-04c4ae328d02)

Figure 9: Day of week by lead status

![image](https://github.com/user-attachments/assets/619933ed-cd83-42be-ac14-7d8368143f21)

Figure 10: Subscription by occupation

![image](https://github.com/user-attachments/assets/cd5e36fb-4d33-4f0e-9749-25e2a72609c4)

Figure 11: Subscription by Housing loan

![image](https://github.com/user-attachments/assets/d88e48f8-d46d-49b7-927e-b02627474a75)

Figure 12: Subscription bt Personal loan

![image](https://github.com/user-attachments/assets/3995f9ce-f22c-4d34-bd4f-80379679fda5)

Figure 13: Subscription by Age

![image](https://github.com/user-attachments/assets/b83912ad-cc61-4d4f-843b-2316a04007ab)

Figure 14: Age distribution across different education levels and subscription

### Hypothesis Testing and Model Building

In this pivotal phase, statistical tests of correlation and association were leveraging to distinguish the relationships between various customer attributes and the likelihood of subscribing to term deposits. The Pearson's product-moment correlation test and Chi-squared tests were our tools of choice for quantifying associations and dependencies, respectively (Borugadda et al., 2021).

### Model Building Process:

#### Model 1:
![image](https://github.com/user-attachments/assets/764a1184-3a05-455c-bf8b-df1da7708bfa)

Figure 15: Logistic regression Model 1
Variables included: Age, Occupation, Marital Status, Campaign, and Personal Loan. Age accounts for varied responses across age groups, occupation for income and lifestyle differences, marital status for financial decisions, campaign interactions for assessing marketing success, and personal loans for their influence on financial decisions and subscription likelihood. These variables collectively provide insights into the dynamics affecting subscription outcomes in the dataset.

#### Model 2:
![image](https://github.com/user-attachments/assets/607639a7-ea96-4829-bdb4-278f04bbcab6)

Figure 16: Logistic regression Model 2
Additional variables: Housing Loan, Education Level, Contact Method, and Pdays (converted to categorical feature) are added. Model 2 underscores the impact of previous campaign outcomes, employment and loan variations, number of contacts, and timing of contacts on subscription success.

#### Model 3:
![image](https://github.com/user-attachments/assets/f9f01ba8-b171-4eb0-b593-da062b271d9c)

Figure 17: Logistic regression Model 3
Additional variables: Poutcome (outcome of the previous marketing campaign), Employment Variation Rate, Consumer Price Index, Euribor 3 Month Rate, Number of Employees, and Month are added.

#### Model 4:
![image](https://github.com/user-attachments/assets/4846b5df-ad3f-4d4c-b61f-ac294358d218)

Variable selection: For model 4, the variables were selected based on their perceived significance, leading to the exclusion of education, number of employees, housing loan, and personal loan.


### Model Evaluation and Assumptions

The assessment of our models extended beyond predictive performance, further investigating into assumptions underlying the best-performing model. A comprehensive suite of diagnostic tests was applied, including checks for multicollinearity, and the identification of influential points through measures like Cook's distance (Baker, 1997). The R code utilized stargazer for model comparison and evaluation metrics, while prediction accuracy was assessed through a confusion matrix and associated statistics. Assumption checking involved examining standardized residuals, Cook's distance, leverage values, and multicollinearity using variance inflation factors (VIF).


## Results and Discussion

### Correlation and Association Analysis
The hypotheses were tested using both Pearson's product-moment correlation and Chi-squared tests to determine the strength and significance of the relationships between various customer characteristics and their likelihood to subscribe to term deposits.
![image](https://github.com/user-attachments/assets/14842093-76b1-4df3-8cdc-4ce3ac714c29)

Figure 18: Correlation: Age and subscribed

Age Influence on Subscription Decision: Our first hypothesis theorised that customer age significantly affects their likelihood to subscribe to term deposits. The Pearson's correlation test revealed a statistically significant correlation (t = 5.9862, p-value = 2.166e-09). A positive correlation coefficient of 0.0296 indicated a modest, yet noteworthy, positive correlation between age and subscription likelihood. This result validate our hypothesis, suggesting that as customers' age increases, there is a slight uptick in their inclination to subscribe to term deposits. Therefore, the null hypothesis is rejected.
![image](https://github.com/user-attachments/assets/7b5fb65d-6ec0-43f3-b100-7b6c9c497290)

Figure 19: Causation: Marital_status and subscribed

Marital Status Impact: To examine the impact of marital status on subscription decisions, Chi-squared test was employed. The result, X-squared = 122.92, df = 3, p-value < 2.2e-16, signified a significant association. The distribution of subscription decisions across marital statuses was not uniform, rejecting the null hypothesis. This implies that marital status plays a noticeable role in shaping customer decision to subscribe to term deposit.
![image](https://github.com/user-attachments/assets/b1305ce3-764c-4db2-b01e-66557519ea03)

Figure 20: Causation: Occupation and subscribed

Occupation as a Determinant: Our third hypothesis suggested that the occupation of clients is a key determinant in the subscription decision. The Chi-squared test, X-squared = 959.69, df = 11, p-value < 2.2e-16, decisively affirmed this hypothesis. Occupation demonstrated a substantial association with subscription decisions, indicating that certain occupational categories are more inclined to subscribe compared to others.
![image](https://github.com/user-attachments/assets/9694351b-72ae-4824-b8f4-f5977e19a4ff)

Figure 21: Causation: Personal_loan and subscribed

Influence of Personal Loans: Whereas, our fourth hypothesis, which suggested that the presence of personal loans influences customers' willingness to subscribe, the Chi-squared test yielded a p-value of 0.6091, indicating no significant association. This result challenges our initial assumption, suggesting that the presence of personal loans does not significantly impact customers' decisions to subscribe to term deposits.
![image](https://github.com/user-attachments/assets/b267e751-4f1d-4e34-97fe-fa36ea34207e)

Figure 22: correlation: Contact and subscribed

Frequency of Contact during Campaign: For our fifth hypothesis, we explored whether the frequency of contact during the marketing campaign plays a significant role in subscription decisions. The Pearson's correlation test revealed a statistically significant negative correlation (t = -13.406, p-value < 2.2e-16), supporting our hypothesis. The negative correlation coefficient of -0.0662 indicates that increased contact during the campaign is associated with a lower likelihood of subscription.

### Logistic Regression Model Selection

![image](https://github.com/user-attachments/assets/dc220a07-c797-4a9d-af35-ed5a0094d776)
![image](https://github.com/user-attachments/assets/fcf6fb8d-b458-4f11-bb88-d217275fc636)
![image](https://github.com/user-attachments/assets/02857c89-3297-4e2a-b275-de688416efc2)
![image](https://github.com/user-attachments/assets/c142ebc8-43f9-4203-855a-7d98bc7990e2)


**Model 1:**
Focus: Basic demographic features and campaign variables. Findings: This model laid the foundation for our analysis, incorporating fundamental factors such as age and campaign-related features. While informative, its simplicity limited its ability to capture the complexity of customer behavior, prompting the exploration of additional variables in subsequent models.

**Model 2:**
Focus: Expanded to include loan statuses and education levels. Findings: The incorporation of personal loan and education variables aimed to enrich predictive capabilities. However, detailed analysis revealed that these additions slightly significantly enhance the model's accuracy - AIC value decreased from 22203 to 20259. Moreover, the results demonstrates that for our dataset, variables like personal_loan and educational_levels might not be the primary drivers of term deposit subscriptions.

**Model 3:**
Focus: Encompassed a broader array of socio-economic factors. Findings: With a more comprehensive set of predictors, including socio-economic variables, Model 3 aimed to capture a holistic view. Surprisingly, it outperform the previous models, emphasizing the importance of variable selection and suggesting that certain socio-economic indicators may strongly influence subscription outcomes in our context. Overall the AIC score dropped to 18248.

**Model 4:**
Focus: Maintained robustness while shedding non-significant predictors. Findings: The final selection, Model 4, showcased a refined set of predictors that achieved a balance between simplicity and informativeness. Notably, it slightly outperformed its predecessors in terms of fit and predictive power – AIC score 18198. This model's accuracy was further validated through assumption checks, affirming its adherence to multicollinearity, and influential points.

### Statistical Indicators:
**AIC**: Model 4 demonstrated lower AIC values, indicating better fit.

**Coefficients**: The coefficients of Model 4 showcased significant predictors, with occupation, marital status, campaign, contact method, and economic indicators playing pivotal roles.

**Observations**: All four models were tested on the same dataset, ensuring a fair comparison.

**P-values**: Throughout the models, variables with p-values above the threshold were systematically pruned in Model 4, enhancing interpretability without sacrificing statistical significance.


### Assumption Checks:
**Multicollinearity:** VIF values in Model 4 suggested minimal multicollinearity issues (Kumari, 2008), ensuring the independence of predictors. Whereas, emp_var_rate, cons_price_idx, and euribor_3m have very high VIF scores > 10, indicating they may be highly correlated with other variables in the model, which can distort and invalidate the model coefficients.

**Influential Points**: Cook's distance revealed no influential points that could unduly affect the model's stability.

**Standardized residuals check**: The result, 1461, indicates that there are 1461 cases in the training set where the standardized residuals are greater than 1.96. This could be a sign that those observations do not fit the model well, and may be outliers or influential points that could potentially affect the model's accuracy and assumptions. It is a diagnostic check to ensure that the model's predictions are reliable and the residuals are well-behaved (Verran and Ferketich, 1984).

### Model Accuracy Checks:
**Confusion Matrix and kappa statistics check:** The confusion matrix and statistics show the performance of a classification model (Krstinić et al., 2020). The model predicted 'no subscription' (0) 7104 times correctly and 'subscription' (1) 222 times correctly, in contrast it also incorrectly predicted 704 'no subscriptions' and 127 'subscriptions'. The model has high accuracy (89.81%) and a moderate kappa score (0.305) indicating a fair agreement. Sensitivity is high (98.24%) indicating that it is good at identifying 'no subscriptions', but specificity is low (23.97%). It highlights that it is not as good at identifying actual 'subscriptions'. The model's tendency to predict 'no subscription' is reflected in the high prevalence (88.65%). The Balanced Accuracy is 61.11%, which is an average of sensitivity and specificity. Moreover the results are also significant.

## Conclusions
Our comprehensive analysis highlighted the complex relationship between customer demographics, economic factors, and the tendency to subscribe to term deposits. Employing correlation analysis, logistic regression, and thorough validation of model assumptions. Here are the main conclusions:

### Key Findings:
Variable Influence: Customer age, marital status, and occupation were significant in predicting term deposit subscriptions (Qingyang, 2023). Notably, campaign contact frequency and economic indicators like the employment rate were also influential.

Model Efficacy: Among the models, Model_4 excelled in predictive power, indicating its suitability as a tool for guiding marketing strategies.

Correlation and Association: Statistically significant correlations and associations were identified, underpinning the nuanced relationship between customer characteristics and their subscription decisions. Therefore, hypothesis H1, H2, and H3 are accepted.

### Implications:
The significant variables identified should be at the forefront of creating targeted marketing campaigns.
Model_4's robustness indicates its potential as a decision-making aid for optimizing marketing efforts.

## Recommendations:
 Regular model updates with new data are recommended to maintain relevance and precision.
 Additional research into the identified significant variables could yield deeper insights, enhancing strategy formulation.


Limitations and Future Work:
 The analysis adheres to the assumptions of logistic regression, and deviations could affect model reliability.
 Future studies could explore machine learning techniques for potentially greater predictive accuracy (Qingyang, 2023).

In sum, this investigation lays a solid groundwork for understanding the factors affecting term deposit subscriptions, offering actionable insights for strategic marketing and customer engagement enhancements in the banking sector.




## References
 Al-Jarrah, O.Y., Yoo, P.D., Muhaidat, S., Karagiannidis, G.K. and Taha, K., 2015. Efficient machine learning for big data: A review. Big Data Research, 2(3), pp.87-93. ---level-
 Baker, E.L., 1997. Model-based performance assessment. Theory into practice, 36(4), pp.247-254
 Borugadda, P., Nandru, P. and Madhavaiah, C., 2021. Predicting the success of bank telemarketing for selling long-term deposits: An application of machine learning algorithms. St. Theresa Journal of Humanities and Social Sciences, 7(1), pp.91-108.
 de Lima Lemos, R.A., Silva, T.C. and Tabak, B.M., 2022. Propension to customer churn in a financial institution: A machine learning approach. Neural Computing and Applications, 34(14), pp.11751-11768.
 Gupta, N., Patel, H., Afzal, S., Panwar, N., Mittal, R.S., Guttula, S., Jain, A., Nagalapatti, L., Mehta, S., Hans, S. and Lohia, P., 2021. Data Quality Toolkit: Automatic assessment of data quality and remediation for machine learning datasets. arXiv preprint arXiv:2108.05935.
 Ilham, A., Khikmah, L., Indra, Ulumuddin and Bagus Ary Indra Iswara, I., 2019, March. Long-term deposits prediction: a comparative framework of classification model for predict the success of bank telemarketing. In Journal of Physics: Conference Series (Vol. 1175, p. 012035). IOP Publishing.
 Ito, K. and Murphy, D., 2013. Application of ggplot2 to pharmacometric graphics. CPT Pharmacometrics Syst Pharmacol. 2013; 2: e79.
 Krstinić, D., Braović, M., Šerić, L. and Božić-Štulić, D., 2020. Multi-label classifier performance evaluation with confusion matrix. Computer Science & Information Technology, 1.
 Kumari, S.S., 2008. Multicollinearity: Estimation and elimination. Journal of Contemporary research in Management, 3(1), pp.87-95.
 Qingyang, Chen., 2023. Interpretable Data Mining Approaches to Predict Term Deposits Subscriptions. BCP business & management, pp.44, 345-350
 Rony, M.A.T., Hassan, M.M., Ahmed, E., Karim, A., Azam, S. and Reza, D.A., 2021, December. Identifying Long-Term Deposit Customers: A Machine Learning Approach. In 2021 2nd International Informatics and Software Engineering Conference (IISEC) (pp. 1-6). IEEE.
 Scholnick, B., 1999. Interest rate asymmetries in long-term loan and deposit markets. Journal of financial services research, 16, pp.5-26.
 Singh, M., Dhanda, N., Farooqui, U.K., Gupta, K.K. and Verma, R., 2023, August. Prediction of Client Term Deposit Subscription Using Machine Learning Check for updates. In Proceedings of the 4th International Conference on Communication, Devices and Computing: ICCDC 2023 (Vol. 1046, p. 83). Springer Nature.
 Thanos, C., Meghini, C., Bartalesi, V. and Coro, G., 2023. An exploratory approach to data driven knowledge creation. Journal of Big Data, 10(1), pp.1-15.
 Verran, J.A. and Ferketich, S.L., 1984. Residual analysis for statistical assumptions of regression equations. Western Journal of Nursing Research, 6(1), pp.27-40.
