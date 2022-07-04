## Manfred - 02 - Linear Models
- Maximum margin hypeplanes
- Feature transformations and kernel functions
- The kernel trick
- String kernels

**THEORY**
**Support Vetor Machines (SVM)** is a classification machine learning model which aims to find the **Maximum margin hyperplanes** in an N-dimensional space (where N is the number of features) that distinctly classifies the datapoints, i.e the maximum distance between datapoints of both classes and this is done by considering the dot products of support vectors and the samples.

Hyperplanes made up the decision boundary that help classify the datapoints. Datapoints falling on either side of the hyperplane can be attributed to different classes. The dimensionality of the hyperplane depends on the number of features, if the input feature is 2, then the hyperplane is just a line. If the number of features is 3, then the hyperplane has two dimension.

The **Maximum margin hyperplane** is a hyperplane that separates the data into two classes.
The intuition behind this is that the larger margin the hyperplane can have between to two different classes the more accurate the model is. So essentially when deciding the best line to make we simply need to maximize the distance to each class. There are data points in both classes whose distance to the hyperplane equals the margin. These are
the support vectors of the hyperplane.

Support vectors are datapoints closer to the hyperplane and influence the position and orientation of the hyperplane. Using these support vectors, we maximize the margin of the classifier. Deleting the support vectors will change the position of the hyperplane.

If the data is not linearly separable, SVM need feature transformation and kernel function to deal with data which is not linearly separable
 - **Feature transformation** adds another dimension to the dataset, making it a higher dimensional dataset. The transformation can also be called the data mapping into features space. After feature transformation, if the data become linearly separable, we can simply apply maximum margin hyperplane to classify data. In practical, finding a convenient function to perform feature transformation is tricky and it can be very computational expensive if input data is already at high dimension. To overcome this, we can use the **kernel function** and the **kernel trick** as alternative to feature transformation.

 - **kernel function** is equal to the dot product of the transformed vectors. This function allows us to create a non-linear hyperplance. A kernel function must satisfy Mercers theorem, which demans that the kernel should be a symmetric continuous function. There are several kind of kernel functions, ex: polynomial, Gaussian and tangent... (they work on numerical data) **string kernel** function is designed to work on non-numerical data, it counts the frequency of the words in the text.
 - **kernel trick** makes it possible to represent the data only through a set of pairwise similarity comparisons between the original data in the low dimensionality, instead of applying the transformation, and representing the data in a higher dimensional feature space.


**Notebook 3**
In the first exercise we are only using 3 and 7 from the MNIST dataset. So it is a binary classification. The data data is split into training and test sets. The training set is used to train the model and the test set is used to test the model. In this self study use the MNIST data set to do character recognition using a Support Vetor Machines (SVM).

We test with different kernels and observed
    **Linear kernel** had an accuracy of 0.98 on the test set. 
    **Polynomial kernel** had an accuracy of 0.99 on the test set. 
    **Gaussian (rbf) kernel** had an accuracy of 0.99 on the test set. 
    **Sigmoid kernel** had an accuracy of 0.96 on the test set. 
The accuracies and training time are all around the same.

When it is not possible to separate data in a low dimensionality, additional dimensions are added by feature transformation. This enables us to separate the data linearly, but when operations are performed with higher dimensions, this can lead to extremely high and impractical computation costs, especially if many dimensions are added.

This is what the kernel trick solves. The trick is that kernel methods represents the data only through a set of pairwise similarity comparisons between the original data in the low dimensionality, instead of applying the transformation, and representing the data in a higher dimensional feature space.

The benefit is that the objective function we are optimizing to fit the higher dimensional decision boundary only includes the dot product of the transformed vectors. Therefore we can just substitute these dot product terms with the kernel function without using $\phi(x)$, meaning we find the optimal hyperplane using the hither dimensional space, without having to calculate or in reality eve know anything about $\phi(x)$.

Now we try to training on the whole dataset with the gaussian kernel. The accuracy is 0.98. The training time is around 104 seconds. So the training time is naturally much larger. Here we have a confusion matrix, where we can see what each class was classified as. We can for example see that 20 9s was classified as 4s and 17 were classified as 7s.

In exercise 2, we create our custom convolution kernels, by taking the dot product between the X and Y. With this kernel an accuracy on the test set of 0.98 is achieved.