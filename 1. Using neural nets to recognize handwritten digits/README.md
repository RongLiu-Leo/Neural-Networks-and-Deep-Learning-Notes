# Using neural nets to recognize handwritten digits

## Perceptrons
![picture](http://neuralnetworksanddeeplearning.com/images/tikz0.png)

Suppose $x$ is the input value; $w$ is the learning weight; $b$ is the bias, which is equal to $-threshold$.The core equation of Perceptron algorithm is:

![](https://latex.codecogs.com/svg.image?output=\left\{\begin{matrix}&space;0&&space;\text{if}\&space;w\cdot&space;x&plus;b\leq&space;0\\&space;1&&space;\text{if}\&space;w\cdot&space;x&plus;b>&space;0&space;\\\end{matrix}\right.)

If you are familar with logistic regression, it turns out that the output is activated by the step function rather than sigmoid function. Therefore, naturally we can find that sigmoid function is acutally the smooth version of step function.

The decision boundary of whether Perceptron or Logistic Regression is ![](https://latex.codecogs.com/svg.latex?w\cdot&space;x&plus;b=0).