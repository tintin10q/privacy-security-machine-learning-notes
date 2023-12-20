This is actually an optimizing technique. However, they used it to create [[Adversarial example]]. So this is a type of [[Evasion Attack|evasion attack]]. The first adversarial examples were generated using this. 

The L-BFGS attack aims to find perturbations that can deceive a neural network model by optimizing an objective function that combines the magnitude of the perturbation and the loss incurred on the target class.

L-BFGS aims to solve the following optimization problem:

*Find minimum perturbation that causes misclassification.* This can be formalized in:
$$\min\limits_{x'}  c||\eta||+\mathcal{J}_\theta(x',l')$$ with $x' \in [0,1]$, c is a constant meant to be a regularization parameter that balances the importance of the perturbation magnitude $(c∥η∥)$ and the loss function that measures the discrepancy between the predicted output of the model for the adversarial example x' and the target class l'. The objective is to find a perturbation η that minimizes the combined value of the regularization term and the loss function.


You start with a benign example and initialize $\eta$ to a 0 vector. Then you use the L-BFGS algorithm to iteratively update the perturbation η to minimize the objective function. L-BFGS algorithm to iteratively update the perturbation η to minimize the objective function. 
During each iteration of L-BFGS, a line search is performed to determine a suitable value for the regularization parameter c.

The loss function is actually the loss function of the model. So basically you see if you can get an $x'$ to get to another label $l'$. 

Here is the example: 

![[Pasted image 20230612125049.png]]

Predicted as ostrich.

This is a white box attacks because you need the parameters of the model to calculate the loss function. 