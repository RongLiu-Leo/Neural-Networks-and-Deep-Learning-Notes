# Using neural nets to recognize handwritten digits

## Perceptrons
<div align=center>
<img src="http://neuralnetworksanddeeplearning.com/images/tikz0.png"/>
</div>


Suppose $x$ is the input value; $w$ is the learning weight; $b$ is the bias, which is equal to $-threshold$.The core equation of Perceptron algorithm is:

$$
output=\begin{cases}
 0 & \text{ if } w\cdot x+b\le 0 \\\\
 1 & \text{ if } w\cdot x+b>0
\end{cases}
$$

If you are familar with logistic regression, it turns out that the output is activated by the step function rather than sigmoid function. Sigmoid function is defined by:

$$
\sigma(z)=\frac{1}{1+e^{-z}}
$$

* Sigmoid function is  the smooth version of step function.

* The decision boundary of whether Perceptron or Logistic Regression is $w\cdot x+b=0$.

<div align=center>
<img src="http://neuralnetworksanddeeplearning.com/images/tikz2.png"/>
</div>


If we set the weight to $-2$ and bias to $3$, the single neuron is a NAND gate.

* The NAND gate is universal for computation, so logically we can build any computation up out of NAND gates.

### Exercises
1. Suppose we take all the weights and biases in a network of perceptrons, and multiply them by a positive constant, $c>0$. Show that the behaviour of the network doesn't change.
   
The decision boundary of perceptrons is $w\cdot x+b=0$. If all the weights and biases are multiplied by a positive constant, $c>0$, we get $cw\cdot x+cb=0$, which is equal to the original equation. That means the decision boundary is stationary.

2. Suppose we have the same setup as the last problem - a network of perceptrons. Suppose also that the overall input to the network of perceptrons has been chosen. We won't need the actual input value, we just need the input to have been fixed. Suppose the weights and biases are such that $w⋅x+b≠0$ for the input $x$ to any particular perceptron in the network. Now replace all the perceptrons in the network by sigmoid neurons, and multiply the weights and biases by a positive constant $c>0$. Show that in the limit as $c→∞$ the behaviour of this network of sigmoid neurons is exactly the same as the network of perceptrons. How can this fail when $w⋅x+b=0$ for one of the perceptrons?

The original term is $w⋅x+b$. If multiplied by a positive constant $c>0$, the term is $c(w⋅x+b)$. Substitute the term into sigmoid function:
$$
\sigma(x) =\frac{1}{1+e^{-c(w⋅x+b)}}, c→∞
$$
* if $w⋅x+b<0$, $c(w⋅x+b)→-∞$, so $\sigma(x)→0$.
* if $w⋅x+b>0$, $c(w⋅x+b)→∞$, so $\sigma(x)→1$.
* if $w⋅x+b=0$, $c(w⋅x+b)=0$, so $\sigma(x)=\frac{1}{2}$.
  
In summary, if $w⋅x+b=0$, the result is a real number, $\frac{1}{2}$, instead of the discreted number 0 or 1, so it cannot meet the output requirement of perceptron algorithm. By contrast, if $w⋅x+b≠0$, when multiplied by positive infinite $c$, the term will rapidly ascend or descend depended on its sign, which means the result of sigmoid function will only be the maxmum 1 or minimum 0, meeting the discreted output value requirement of perceptron algorithm.

## A simple network to classify handwritten digits
You might wonder why we use 10 output neurons. After all, the goal of the network is to tell us which digit (0,1,2,…,9) corresponds to the input image. A seemingly natural way of doing that is to use just 4 output neurons, treating each neuron as taking on a binary value, depending on whether the neuron's output is closer to 0 or to 1. Four neurons are enough to encode the answer, since $2^4=16$ is more than the 10 possible values for the input digit. Why should our network use 10 neurons instead? Isn't that inefficient? 

The ultimate justification is empirical: we can try out both network designs, and it turns out that, for this particular problem, the network with 10 output neurons learns to recognize digits better than the network with 4 output neurons. But that leaves us wondering why using 10 output neurons works better. Is there some heuristic that would tell us in advance that we should use the 10-output encoding instead of the 4-output encoding?

It's natural to match different local digit pattern features with real numbers rather than bluntly build up relationship between digital bits and features.

### Exercises
1. There is a way of determining the bitwise representation of a digit by adding an extra layer to the three-layer network above. The extra layer converts the output from the previous layer into a binary representation, as illustrated in the figure below. Find a set of weights and biases for the new output layer. Assume that the first 3 layers of neurons are such that the correct output in the third layer (i.e., the old output layer) has activation at least 0.99, and incorrect outputs have activation less than 0.01.
<div align=center>
<img src="http://neuralnetworksanddeeplearning.com/images/tikz13.png"/>
</div>

Due to the third layer output $x$ is a vector shape of (10,1), we should construct a matrix $W\in R^{4\times 10}$ in response to meet the output $z$ shaped (4,1). In addition, the shape of $b$ is (4,1) consistent with the output value. Firstly we ommit the $b$ to simplify the problem:
$$
z = Wx=\begin{bmatrix}
 w_{00}x_0+w_{01}x_1+...+w_{09}x_9\\
 w_{10}x_0+w_{11}x_1+...+w_{19}x_9\\
 w_{20}x_0+w_{21}x_1+...+w_{29}x_9\\
w_{30}x_0+w_{31}x_1+...+w_{39}x_9
\end{bmatrix}
$$
On account of only one nueron fired in the third layer, mere one scalar $x$ is activated and others are close to 0. Thus, actually each time only one column in matrix $w$ is meaningful. For example, if the value of the third layer is a 1, the output is:
$$
z = Wx=\begin{bmatrix}
 0+w_{01}+0+...+0\\
 0+w_{11}+0+...+0\\
 0+w_{21}+0+...+0\\
 0+w_{31}+0+...+0
\end{bmatrix}
=\begin{bmatrix}
 w_{01}\\
 w_{11}\\
 w_{21}\\
 w_{31}
\end{bmatrix}
$$
In summary, the column of matrix $W$ is the relative binary numbers. 
Therefore, we set all elements of $b$ to 0 and weight matrix $W$ to:
$$
W=\begin{bmatrix}
 0,1,0,1,0,1,0,1,0,1\\
 0,0,1,1,0,0,1,1,0,0\\
 0,0,0,0,1,1,1,1,0,0 \\
 0,0,0,0,0,0,0,0,1,1
\end{bmatrix}
$$