# Credit_Risk_Analysis

## Overview of the analysis
Through this analysis it is expected to use and compare the different sampling models available to preprocess the financial data given to us and combine it with logistic regression model, as well as use ensemble models, as to conclude which of them fits better our data and find the reasons why it does. This information will be a big help as it will help the client decide on whom to give service and trust. So, ultimately it helps reduce risk.

## Results
The data given to us was passed through the ETL process as it should, so all the data points used for the analysis is as pure as it can get. No null values or empty columns, the information contained was formatted as it should and finally it was separated in features and target. We will validate the models after three performance metrics: the accuracy score, the recall (sensitivity) and precision scores. The accuracy is based of the difference between the predicted values and the actual values, precision is a measure of how reliable a positive classification is and recall or sensitivity is a measure of how many positive values are predicted correctly. The F1 Score is also useful as it serves as a sinlge summary statistic of precision and sensitivity, it can detect a pronounced imbalance between sensitivity and precision by a low F1 score.

# Resampling models: 
For this results a different model was used in each, as a part of preprocessing, a balancing method as to have the same amount of the target outcomes possibilities and try to not have a bias to either one. This is done either by trying to get more data for the target with least information (oversampling) until it has tha same amount as the one with the most data or by condensing the data points from the target that has the most to the same level of the of the with the least (undersampling) or by doing both to the same data.

**Oversampling**
* Random Oversampling: 

![Random_over_sampler](https://user-images.githubusercontent.com/110573146/219883882-3ad43000-87c0-4ba7-b462-ced3db3703cd.png)

* SMOTE Oversampling:

![SMOTE](https://user-images.githubusercontent.com/110573146/219883890-7ae97771-f845-4bb5-9f58-242048f8213a.png)

**Undersampling**
* Cluster centroids:

![Cluster_centroids](https://user-images.githubusercontent.com/110573146/219883895-a63afeac-ce7a-4b43-8bf4-f002b68d7e91.png)

**Combination (Over and Under) Sampling**
* SMOTEENN:

![SMOTEENN](https://user-images.githubusercontent.com/110573146/219883902-bf8d1b7b-a72a-467a-bbef-55b221a2a2f4.png)


# Ensemble models:
The next results are product of a different model than Logistic Regression (linear), as these are more focused on alternatives and paths to take to get a final conclusion on the target. Another difference is that for this models no preprocessing was done like resampling or scaling.

* Balanced Random Forest Classifier:

![Balanced_Random_Forest](https://user-images.githubusercontent.com/110573146/219884518-80762a20-db0c-4cf5-9a2b-d0c6ee48daed.png)

* Easy Ensemble AdaBoost Classifier:

![Easy_Ensemble](https://user-images.githubusercontent.com/110573146/219884522-9ebcd7c9-7b22-438d-8e0a-c575063ee46d.png)

# Summary: 
Summarize the results of the machine learning models, and include a recommendation on the model to use, if any. If you do not recommend any of the models, justify your reasoning.

To correctly choose a model it is necessary to take a look into their scores (accuracy, recall, precision and f1), to only have the attention on one of this these would be a mistake as all them tell different characteristics about the model and how it relates to the data. In first instance we could look into the accuracy score as it tells us a sumary of the predicted values against the expected values. From there we can take a deeper look into the oter scores as to get a better conclusion.

The accuracy scores in descending order:
1. Easy Ensemble Classifier (0.91)
2. Balanced Random Forest Classifier (0.77)
3. SMOTE (0.64) 
4. Random Over Sampler (0.63)
5. SMOTEENN (0.62) 
6. Cluster centroids (0.58)

From these results we then take a look into the recall and precision scores through the F1 values. We will take a look into the top 3 models in accuracy scores as the the other should not be considered as they have less than 64% of correct prediction and using them may result more harmful for our client rather than helpful.

+ For SMOTE the f1 value for high_risk is of 0.02 while for low_risk is of 0.84, this means that there is not a balance between the sensitivity and the precision for the value of high_risk and looking further into the results precision has a score of 0.01 and recall of 0.56, so it is confirmed that there is indeed imbalance. This model should also not be considered for the job as it is not precise as their high_risk predictions will most likely be false. 

+ For Balanced Random Forest Classifier the accuracy is that of 0.77, so it has more reliabilty and based on the context of the situation and the application it could do one could argue it is enough to be used, so that is why we have to compare it with others and dig deeper as to choose the best fit. The f1 value for the high_risk is of 0.05 while for low_risk is 0.94, again the low_risk is higher and the high_risk warns of an imbalance between precison (0.03) and recall (0.65) which again brings the same problem as the SMOTE, the high_risk predictions it makes will most likely be a mistake.

+ Lastly Easy Ensemble Classifier has the best accuracy score of all (0.91) and for some it would be more than enough to use this score as a "ready to go" but we have to analyze it to be sure. The f1 score for high_risk is of 0.14 and for low_risk of 0.97, indeed the high_risk score is the highest but it is not high enough yet. As the precision score is of 0.07 while the recall is of 0.86, so in other words this algorithm is not useful also for the same reason the other two.

After fully analysis it has been determined to not use any of the models showed in these codes as they all show an imbalance between precision and recall, one may argue that in this situation a high recall value and a low precision value over the high_risk classification may not be bad as if a person was considered high_risk when it should not be then the bank would not suffer that much but I would say that yes they have suffered a potentially lost forever a honest and loyal client, so this is why checking the f1 score is also a good idea as to have an idea of these imbalances. So in the end any of the models will predict all high_risk classifications correct but it cannot differentiate the ones that are not, so it would be as if it classifies all values as high_risk, te low precison tells us we cannot trust the reliability of the high_risk classification. 
