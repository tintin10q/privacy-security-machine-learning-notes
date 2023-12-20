
The problem with the [[Evasion Attack#Known Evasion defenses|most defenses against evasion attacks]] is that they are empirical in nature. This means that they work sometimes and sometimes don't and differently. With work, we mean improve robustness of the model. You kind of have to repeat the experiment for each setup and it doesn't really generalize in theory. It kinda does of course. 

Certified robustness gives us defenses against evasion attacks which are formally proven with theoretical guarantees. How does this work?  

![[Pasted image 20230612231817.png]]

A defense gets certified robustness if you can do a robustness validation with a guarantee. Without the guarantee it's an empirical defense. 

So how do you give the guarantee? It consists of:
- Robust verification 
- Robust training 

![[Pasted image 20230613022511.png]]

You have an input, you have a shape which abstracts all possible reasonable perturbation, you then transform that shape in your network in the layers, convolution, make it dense etc, then you have a shape that abstracts all possible outputs and if all possible outputs still all output the right class it always works.

## Robustness verification

The idea behind robustness verification is to provide a lower bound on the robustness of the model with respect to the constraints of the perturbation (a [[perturbation distance metrics|pertubation distance metric]] like $l_2$ norm). 

### TLDR
He said that knowing the concept is enough. So here is the tldr:

Certified robustness gives mathematical guarantees about robustness of model e.g. resistance against evasion attacks.

With complete verification you guarantee that you will always be able to detect adversarial examples. However, this is too expensive for larger models. So then you get incomplete verification which just provide bounds on which adversarial examples will be detected. 

Probabilistic and deterministic verification refer to different approaches in assessing the robustness of a model against adversarial examples. If an input x is non-robust against adversarial examples, **deterministic** will always label it as non-robust (**yes or no**).  **Probabilistic** Verification gives a **confidence probability** of how likely the input is an adversarial example.

Robust training is a complement to robustness verification. He didn't really give examples 

### Complete Verification 
If a verification method is complete, it guarantees that for any non-verified input x, it will be able to detect an adversarial example $x'$ if one exists. In other words, it ensures that the verification process covers all possible inputs and can accurately identify any inputs that can be perturbed to produce adversarial examples. Complete verification provides a stronger guarantee but may be more computationally expensive (exponentially in the worst case) or even infeasible for complex models or large datasets. But it works reasonably well on NN with a couple of thousands of neurons.

Ways to do this includes a *Solver based approach* or a *branch and bound approach*.

### Incomplete Verification 
Complete verification is not feasible for large NNs.
Incomplete verification, on the other hand of complete verification, provides a partial or limited analysis of the model's robustness. It may not cover all possible inputs or may have certain limitations in terms of the types of adversarial examples it can detect. While incomplete verification methods may not provide guarantees for all inputs, they can still be useful in identifying vulnerabilities and improving the model's robustness within the scope of their analysis.

For deterministic incomplete verification there is 
- *Semidefinite programming*: formulates the robustness verification problem as an optimization problem with linear matrix inequalities. SDP solvers find tight upper bounds on the maximum allowable adversarial perturbations that a network can tolerate while maintaining robustness guarantees. 
- Linear relaxation (approach the real model with a linear model to be able to reason about it) you can do this on one neuron or multiple neurons
- *Lipschitz bounds*: Lipschitz bounds refer to a property of continuous functions where the rate of change of the function is limited by a constant factor. The Lipschitz constant represents the smallest such factor that bounds the function's increase. Lipschitz bounds are used to ensure that the output of a neural network changes smoothly within a certain range, providing guarantees on the robustness of the network against adversarial perturbations.

![[Pasted image 20230613122808.png]]

With Linear relaxation example ^

### Probabilistic vs. deterministic verification

In the context of robustness verification, probabilistic and deterministic verification refer to different approaches in assessing the robustness of a model against adversarial examples. If an input x is non-robust against adversarial examples, deterministic will definitely label it as non-robust.

#### Deterministic verification

Deterministic verification methods aim to provide a binary determination of robustness for each input. If an input x is deemed non-robust under deterministic verification, it means that the method is confident that there exists at least one adversarial example that can fool the model for that specific input. The x will be labeled as non robust. Deterministic verification does not provide a probability or confidence score but rather gives a definitive answer of either robust or non-robust. 

#### Probabilistic verification

Probabilistic verification methods, on the other hand, provide a measure of confidence or probability associated with the model's robustness for each input. Instead of giving a binary determination, probabilistic verification assigns a likelihood or confidence score to indicate the likelihood that an input is robust against adversarial examples. This probability can be interpreted as the estimated probability that the model's prediction remains correct in the presence of potential adversarial perturbations. Probabilistic verification approaches often involve statistical or sampling-based techniques to estimate the robustness.

### Robustness Verification Optimization Problem 

The optimization problem:
$$M(l, l′) = \min\limits_{x+\eta} Z_\theta(x + \eta)_l − Z_\theta(x + \eta)_{l′}$$
s.t. $f(x) = l := arg\max\limits_{l_i}z_\theta(x)_{l_i}$ and $\|\eta \|\leq \epsilon$
where $Z_\theta(x)_l$ is the softmax output for input x on class l and $\eta$ is the perturbation.

> **Certified Robustness**
> If $M(l,l') > 0$ for all $l' \neq l$, then the model is *certifiably robust*  at input x within radius $\epsilon$ with respect to the $l_p$ norm

So robustness is shown when $M(l,l') > 0$. 
Not very salable because it is NP complete too bad. But you can compute a lower bound on M by relaxing the conditions. Compute lower bound on M. You do a loose bound. However, this is a trade of. The more salable the model the less tight. 

There are a lot of robustness verification methods. 

## Robust training

Robust training is a complement to robustness verification. He didn't really give examples 
- It is used to enhance to certifiably of the model.
- Objective function aims to minimize
		- the loss function (for accuracy) 
		- linear relaxations and/or bounds (for robustness).