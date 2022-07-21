> # **Bank Marketing Campaign**

---
# **Business Problem and Data Understanding**
---
## **Define Business Problem**

### **Context**

Bank or Financial services experienced a dramatic change in terms of technology, strategy, and customer service due to globalization of economics. This situation challenge every banking sector to adopt the emerging technologies and applied them in their internal business. Its also mean how those banking sectors can use the technology in embracing their customers. 

One of technology-enabled marketing practice that many of banking sector applied these days called telemarketing.


>***Telemarketing*** : *is a direct marketing strategy method in which a salesperson acquires the prospective customer's willingness to purchase products or services over phone calls.*

In simply way, the bank embrace the customer through phone calls and offer their products. Those campaigns activity usually carried out by the marketing department or Customer Care & Telemarketing.

We must keep in mind that every campaign that were carried out are inseparable with operational costs. The effectiveness and efficiency of these activities will certainly affect operational costs. And this is the main concern for every banking sector : minimize/maintain the cost in order maximize the gain.

Portuguese Bank is one of the banking sector that are experiencing the same concern. They offering the client's to place a term deposit through telemarketing. But there has been a revenue decline and would like to know what actions to take.

Zeta Squad as the Bank's DS team has an important task to find out the root cause and provide appropiate recommendations in order to increase the revenue.

### **Problem**

**> Problem Stakeholder : Portuguese Bank**


From Portugal bank data, we found out that only few customer opened term deposits (appx. 11% of total customer that contacted by the marketing teams). This is one of the reasons why the decline in revenue occurred. We can see that there might be a campaign failure in the process. This indicate that the campaign didn't inline with the targeted customer. Which also mean that the bank marketing teams has not effectively delivered the right campaigns to the right customers. They did the same campaign to every single customers without did the selection first (which most likely to open the deposit & not open the deposit). This behaviour leads to several problems :

- For corporate business:
    - Waste of time, human resources, and operational costs for unsuccessful telemarketing activities.
    - Loss of potential customers because wasted resources should be used for more potential consumers.

- For Customers:
    - Consumers are annoyed with junk phones.

    ### **Goals**

**> Goals Stakeholder : Zeta Squad**

It would be better and effective if the bank marketing teams know which customers that most likely interested in opening a deposit, so they can maximized the resource and minimized the loss.

Our goal is:
1. Create a machine learning model to predict customers who most likely make deposits, so that banks can maximize campaigns that are carried out. Our target is to create a machine learning with good performance to predict customer's choice.

2. Find out which factors that can influence a customer's decision to make a deposit or not, so that banks can create more effective campaigns.

### **Analytics Approach**

These are the following steps that will be performed to complete the task:

In this analysis we want to see the tendency of customers to subscribe a term deposit by doing a machine learning analysis and evaluate the model performance through ROC-AUC Score. 

![Confusion_Matrix](https://github.com/PurwadhikaDev/ZetaSquadTeam_JC_DS_VL_05_FinalProject/blob/main/Images/Confusion%20Matrix.png)


<br>True Negative (TN)  | Actual(0) & Predict(0):
<br>The model predicts that the consumer will not make a deposit, and the customer does not. 
<br>True Positive (TP)  | Actual(1) & Predict(1): 
<br>The model predicts that the consumer will make a deposit, and the customer does. 
<br>False Negative (FN) | Actual(1) & Predict(0): 
<br>The model predicts that the customer will not make a deposit, however the customer does make a deposit. 
<br>False Positive (FP) | Actual(0) & Predict(1): 
<br>The model predicts a deposit even if the consumer does not make a deposit.

Therefore, we try to suppress the False Positive (FP) Score of the Confusion Matrix to improve the telemarketing efforts.

## **Data Understanding**
#### Data Source
Dataset Source: https://www.kaggle.com/datasets/volodymyrgavrysh/bank-marketing-campaigns-dataset which the data modified from [Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014

#### Dataset Description
The data is related with direct marketing campaigns of a Portuguese banking institution. The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed.
- Data Set Characteristics: Multivariate
- Attribute Characteristics: Real
- Associated Tasks: Classification
- Number of Instances: 41188
- Number of Attributes: 21
- Missing Values: coded as **'unknown'**
- Area: Business
- Dataset period: from May 2008 to November 2010

#### Attributes Information
Input variables:
- Bank client data:
  1. `age` (numeric)
  2. `job` : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')
  3. `marital` : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
  4. `education` (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
  5. `default`: has credit in default? (categorical: 'no','yes','unknown')
  6. `housing`: has housing loan? (categorical: 'no','yes','unknown')
  7. `loan`: has personal loan? (categorical: 'no','yes','unknown')

- Related with the last contact of the current campaign:
  8. `contact`: contact communication type (categorical: 'cellular','telephone')
  9. `month`: last contact month of year (categorical: 'mar' to 'dec')
  10. `day_of_week`: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
  11. `duration`: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.

- Other attributes:
  12. `campaign`: number of contacts performed during this campaign and for this client (numeric, includes last contact)
  13. `pdays`: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
  14. `previous`: number of contacts performed before this campaign and for this client (numeric)
  15. `poutcome`: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')

- Social and economic context attributes:
  16. `emp.var.rate`: employment variation rate - quarterly indicator (numeric)
  17. `cons.price.idx`: consumer price index - monthly indicator (numeric)
  18. `cons.conf.idx`: consumer confidence index - monthly indicator (numeric)
  19. `euribor3m`: euribor 3 month rate - daily indicator (numeric)
  20. `nr.employed`: number of employees - quarterly indicator (numeric)

- Output variable (desired target):
  21. `y` - has the client subscribed a term deposit? (binary: 'yes','no')

---
# **Exploratory Data Analysis**
---

[Dashboard_1](https://public.tableau.com/app/profile/monika.pangestu/viz/Zeta-EDAPresentationVer_/Dashboard1?publish=yes)
![Dashboard_1](https://github.com/PurwadhikaDev/ZetaSquadTeam_JC_DS_VL_05_FinalProject/blob/main/Images/Dashboard%201.png)

- The percentage of people who does the deposit (11%)  are lower than the people who doesn’t (89%)
- Single & divorce category have more percentage of deposit customer than the married category (single deposit : 13.65%, married deposit : 10.10%, divorced deposit : 10.41%). It’s probably due to customer with single status has less living expenses compared to the other two categories.
- Most of the customer have personal loans & housing Loan, there are about 46% of total customers


[Dashboard_2](https://public.tableau.com/app/profile/monika.pangestu/viz/Zeta-EDAPresentationVer_/Dashboard1a)
![Dashboard_2](https://github.com/PurwadhikaDev/ZetaSquadTeam_JC_DS_VL_05_FinalProject/blob/main/Images/Dashboard%201a.png)

- The job vs age boxplot displays that despite of the most customers are in prime working age, the median of all job classes are generally above 40yo (except the student class). It means that the bank targeted more on experience workers instead of entry level workers. It’s probably that telemarketer perceives experience workers has more money and tend to subscribe to deposits.
- Based on call durations boxplot, it can be seen where customers who are interested in opening a deposit spend time 50% longer (median > 6mins) on the phone compared to those who are not interested (median < 4mins).



[Dashboard_3](https://public.tableau.com/app/profile/monika.pangestu/viz/Zeta-EDAPresentationVer_/Dashboard2a)
![Dashboard_3](https://github.com/PurwadhikaDev/ZetaSquadTeam_JC_DS_VL_05_FinalProject/blob/main/Images/Dashboard%202a.png)
- From the charts and table above, it can be seen that the top 3 deposit rate based on job class are student, non-worker (mostly retiree) and admin. It is also supported by the age group variable where early working age and elderly have the highest deposit rate, 21.9% and 45.9% respectively. 
- The previous campaign rate also illustrate the resemblance output with the current campaign. From the table we can see that telemarketer did not continue targeting the highest deposit rate from previous campaign but instead reaching admin, blue-collar and technician where they have low deposit rate. We can infer that telemarketer has false perception on customer’s market target. 


---
# **Data Processing**
---

Taking a closer look, we see that some of the following characteristics have little bearing on the effectiveness of the marketing effort: 
- The `default` variables: It is related to binary credit in default categories and has too many unknown data (20% of all data) to be dropped. Meanwhile, the data of this variable are imbalance where 3 data as non-default and the rest are default. Instead of removing samples, this variable will be excluded for further processing.
- The `contact` variable is deleted since the contact method (cellular, telephone, and unknown) provides no useful information. 
- The `duration` variable will be excluded from modeling process since we are intending to predict the potential customer prior the calling.

On the other hand, the new variable that created (`campaign_reps`, `pdays_class` & `age_group` as in categorical variable) will be utilized to replace `campaign`, `pdays`, and `age` which was numerical variable. To help achieve this aim, the following important columns are included in a new subset.

## Model Selection

CV Score ROC_AUC	                                    Mean ROC_AUC	SDev
Model			
XGBoost	            [0.808, 0.797, 0.793, 0.796, 0.784]	 0.795521	  0.007763
Logistic Regression	[0.788, 0.775, 0.775, 0.768, 0.77]	 0.775084	  0.006964
Random Forest	    [0.744, 0.754, 0.757, 0.749, 0.745]	 0.749982	  0.004970
Decision Tree	    [0.62, 0.622, 0.619, 0.621, 0.595]	 0.615219	  0.009985

<br>ROC_AUC Score
<br>Model	
<br>Random Forest	0.633011
<br>Decision Tree	0.629247
<br>XGBoost	0.614783
<br>Logistic Regression	0.573347

Between 4 models candidate, XGBoost, LogReg, and Random Forest have relatively similar ROC_AUC score. Nevertheless, Random Forest has the lowest deviation score (0.004) compared to others.

Based on the benchmark result, XGBoost has the highest mean cross validation score approximately around 79%. However, Random Forest has the highest ROC-AUC score on test set 63%. Therefore, Random Forest will be used for further processing according test set score. 

## **Imbalance Treatment**

Since the target (`deposit`) consists of yes (11%) and no (88%), it indicates imbalance data. It will affects on model's prediction. Moreover, we want to surpress the False Positive prediction as it can damaging the Bank's profit on deposits. Therefore, imbalance treatment will be applied. This project will implement Random Over Sampling and Random Under Sampling for imbalance treatment based on Random Forest model as it has the highest benchmark score.

No Treatment
<br>[[6698   99]
<br> [ 644  208]]
<br>Random Forest_NoTreat ROC-AUC Score :  61.5 %
<br>Random Forest_NoTreat CV Mean Score :  0.749


Random Over Sampling
<br>[[5890  907]
<br> [ 482  370]]
<br>Random Forest_ROS ROC-AUC Score     :  65.0 %
<br>Random Forest_ROS CV Mean Score     :  0.969


Random Under Sampling
<br>[[5002 1795]
<br> [ 268  584]]
<br>Random Forest_RUS ROC-AUC Score     :  71.1 %
<br>Random Forest_RUS CV Mean Score     :  0.759

## Hyperparameter Tuning

Obtaining Best Model for RandomForest
<br>Best Parameters:  {'model__max_depth': 8, 'model__max_features': 'sqrt'}
<br>Best Scores:  0.7912778385657774

<br>ROC AUC Score Default Random Forest :  0.7106794560704427
<br>ROC AUC Score Tuned Random Forest   :  0.744451173225415

After tuning, the ROC-AUC score slightly increase from 71% becoming 74%. Therefore, we will used tuned Random Forest model for final model.

## **Modeling with Best Parameters and Selected Features**

<br>ROC AUC Score Default Random Forest :  0.71
<br>ROC AUC Score Tuned Random Forest   :  0.74
<br>ROC AUC Score Select Random Forest  :  0.75

# **Conclusion**

Below a guide in assesing our model:
* 0.9 - 1.0 = excellent
* 0.8 - 0.9 = good
* 0.7 - 0.8 = fair
* 0.6 - 0.7 = poor
* 0.5 - 0.6 = fail
<br> Source: [Model Scoring](https://medium.com/@sardina.aleigha/bank-marketing-a-classification-exercise-fd9b77a1da4d)

Our model has fair performance as we obtain 0.75 of ROC-AUC score. On Bank's Marketing Campaign, between False Positive (FP) and False Negative (FN), we want to suppress the prediction on FP. Because higher FP value means we predict the customer will subscribe to a deposit but in actual they don't. Having this condition the telemarketer will waste more resource on non-prostective customers. Not only do we lost the profit but also it becomes a burden for operational cost.
Why we not focused on minimize the False Negative (FN)? FN means that we predict the customer not do the deposit but they actually do the deposit, this didnt give any loss for business. Why ? Because at last they do the deposit, and we dont use any marketing cost to make them do the deposit.

On the otherhand, based on confusion matrix output, our model can reduce the FP class from 1795 customers to 848 customers. This mean we can reduce up to +50% of the big loss operational business cost and efficiency can be reach. For example :

* FP  Simulation Default
<br>Total Customer = 2000 persons
<br>Total FP = 1795 persons
<br> Marketing cost = 1 /persons
<br> Revenue = 10 /persons
<br> Total marketing Cost : 1 * 2000 = 2000
<br> Total Revenue = 10 * (2000-1795) = 2050
<br> Total Profit = 2050 - 2000 = 50

* FP Simulation After Feature Selection
<br>Total Customer = 2000 persons
<br>Total FP = 848 persons
<br> Marketing cost = 1 / persons
<br> Revenue = 10 / persons
<br> Total marketing Cost : 1 * 2000 = 2000
<br> Total Revenue = 10 * (2000-848) = 11,520
<br> Total Profit = 11520 - 2000 = 9,520

As following example, we can see that there are big efficiency & effectiveness if we suppress the FP

# **Recommendation**

The following are some significant factors that should be prioritized in order to increase campaign success rates: 

- Loan & Balance: We discovered that many term deposit subscribers were loan-free. There are also those who have a loan but have not subscribed to the deposit, as well as those who do not have a loan but have not signed to the deposit. The primary reason for this is balance. Those with a sufficient amount are more likely to subscribe to a term deposit. 

- Contacts: Based on our findings, the majority of customers that subscribe to deposit have had contacted less than six time. Hence, contacting someone more than six times should be avoided.

- Jobs: Targeting students, non-workers, or admin will result in more success. Furthermore, the data revealed that those with employment professions such as blue-collar, entrepreneur, services, house-maid, and so on had a very low favorable reaction. Contact with such persons should be avoided, or at the very least, other aspects such as balance, debt, and education should be considered before addressing them. Overall, this component should be used in conjunction with education. 

- Education is a minor yet crucial thing to consider. According to our findings, there are many subscribers with a strong educational background. We feel that an intelligent person with some understanding of investing will take some extra time to understand the offer presented.

- We can also adding another related features such as saving balances
