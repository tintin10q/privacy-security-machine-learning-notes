The PGD [[Evasion Attack]] improves over the [[FGSM]] attack by taking a multiple-step approach. 

FGSM creates the [[Adversarial example]] by looking at the gradients with respect to the input once to change the input in such a way that we maximally increase the loss. With PGD we keep repeating this process with the obtained adversarial examples to get a more accurate result closer to the decision boundary, so less perturbation.

![[Pasted image 20230612140048.png]]

You do have like iterative FGSM like IFGSM but PGD adds that you **don't have to start from the original point.**  The PGD attacks start at a random point to reduce the risk of running into a local minimum. When this happens it could even be that small perturbations make the image less likely to be misclassified because the perturbation happens to move the input into a direction which is easier for the model to recognize. If the attack starts from a random place instead, this is much less likely to happen. In other words, PGD with random start points can find very diverse adversarial examples because you find other maxima.

There is also another step which makes sure your $x'_t$ remains a valid input. Valid/allowed inputs are in the set called $S$. Basically this is the $x'\in [0,1]$ constraint. But S is basically a generalization of this. So if the point $x_t + \epsilon \cdot \text{sign}(\nabla_x\mathcal{J}_\theta(x,l))$ after the gradient update leaves the set S, PGD projects it back into S. Either by like clipping or doing min max or some other way. Maybe you do an update that actually decreases the loss again. But this way you stay on the boundary of S which gives good results. Hopefully still with small perturbation.  

So in math we can say that  $\eta = \epsilon · sign(\nabla_x \mathcal{J}_\theta(x, l))$ can be
updated by:
$$x_t = x + \epsilon \cdot \text{sign}(\nabla_x\mathcal{J}_\theta(x,l))
$$$$x_{t+1} = Clip_{x+S}(x_t + \alpha\cdot\text{sign}({sign}(\nabla_x\mathcal{J}_\theta(x,l)))$$So we add the formula to get $x_{t+1}$ and which involves the $Clip(\cdot)$ which limits the changes of the generated adversarial example. 

This is a bit confusing because there is kinda two types of limiting:
 
1. When you update the adversarial images inside the loop with grad you do not want the adversarial images to be too different, so PGD projects it by back so that the perturbation with: $\eta = (x't - x)$ should be in the range of $[−𝜖,𝜖]$. So $\epsilon$ is more like the perturbation budget. 
2. After you add this perturbation, you want to make sure it is a real image. So you should project it back such that the image is in range [0,1]



PGD was proposed as a [[data augmentation]] method to get inputs [[adversarial training]]. It is currently the best one they have.

