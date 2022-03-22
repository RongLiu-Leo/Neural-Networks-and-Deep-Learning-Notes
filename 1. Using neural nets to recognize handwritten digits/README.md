# Using neural nets to recognize handwritten digits

## Perceptrons
![](http://neuralnetworksanddeeplearning.com/images/tikz0.png)

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

![](http://neuralnetworksanddeeplearning.com/images/tikz2.png)

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
