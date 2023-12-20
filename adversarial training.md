In adversarial training you generate [[Adversarial example|adversarial examples]] on purpose and include them into the training data with the correct label. This learns the model on how to deal with adversarial examples and adjust the decision boundary.

To build a robust network against adversarial examples. To do these you can make your own adversarial examples and (re)train your model with adversarial examples. 

**Adversarial training will make your model more robust.** For this we use the min max loss function. Because, we want to maximize the loss function when we see the perturbation, and you minimize theta, so the adversarial training is as efficient as possible. 

The min-max formulation of the loss function captures the adversarial training process. It involves finding the optimal model parameters (θ) that minimize the overall loss, while simultaneously finding the optimal perturbations (η) that maximize the loss for each example.

The use of the min-max loss function allows the adversarial training process to find an equilibrium between improving the model's accuracy on clean data and enhancing its robustness against adversarial examples. 

![[Pasted image 20230612141254.png]]

Here, $\rho(\theta)$ represents the expectation (average) over the training data $(x, l)$ drawn from distribution D. $\mathcal{J}_\theta(f (x_i + η), l_i)$ is the loss function that measures the discrepancy between the predicted output $f(xi + η)$ and the true label ($l_i$) for a given input ($x_i$) perturbed by the adversarial example ($\eta$). S represents the set of perturbations that satisfy certain constraints (e.g., L2 norm $\leq$ r).

On another slide in lecture 4 he had this function: $$\min\limits_\theta\max\limits_{\eta\in S}\mathcal{L}_{CE}(\theta, x_{i}+\eta, y_i)$$ here $\theta$ are the weights of the model and $\eta$ is the adversarial perturbation. 
- The inner maximization problem looks for adversarial examples by modifying input $x_i$.
- The outer minimization problem is to find a better θ to decrease the loss.

You could also have an **adversarial input** class. 

The idea is to actually use adversarial examples and not just like [[data augmentation]]. But I imagine data augmentation still works. 

## How to get adversarial examples 

The funny thing is that you can use the attacks like [[FGSM]] and [[PGD]] to get your adversarial examples. Interestingly adding FGSM adversarial examples does not protect against stronger iterative PGD attacks. PGD training is thought of as the most successful defense, as a network trained with PGD examples is robust against a wide range of attacks. 

![[Pasted image 20230612200544.png]]

Why does PGD work well? The attacker can use any attack so you want best adversarial training.  Probably because PGD is good at finding local maxima are likely to be the true maxima. Maybe because it moves around the decision boundary. As you can see here robust models with PGD have a much smaller loss and much less varied loss with less outliers than normal networks. 

![[Pasted image 20230612200837.png]]

So you probably train with the best adversarial examples you can get. In other words, PGD with random start points can find very diverse adversarial examples.  

Ideally, we hope there is only one global minimum for adversarial perturbation, but this is not realistic. We usually have multiple local minima for optimization problems in machine learning.
- Finding global minimum is too difficult, but many local minima are enough to cheat the model in evasion attacks.
- With "random start", PGD can find more local minima. 

![[Pasted image 20230612201245.png]]


Overdoing the perturbation (large perturbation) doesn't really work because the perturbation moves the original image a lot to the other class. Then you kind of the loose the point because the point is that the small perturbations look like noisy versions of the original image but large perturbation is too different  anyway so you don't really have to protect. 

## How robust is adversarial training 

Adversarial training will decrease the performance on clean data because the model becomes more complex. The best robust accuracy on CIFAR-10 is 64.25%, while it is easy to have clean accuracy higher than 90%. 

It is often easier than you would think to defend, but it comes at a cost. So it has to be worth it. 

### What did adversarial training do during training? 

They say Adversarial training learns rather than remembers. The idea is that the adversarial examples move the weights more on to the main task instead of also the small adversarial changes. You could say that the decision boundary becomes more pure, as Adversarial training encourages the model to focus more on the underlying task and the essential features of the data, rather than being overly influenced by small adversarial perturbations.

## Takeaway of Adversarial Training 

Adversarial training removes unnecessary features for robustness and focuses only on the important part.
- But the ignored part might be good for generalization (better clean accuracy).
- The large perturbation generated by a robust model tends to produce salient characteristics of the misclassified class.
- Due to these phenomena, robust models provide an additional benefit, which makes the saliency map easier to understand for human eyes.

![[Pasted image 20230612212428.png]]

