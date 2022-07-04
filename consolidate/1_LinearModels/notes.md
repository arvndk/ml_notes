
- Decision Regions
- Overfitting
- Least squares regression (corresponding to sklearn LinearRegression in selfstudy 1)
- Linear discriminant analysis?
- Logistic Regression

Theory:
**Linear models** are used to predict the class of a data point. There are some commonly used models such as: **Logistic Regression, Linear Regression, SVC**... while K-Nearest Neighbors is an example of non-linear classification model.

<!-- Linear Regression is used to predict continuous values and Logistic Regression is used to predict discrete values. There is no point of having a decision boundary for a set of continuous values. That is why we don't talk about a decision boundary in Linear Regression. -->

**Decision regions** are a regions in the input space where the model is able to make a decision, each region corresponds to some class. So each region classifies 1 label for data points that are assigned to it.

From the first sight Linear models are mostly suited for binary classification problem however they can be used in multiple class classification problems too, by computing multiple linear algorithms and combining them together. There are generally two different approaches to this: 
 - one against all classification
 - one against one classification. 
Although this approach clearly helps classifying, it also creates those green areas where the classifiers completely disagree on the label, making the datapoints that land in those green areas unclassifiable.

One way to fix this is by learning **discriminant functions**. Instead of making the 3 classifiers agree on their results, we just take the ones that are the most accurate in that region. So even if there are results that don't match the classifier's output, it still rules that region because it classifies correctly, most of the time.

Regarding **overfitting**. Essentially overfitting is a symptom of too much training on the same data, meaning that the learned model is highly specialized to classify only the data in the training set. Overfitting is somewhat easy to spot as it results in very good accuracies for the training set, but increasingly bad accuracies for the test set. Beside, we also have underfitting which is ... #TODO

**Logistic Regression** is used when the target variable is categorical, like whether an email is spam or not. The idea is to find a relationship between featuers and probabilities of particular outcomes. The output will be a number between 0 and 1 using sigmoid. The point is to find a **decision boundary**, which is the threshold used to categorize the datapoints. We are using **one hot encoding** to encode the categorical variables. When training, we find the best weights for the linear model within logistic regression. This is done based on a cost function (LogLoss) where we minimize the function which is optimized using gradient descent.

**Linear Regression** assumes a linear relationship between the input variable and the output variable. When training, a linear equation is fitted to the observed data, where the loss is lowest, for example least square error. This, calculated the best-fitting line by minimizing the sum of squares of the vertical deviations from each point to the line. The optimal score is 0, and it is squared to cancel out between positive and negative values.

**The least square regression** finds the hyperplane by reducing the sum of the squared error as much as possible. The method has some limitation:
 - it is unreliable when data is not evenly distributed
 - it is sensitive with the data set contains some outliers, this can skew the hyperplane made by this method.


<!-- TODO -->
<!-- 
**K-nearest neighbor** assumes similar things exists in close proximity. 
- As K is decreased, predictions become less stable. A low k can also lead to overfitting
- As K is increased, predictions becomes more stable due to majority voting/averaging. I can however become too large and lead to underfitting.
Using the euclidean distance, we consider the k nearest neighbors, and that a point will be the same class as the majority of those. To avoid tiebreaks, avoid even k values.

**The least squares regression**  is the error function, that tries to minimize the classification error. The least square error has some problems, if the data set contains some outliers. As can be seen here. Least squares regression is not optimal for this kind of dataset.
 
A **linear discriminant function** is a function where the decision surfaces are hyperplanes.
-->
**Notebook_01**

The dataset iris was used, which a dataset with 3 classes which are types of iris plants. Three linear models were used in the self study as well as the non-linear classifier **K-nearest neighbor**.

- KNN we see that the decision boundaries are somewhat horizontal lines through the space, which splits the classes into different decision regions. When K is low we can that there can be small regions of a class inside other regions because it only considers few neighbors. This makes it fit more to the training data, but is probably overfitting, and could perform bad on test data. With a high K value it may be computationally expensive and may also be underfitting because it can fit to to outliers.

- Linear Regression shows the three linear decision boundaries, which have no overlap in the decision regions, this will result in as we can see these intersecting hyperplanes, as each hyperplane only is fitted on the single class. It seems not as good as KNN. It misclassifies a bunch of the blue points.

- Logistic Regression shows the three linear decision boundaries, each nicely dividing the data. Log reg is usually used for binary classification problem.

- SVC: generally looks a lot like the log reg. 

For the next exercise we do 70% 30% split, for the train and test set.
This is to compare the accuracy of the KNN and linear regression models.

From this we can see tha the KNN has an accuracy:
KNN Train accuracy 0.9428571428571428
KNN Test accuracy: 0.9333333333333333

and the linear regression has an accuracy:
Linear Regression Train accuracy 0.7904761904761904
Linear Regression Test accuracy: 0.6444444444444445

Here it is clear that the KNN is better than the linear regression.

We can see very clearly from the confusion matrix for linReg. on the test set it has some clear difficulties on class:1 (blue), where it classifies a significant portion as class:2 (green), we can scroll up and we can also see very clearly from the decision boundaries on the train set, why this is happening.

table of confusion matrix for logReg:
 [[ 9  0  0]
 [ 2  5 13]
 [ 0  1 15]]

 For the next exercise we ran the same experiment on all four features in the dataset the results were that both were generally better than with only two.

 <!-- TODO where is notes for notebook 2? -->