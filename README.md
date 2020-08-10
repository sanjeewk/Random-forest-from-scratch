# REPORT

We are using **random forest algorithm** for the implementation in this assignment.

Random forest falls under Supervised Learning. It is a method that operates by constructing
multiple decision trees during training phrase. The decision of the majority is chosen by the
random forest algorithm as the final decision.
We wrote two codes for two datasets with the same core algorithm for random forest.

Given below are the details on the implementation of the algorithm:

**Decision Tree algorithm** : It breaks down our data by making a decision based on asking a
series of questions.

## Train Algorithm:

- First make a function to calculate the entropy which is the measure of randomness in a given dataset.

- Create a data structure class Node to assign initial default values in def __init__
- Create a class DecisionTree to include the following functions below.
- Implement Information gain function, which is the measure of decrease in entropy
    after dataset split and is calculated by the formula IG = E(parent) – [weighted average]
    * E(children)
- Start from the root node and at each decision node we select the best split based on
    best IG.
- We use Greedy Search to loop over all features and over all thresholds which are all
    possible feature values.
- Save the best split feature and split threshold at each node and build the tree
    recursively.
- Apply stopping criteria to stop the tree from growing, so we use maximum depth,
    minimum samples at node, no more class distribution in node.
- When we have a leaf node, store the most common class label of this node.

## Predict Algorithm:

- Traverse the tree recursively.
- At each node look at the best split feature of the test feature vector x and go left or
    right depending on feature index <= threshold
- When we reach the leaf node we return the stored most common class label.


**Random forest algorithm:** The idea behind a random forest is to average multiple (deep)
decision trees that individually suffer from high variance, to build a more robust model that
has a better generalization performance and is less susceptible to overfitting.

```
Train Algorithm:
```
- First, we create a data structure class RandomForest to assign initial default values in
    def __init__ to hold multiple instances on class DecisionTree.
- Create a global function, pick_data for bootstrapping to input all the samples and
    features and randomly choose with replace=true to allow repetition to make the
    subsets to train tree.
- Create another global function, most_common_label similarly as done for decision
    tree algorithm.
- Create function fit to train data where we create trees recursively and give them
    sample split, maximum depth and append them.
- Create function predict to predict data recursively.
- From all of the trees, we want the corresponding predictions combined. So, we use
    np.swapaxes function.
- Then we predict the most common label and return it as a numpy array.

**Results:**

**Breast Cancer dataset**

a) We set the number of trees to 2 and max_depth to 10, and with that we obtain 0.
accuracy as shown below.

b) Then we set the number of trees to 3 and max_depth to 10, and with that we obtain
0.937 accuracy as shown below.

c) Then we set the number of trees to 5 and max_depth to 10, and with that we obtain
0.965 accuracy as shown below.

d) Then we set the number of trees to 7 and max_depth to 10, and with that we obtain
0.9 58 accuracy as shown below.

d) Then we set the number of trees to 1 and max_depth to 10, and with that we obtain
0.9 02 accuracy as shown below.

**Car Evaluation dataset**

a) We set the number of trees to 3 and max_depth to 10, and with that we obtain 0.976
accuracy.

b) We set the number of trees to 5 and max_depth to 10, and with that we obtain 0.973
accuracy.

c) We set the number of trees to 7 and max_depth to 10, and with that we obtain 0.976
accuracy.

d) We set the number of trees to 10 and max_depth to 10, and with that we obtain 0.971 accuracy.

e) We set the number of trees to 1 and max_depth to 10, and with that we obtain 0

We can see the difference when depth=1 and depth>1. Larger trees help you to convey more info whereas smaller tree gives less precise info. So depth should
large enough to split each node to your desired number of observations. More trees also
mean more computational cost and after a certain number of trees, the improvement is
negligible. Broadly, we didn’t find depth to be a limiting factor. Also after reruns, we found
sample size = 10 to the most fitting in the model.

Advantages of random forest algorithm are:

1. **Reduces overfitting** : It creates as many trees on the subset of the data and combines
    the output of all the trees. In this way it **reduces overfitting** problem in decision
    trees and also **reduces the variance** and therefore **improves the accuracy**.
2. **High accuracy** : It runs efficiently on a large database and produces highly accurate
    predictions.
3. **Stability:** Random Forest algorithm is very **stable**. Even if a new data point is
    introduced in the dataset, the overall algorithm is not affected much since the new
    data may impact one tree, but it is very hard for it to impact all the trees.
4. **Estimates missing data** : It can maintain accuracy when a large portion of data is
    missing as in the case of many real-life examples.

Limitations of random forest algorithm are:

1. **Longer Training Period:** Random Forest require much more time to train as
    compared to decision trees as it generates a lot of trees (instead of one tree in case
    of decision tree) and makes decision on the majority of votes.

2. **Complexity:** Random Forest creates a lot of trees (unlike only one tree in case of
    decision tree) and combines their outputs. To do so, this algorithm requires much
    more computational power and resources.
