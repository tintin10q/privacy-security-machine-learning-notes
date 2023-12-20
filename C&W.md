With the C&W [[Evasion Attack]] attach we change the general evasion attack algorithm. Usually finding an adversarial example is defined as $$\min\limits_{x+\eta}\|x,x+\eta\|$$ where you want $f(x+\eta) = l'$ where $f(x) = l$, so $l' \neq l$, and $\eta \in [0,1]^n$ so you want the model to give a different label with the smallest $\eta$ or the smallest difference between $x$ and $x'$. 

The C&W method replaces the first part with: $$\min\limits_\eta\|\eta\|_p+c\cdot g(x+\eta)$$
Where $g$ satisfies: $f(x+\eta)=l'\Leftrightarrow g(x+\eta) \leq 0$ 

So I think they added minimizing a [[perturbation distance metrics|distance norm]] instead of simple distance, and they added the g objective function. The g function serves as a measure or indicator of how well the adversarial condition is satisfied. It is designed in such a way that g(x + η) ≤ 0 implies that the adversarial condition is met (i.e., f(x + η) = l').


![[Pasted image 20230612160714.png]]

## Example G 
An example G is: $$g(x') = \max(\max\limits_{i\neq l'}\{Z(x')_i\}-Z(x')_{l'}, -\kappa)$$
- $Z(\cdot)_i$ is the soft max function output for class i 
- $\max\limits_{i \neq l'}\{Z(x')_i\}$ calculates the maximum confidence or probability among all classes other than the target class $l'$. It represents the maximum probability assigned by the model to any non-target class for the adversarial example $x'$.
- $Z(x')_{l'}$ represents the confidence or probability assigned by the model to the target class $l'$ for the adversarial example $x'$.
- $\max\limits_{i\neq l'}\{Z(x')_i\} - Z(x')_{l'}$: calculates the difference between the maximum confidence among non-target classes and the confidence assigned to the target class. It measures the margin between the highest non-target class confidence and the target class confidence for the adversarial example.
- $-\kappa$ is the confidence constant, usually set to zero. The confidence constant κ is a parameter that helps control the strictness of the adversarial condition. It is usually set to 0. This constant ensures that the margin between the highest non-target class confidence and the target class confidence is negative (i.e., adversarial condition is satisfied) and greater than or equal to $-\kappa$.

By taking the maximum of the margin $\max\limits_{i\neq l'}\{Z(x')_i\} - Z(x')_{l'}$ and $-\kappa$ , the function $g(x')$ ensures that if the margin is positive or greater than -κ, it implies that the adversarial condition is not met ($f(x') \neq l'$). In that case, $g(x')$ will be positive. However, if the margin is negative (i.e., $f(x') = l')$, $g(x')$ will be zero or negative, indicating that the adversarial condition is satisfied.

So really the function $g(x')$ captures the difference between the highest non-target class confidence and the target class confidence for the adversarial example $x'$. If this difference is positive it means that the target class confidence was not higher than the highest non target class confidence and not the predicted class. If this difference (between the target class and highest confidence of non target class) is negative it means that the target class is more confident than any other class and then that's what we want. 

So with $f(x+\eta)=l'\Leftrightarrow g(x+\eta) \leq 0$ we mean that g has to behave in such a way that if the output of $g$ is negative that we have fooled the model with our $\eta$. 


### Why do we involve the objective function:

- The g function provides a fine-grained control over the satisfaction of the adversarial condition
- The g function instance can be chosen to exactly what you need
- The g function helps in generating adversarial examples that are more **robust** against various defenses.
- The inclusion of the g function ensures that the generated adversarial examples satisfy the desired adversarial conditions. For instance this g makes the inputs be more reliable false positived as the target class. 
- **Less focus on decision boundary**. Unlike PGD, the g function offers a principled approach for generating adversarial examples by considering confidence, margin, and model behavior instead of relying on proximity to the decision boundary.
- To **avoid box constraints** you can also have another g called $\omega$. Box constrains (e.g., restricting the perturbed input within a specific range) can limit the search space for adversarial examples. The g function provides an alternative approach by effectively defining a constraint through its properties.
- Good perturbations, subjectively you don't see the changes. 

This is a black box attack because you don't need access to the model internals.