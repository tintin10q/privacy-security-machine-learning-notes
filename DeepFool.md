
The DeepFool attack is an [[Evasion Attack]].

Shortly said: DeepFool uses gradient to project η∗(x0) to classification boundary. Now if you want to know more:


The key idea behind the DeepFool attack is to iteratively compute the shortest distance from an input sample to the decision boundary of a neural network.

DeepFool builds adversarial examples by searching for the closest perturbation to the decision boundary. 

![[Pasted image 20230612172102.png]]


As multi-class classifier can be viewed as aggregation of binary classifiers, we first give the algorithm for binary classifiers: $f(x) = w^T x + b$.
- The minimal perturbation to change the classification is the minimal distance to the decision boundary: $\{w^T x + b = 0\}$.
- The minimal perturbation corresponds to the orthogonal projection of $x_0$ onto $f(x) = 0$.

Here's a step-by-step explanation of the DeepFool attack:

1. **Initialization**: Start with an input sample, x, for which you want to craft an adversarial example. Let f(x) be the output vector of class probabilities predicted by the target neural network.
2. **Iterative Perturbation**: Repeat the following steps until the adversarial condition is satisfied:
    - Compute the gradient of the loss function with respect to the input x. This gradient provides information about the direction of steepest ascent towards the decision boundary.
    - For each class $i \neq$ *the original predicted class*, compute the distance $d_i$ from $x$ to the decision boundary of class $i$ like so: 
    1. Compute the absolute difference between the score (or probability) of class $i$ and the score of the true class.
    2. Divide this absolute difference by the $L_2$ norm of the gradient.
    3. The class with the smallest distance $d_i$ is the closest incorrect class.
    
    In other words, for each class that is not the original predicted class, DeepFool measures how far the input sample $x$ is from the decision boundary of that class. This distance is computed by taking into account the difference in scores between class $i$ and the true class, and normalizing it by the magnitude of the gradient. The class with the smallest distance is considered the closest incorrect class, as it indicates the direction in which the input needs to be perturbed to cross the decision boundary.
    - Determine the minimum perturbation needed to cross the decision boundary towards the closest incorrect class. This perturbation is computed as the product of the gradient and a scaling factor that depends on the distance d_i. The scaling factor ensures that the perturbation is minimal.
    - Update the input sample x by adding the computed perturbation.
    - Recalculate the output vector f(x) for the updated input.
3. **Adversarial Example**: Once the adversarial condition is satisfied (e.g., the predicted class changes), the algorithm terminates, and the resulting perturbed input x' is considered the adversarial example.

The DeepFool attack aims to minimize the L2 norm of the perturbation required to cause misclassification. It takes into account the decision boundaries and the sensitivity of the neural network to perturbations. 

### From the slides

By finding the closest incorrect class, DeepFool identifies the direction in which the input sample should be perturbed to achieve misclassification with the smallest possible perturbation.

The minimal perturbation corresponds to the orthogonal projection of $x_0$ onto f (x) = 0.

In math: $\eta\cdot(x_{o)}= \text{argmin}\|\eta\|_2$ subject to: $\text{sign}(f(x_{0+\eta))}\neq sign(f(x_0))$

We want to find an adversarial perturbation for the point ($x_{0,}y_{0}$. 
In Euclidean geometry, the distance from a point to a line $f(x) = 0 can be given by: $$\eta\cdot(x_0)=-\frac{f(x_{0})}{\|w\|^2_2}w$$
![[Pasted image 20230612190712.png]]