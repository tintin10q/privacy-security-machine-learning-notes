
In supervised learning the objective you have a set of pairs (x, y) called training examples. 
x is a feature vector and y is the label for this feature vector (the classification value of x). 
$x^i$ is the i-th example and $y^i$ is the corresponding output value. 
Sometimes the **x** are called the features or also independent variables or samples.
Sometimes y is called the dependent variables.  

The goal of supervised learning is to find a function f such that $y = f(x)$ for any possible x.

We train this function on the training set where we try to make the best function to predict the test set and then we evaluate the function on a test set to see the generalization ability of f.  

- If y is a real number we call this a regression problem
- If y is a boolean variable we call this a binary classification
- If y is a member of a finite set we call this a multi class classification (most important in course) 

So how do you train f using the training data?
You use the labeled data and a loss function $\mathcal{L}$. The $\mathcal{L}$ function tells you how well your f is doing. This basically means some figure saying how many inputs x probably gave the right y as output. Then once you have this loss function you want to minimize it. Through back propagation you can minimize the loss function by chaining the model parameters $\theta$ in the right way. This is done by after calculating the loss function basically taking the derivative of the loss function (which is basically the derivative of the entire model as a math function) and then you use the derivative to move the $\theta$ in the right direction to make the loss function smaller. 

A common loss function is: $$\min\limits_{\theta} \frac{1}{n}\sum\limits_{i=1}^n\mathcal{L}(f_\theta(\mathbf{x}_i), \mathbf{y}_i)$$ 

So with $f_\theta$ we mean f instantiated with the hyper parameters $\theta$. 

Also see [[Gradient calculation]] for an example of this derivative stuff. 

### No free lunch
There is no free lunch which means that there exists no single model that works best for every problem. You don't know if you can ever find the best model or best defense. To find the best model have to test a lot of models, and then you still don't know. But after doing a lot of testing you can make trade-offs between the speed, accuracy, and complexity of the obtained models. It could be that you have a defense that works but is very expensive so then no one uses it.

## Generative vs Discriminative

You can then have 2 types of supervised learning models: 

### Generative models 
With generative models you assume that the probability the example x belongs to a class is proportional to the joint probability of example x and class. So P(x | c). You try to make a model that understands the underlying distribution of the data. This is like GAN models etc.

### Discriminative models

Directly model whether an example x belongs to the class. Discriminative models try to directly model the decision boundary between different classes without explicitly modeling the joint probability distribution of the input data and the class labels. Discriminative models aim to learn a function that directly maps the input data to the class label.

Discriminative models can be further categorized into probabilistic and non-probabilistic models.

- **Probabilistic discriminative models**: These models provide a probability distribution over the class labels given the input data. In other words, they estimate the conditional probability P(c|x), where c represents the class label and x represents the input data. Examples of probabilistic discriminative models include logistic regression and softmax regression. So here the softmax gives a vector where each position of the vector indicates the probability that the input was a certain class.
- **Non-probabilistic discriminative models**: These models do not provide a direct probability distribution over class labels. Instead, they learn a decision boundary that separates different classes. Support Vector Machines (SVMs) and decision trees are examples of non-probabilistic discriminative models. With these you only get one class as output and no explicit probability for each class.  

Probabilistic discriminative models provide explicit probability estimates for class labels, making them well-suited for classification tasks. Non-probabilistic discriminative models focus on directly learning a discriminative function or decision boundary, making them applicable to both classification and regression tasks.

