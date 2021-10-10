# Credit_Risk_Analysis

## Overview of the Analysis

The purpose of this analysis was to use multiple machine learning models to predict credit risk.  According to the management, credit risk is inherently unbalanced and "good" loans significatly outnumber "bad" loans.  As a result, this analysis used different techniques, models, and libraries to eveluate the data.  We used **imbalanced-learn** and **scikit-learn** libraries as the backbone of our models that were used to evaluate the credit risk.

## Results
As mentioned, credit risk data is unbalanced, so a variety of machine learning models were employeed to assist in evaluating the data.  First, we **OverSampled** the data using **RandomOverSampler** and **Smote** algorithms.
### **RandomOverSampler**
"In random oversampling, instances of the minority class are randomly selected and added to the training set until the majority and minority classes are balanced."
The original data had 68,470 "Low_Risk" entries, and only 347 "High_Risk" entries.  RandomOverSampler balanced these entries out (to 51,352 each) by creating random data to fill in for the undersampled portion of the data.  The following are the results.

![image](https://user-images.githubusercontent.com/85403978/136662479-4acce2ea-5f67-49f6-9d8d-328af745fd73.png)
![image](https://user-images.githubusercontent.com/85403978/136662575-7aea94dc-f290-4c67-9aac-e440681f6387.png)

The Balanced_Accuracy_Score in this model is 64.28% which is fairly low.  Also, looking at the Classification_Report, we can see that the Precision (Pre) and the Recall (rec) are high for the "low_risk" and low for the "high_risk."  Perhaps this model isn't the best for our predictions.  There are other models to choose from.

### **Synthetic Minority Oversampling Technique (SMOTE)**

"The synthetic minority oversampling technique (SMOTE) is another oversampling approach to deal with unbalanced datasets. In SMOTE, like random oversampling, the size of the minority is increased. The key difference between the two lies in how the minority class is increased in size."

![image](https://user-images.githubusercontent.com/85403978/136664176-2e5b1de3-f03c-41ee-ae85-0923e2f54980.png)

The Balanced_Accuracy_Score is even lower in this model at 62.01%.  Also, looking at the Classification_Report, we can see that the Precision (Pre) has remained the same as the RandomOverSampler, but the Recall (rec) has gone down. Perhaps this model also isn't the best for our predictions.
____________________________________________________________________________________________________________________________________________________________________

Next, we **UnderSampled** the data using **ClusterCentroids**.
"Undersampling takes the opposite approach of oversampling. Instead of increasing the number of the minority class, the size of the majority class is decreased." "Cluster centroid undersampling is akin to SMOTE. The algorithm identifies clusters of the majority class, then generates synthetic data points, called centroids, that are representative of the clusters. The majority class is then undersampled down to the size of the minority class."

![image](https://user-images.githubusercontent.com/85403978/136664660-78ab1118-98bd-4b46-9525-53cc63d64485.png)

In this situation, instead of having a balanced number of entries at 51,352, the entries are still balanced, but there are only 260.  The results did not improve.  The Balanced_Accuracy_Score went down to 51.03%.  And, while the precision score remained the same, the recall decreased further.  Again, probably not the best model.
____________________________________________________________________________________________________________________________________________________________________

Moving on, we use a combination of Over and Under Sampling **SMOTEEN**.  
"SMOTEENN combines the SMOTE and Edited Nearest Neighbors (ENN) algorithms. SMOTEENN is a two-step process; Oversample the minority class with SMOTE, and Clean the resulting data with an undersampling strategy. If the two nearest neighbors of a data point belong to two different classes, that data point is dropped."

![image](https://user-images.githubusercontent.com/85403978/136698524-efb33122-0826-4da6-a9e7-a3649af468b3.png)

In this situation, there are slightly more entries in the "high_risk" category, but the accuracy continues to be low at only 51.03%, and the recall continues to get worse.

____________________________________________________________________________________________________________________________________________________________________

Finally, we run the same data through **Ensemble Learners**. The first of these Ensemble Learners is Balanced_Random_Forest_Classifier. "A balanced random forest randomly under-samples each boostrap sample to balance it."  "Bootstrap aggregation, or "bagging," is an ensemble learning technique that combines weak learners into a strong learner."

![image](https://user-images.githubusercontent.com/85403978/136699070-734e50d8-38b3-4204-9878-dd968cdff808.png)

A better performance than the other models.  The accuracy score is back up to 78.78% and the recall is higher.  Perhaps the best model for the client to use, so far.  But, we also have the EasyEnsembleClassifier to consider.

"The Easy Ensemble involves creating balanced samples of the training dataset by selecting all examples from the minority class and a subset from the majority class. Rather than using pruned decision trees, boosted decision trees are used on each subset, specifically the AdaBoost algorithm."

![image](https://user-images.githubusercontent.com/85403978/136699360-d0e3f2f7-d442-4d6d-865d-92dcea56f71f.png)

## **Summary**

This method has proved to be the best model of them all.  The balanced_accuracy_score is the best at 92.54%, and both the precision and recall scores are the best at .99 and .94 respectively.  These results show that this is the best model for the client to consider.
____________________________________________________________________________________________________________________________________________________________________
**Sources**

Class module 17

https://machinelearningmastery.com/bagging-and-random-forest-for-imbalanced-classification/ 

https://imbalanced-learn.org/stable/references/generated/imblearn.ensemble.BalancedRandomForestClassifier.html


