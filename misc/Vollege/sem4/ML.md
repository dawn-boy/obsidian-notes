## Types of learning
### Reinforced learning
- feedback is given to algorithm when it does something right or wrong
### Supervised learning
- pre-labelled data is given to the model to predict new outcomes
### Unsupervised learning
- non labelled data self organizes to predict new outcomes
***
# Perceptron
- perceptron is a neural network unit that uses an algorithm to learn the weights for the input in order to draw a boundary
## Artificial neural network
- its a mathematical function based on a model of biological neurons, where each neuron takes inputs, weighs them separately, sums them up and passes the sum through a step (activation node) to produce the output
## Single Layer Perceptron (SLP)
### Components

![[Pasted image 20250316105741.png]]
- Input features
	the perceptron takes multiple inputs features, each input refers a characteristic of the input data
- Weights
	Each input is assigned a weight that determines the influence of the input on final output. During training the weights are adjusted to find optimal values.
- Summation function
	The summation function combines all the weighted input and its passed onto the activation function
- Activation function
	the weighted sum is compared with a threshold value to produce a output (0 or 1)
- Output
	the final output is determined by the activation function
- Bias
	bias makes independent adjustments to the input, improving the flexibility in learning
- Learning algorithm
	the perceptron adjusts its weights and bias using a learning algorithm like **Perceptron Learning Rule** to minimize the prediction errors.
### Activation function

![[ml_16.png]]
- The activation function is a mathematical gate in between the input of current neuron and the output of next neuron. 
- The activation function decides whether to activate a neuron or not by calculating the weighted sum and further adding bias to it
- The purpose of activation function is to introduce non-linearity 
### Algorithm: Perceptron Learning Rule
- it states that the algorithm would automatically learn the optimal weight coefficients of the inputs 
#### How Perceptron learn
1. Initialize the weights at random
2. compute the output Y 
	$$(compute\ input)\ \implies a = \sum_ix_i*w_i $$$$ (pass\ to\ activation\ function) \implies Y_{observed} = f(a)  $$
	![[Pasted image 20250316122207.png]]
3. Calculate the error $$ \delta = Y_{target}\  - Y_{observed} $$
4. Use the newly calculated error to update weights 
 $$ w_{new} = w_{old}\ + \eta\ \delta \ x $$ 
	 where, 
	 $\eta \implies learning\ rate$,
	 $\delta \implies error,$
	 $x \implies inputs$

5.  Repeat step 2, 3, 4 until convergence, that is error is zero

### Linearly Separable Problem

![[Pasted image 20250316104615.png]]
- A linearly separable problem refers to a classification task where data points from different classes can be separated by a straight line given by linear equation 

#### Decision boundaries for AND, OR, XOR
##### For AND
![[Pasted image 20250316104838.png]]
- AND gate can clearly distinguish different classes ( Target classes => 0 and 1) using a single line.
- Lower region from the line contains all the 0 class data points while upper region has 1 class data points.
##### For OR
![[Pasted image 20250316105207.png]]
- OR gate can also clearly distinguish different classes with a single line.
##### For XOR
![[Pasted image 20250316105334.png]]
- Decision boundaries for XOR gets difficult to deal with as we need two straight lines to distinguish data points. 
- So either we need to have a transfer function that includes more than one decision boundary or we have to use a more complex neural network that is able to generate a more complex decision boundary.
## Multi Layer Perceptron

![[Pasted image 20250316105900.png]]
- Multi Layer perceptron teams up with additional perceptron that is stacked in several layers to solve complex problems
- Each perceptron on the left (The Input layer) send output to all the perceptrons in the middle layer (The Hidden layer) which then sends its outputs to the final layer (The Output layer)
- For each signal the perceptron uses different weights
- Types on number of layers
	- Shallow neural network - Three layer MLP
	- Deep neural network - four or more layers MLP
- In SLP, the activation function is a simple step function that outputs binary (either 1 or 0) but in MLP, other activation functions (generally sigmoid activation functions) can be used which results in an output of real values, usually between 0 and 1 or -1 and 1. ***This allows for probability based prediction or classification of items into different labels***
### Components

![[Pasted image 20250316112634.png]]

- Input layer
	introduces input into the network
- hidden layer
	Performs classification of features. Two hidden layers are sufficient to solve most problems
- output layer
	produces output
### Algorithm: Backpropagation
There are two phases in this algorithm
1. Forward phase
	the activations are propagated from input to the output
2. Backward phase
	in this phase, the error between the observed value and the target value is calculated. The weights and bias are adjusted based on the error 
#### Gradient descent
- A mathematical technique the modifies the parameters of a function to descent from a high value of a function to a low value 
- Applying gradient descent to the error function helps find weights that achieve lower error values making the model more accurate

### Steps for training a MLP using backpropagation gradient descent algorithm

1. Understand the problem and decide on the network structure.
	- number of input nodes,
	- number of hidden layer nodes
	- number of output nodes
2. Initialize the network parameters
	- Epochs
	- learning rate
	- network and bias weights
	- bias input
	- activation function
3. Start the learning process
	At each iteration
	1. Set input to the model and compute its output
	2. using back propagation, compute the error for output and hidden nodes
	3. update the weight between hidden layer and output layer
	4. update the weight between input layer and hidden layer
	5. display the weight
### Problem
![[Pasted image 20250316123001.png]]
#### forward pass
1. Calculate the output
	- Output of input nodes,
	 $$ a_j = \sum_j(w_{ij}*x_i)  $$
		$a_3 = (w_{13}*x_1) + (w_{23}*x_2)$
		$a_4 = (w_{14}*x_1) + (w_{24}*x_2)$
	
	-  Output of hidden nodes (using activation function)$$ y_j = F(a_j) = \frac{1}{1+e^{-a_j}} $$
		$y_3 = F(a_3) = \frac{1}{1+e^{-a_3}}$
		$y_4 = F(a_4) = \frac{1}{1+e^{-a_4}}$
	
	- compute the total network output,
		$a_5 = (w_{35}*y_3) + (w_{45}*y_4)$
		$y_5 = F(a_5) = \frac{1}{1+e^{-a_5}}$
	
2. Calculate the error
	- for output unit,$$\delta_{j}= y_j * (1-y_j) * (y_{target} - y_j) $$
		$\delta_{5}= y_5 * (1-y_5) * (y_{target} - y_5)$
	
	- for hidden unit,$$\delta_{j}= y_j * (1-y_j) * \sum_k(\delta_k*w_{jk}) $$
		$\delta_{3}=  y_3 * (1-y_3) *\delta_5\ w_{35}$	
		$\delta_{4}=  y_4 * (1-y_4) *\delta_5\ w_{45}$	
	
3. Update the weights$$w_{new} = w_{old} + \eta\ \delta_j\ x_j  $$
	where,
	$\eta \implies learning\ rate,$
	$\delta_j \implies error,$
	$x_j \implies input$
	
4. Repeat step 1,2,3 until convergence, that is until the error rate is negligible



***
# Geometric models

 - uses geometric notion of distance to represent similarity
- if the distance between two points are small, then they are expected to have similar features
- so nearby features are expected to be classified under the same cluster
## KNN classifier (K nearest neighbors)
- it belongs to supervised learning and is useful in intense application used for pattern recognition 
- it is a non-parametric and lazy-learning algorithm
- It stores all the available cases and classifies the new data based on a similarity measure ( using distance functions )
- use KNN classifier only when the data is 
	- noise free
	- dataset is small
	- data is labeled
- if k-value is too small
	- then that leads to overfitting because of the noise in the data
	- it leads to unstable boundaries
- if k-value is too large
	- then that leads to misclassification of data because it'll include data points that are far away from the neighbors
### problem

- using a distance function calculate the distance between the test data and other training data points
- take K number of neighbors based on the distance 
- take the median value of the neighbors class and classify the test data under that
	![[ml_14.png]]

- advantages
	- easy to implement
	- optimal in large sample limit
- disadvantages
	- large storage req
	- computationally intensive
	- highly susceptible to curse of dimensionality ( with increase in dimensions of the data, the time complexity increases)
- applications
	- image recognition
	- video recognition
	- pattern recognition

***
# K-means clustering

- it is an iterative algorithm that divides the unlabeled dataset into k different clusters
- partitioning the dataset into clusters without forming a hierarchical structure
- The value of K must be predetermined before-hand
- It is a centroid-based algorithm where each cluster is associated with a centroid
- The main aim of this algorithm is to minimize the distance between data points and its respective clusters
- The 'K' in k-means denotes the number of k clusters
### advantages
- easy to implement
- fast and efficient
- only one parameter to be customized (k value) and then results can be seen
### disadvantages
- should choose k value manually
- very sensitive to normalization and standardization
- doesn't work well if clusters are of different sizes and density
## problem
1. Select random points as Cluster 1 and Cluster 2
2. using the Euclidean distance formula calculate the distance between all the points
3. assign each point to their closest clusters
4. calculate the mean of x distance of data points and y distance of data points
5. now, use the mean value as the new location of cluster 1 and cluster 2
6. repeat step 3,4
7. if the mean value differs from the previously calculated mean value goto step 5 or else terminate. We have our model.

## Elbow method
- this method executes k-means algorithm for different k values (1-10). 
- For each value of K, a WCSS (within cluster sum of squares) score is calculated
- WCSS score is the distance between the data points in a cluster to its centroid
- the sharp point of bend in the plotted graph (between k-value and WCSS score) is said to be the best k value
	![[ml_13.png]]
	
***
# Hierarchical clustering
- hierarchical clustering starts by treating each observation as a separate cluster
- then it repeatedly identifies the two clusters that are closer to each other and merges the two most similar clusters
	![[ml_7.png]]
- this iterative process continues until all the clusters are merged together
#### ==***this algorithm uses distance matrix as the clustering criteria to compare data points***==

- this process can be also visualized in a **dendrogram form** ( its a tree structure form)
	![[ml_8.png]] 
- it shows how objects are grouped together (in an agglomerative way) or partitioned ( in a divisive way)
### types of approach
- Agglomerative approach
	- also called bottom-up approach
	- each sample is treated as a single cluster and then successively merged until there's a single cluster
	- can represent the data in a dendrogram form
- divisive approach
	- also called top-down approach
	- initially all node belongs to a single cluster, then eventually each node forms its own cluster
	- reverse of agglomerative approach
## METRICS used for judging clustering methods 
- it should provide high quality clusters
- Should have High Intra-class similarity: 
	- Data points should be cohesive with their cluster
- Should have low Inter-class similarity:
	- Data points should be distinct from other clusters
## METRICS used for calculating distance
- Euclidean distance
	- its the ordinary straight line between two distance points in Euclidean space

$$ Euclidean =>  \sqrt{{(x_{1}-x_{2})^2}} $$
- Manhattan distance 
	- its the difference between the absolute values of two points 
$$ Manhattan => | x_1 - x_2 | $$

### cluster linkage strategies
- single linkage 
	- considers the minimum distance between two clusters
		![[ml_9.png]]
- complete linkage
	- considers the largest distance between a node in one cluster and a node in another
		![[ml_10.png]]
- average linkage
	- takes the average distance between elements in one cluster and elements in another
		![[ml_11.png]]
- centroid linkage
	- takes the distance between the cluster centroids
### Problem sum
given a distance matrix of two clusters C1: {a,b} and C2: {c,d,e}. Find three cluster distances

![[ml_12.png]]
### single link
$$ dist(C1, C2) \implies min\{{d(a,c),\ d(a,d),\ d(a,e),\ d(b,c),\ d(b,d),\ d(b,e)\}} $$
$$ \implies min\{{3,4,5,2,3,4\}} $$
$$ \implies 2 $$

### complete link
$$ dist(C1, C2) \implies max\{{d(a,c),\ d(a,d),\ d(a,e),\ d(b,c),\ d(b,d),\ d(b,e)\}} $$
$$ \implies max\{{3,4,5,2,3,4\}} $$
$$ \implies 5 $$
### average link
$$ dist(C1, C2) \implies \frac{d(a,c)+\ d(a,d)+\ d(a,e)+\ d(b,c)+\ d(b,d)+ d(b,e)}{6} $$
$$ \frac{3+4+5+2+3+4}{6} \implies \frac{21}{6} \implies 3.5$$
***
# clustering
- clustering is a unsupervised machine learning that categorizes the given unlabeled dataset by similar patterns 
- application: 
	- land use: identification of similar land use
	- marketing: helps marketers discover similar customer bases and use targeted advertising
- types of clustering: 
	- Hard clustering:
		- each data point fully belongs to a particular cluster.
			![[ml_2.png]]
	- Soft clustering
		- each data point can belong to multiple clusters with a certain probability
			![[ml_3.png]]

- types of clustering algorithms
	- centroid based clustering
		- this method groups data points around a central point. Each data point is assigned to the nearest centroid
		- Limitation: the number of clusters (k) must be chosen in advance
			 ![[ml_4.png]]
		- Example: K-means
	- density based clustering
		- clusters are formed in areas where data points are closely packed together, with gaps indicating separation.
		- This method automatically finds the number of clusters
			![[ml_5.png]]
		- Example: DBScan
	- connectivity based clustering
		- builds a tree like structure that group similar data points
		- types:
			- divisive: starts with one large cluster and splits into smaller clusters
			- agglomerative: starts with individual data points and merges them into a larger cluster on the way up
			![[ml_6.png]]
	- fuzzy clustering
		- instead of assigning each data point to only one cluster. fuzzy clustering gives a membership score showing how much a point belongs to each cluster.
 