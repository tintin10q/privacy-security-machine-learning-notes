Pruning is a way to make models simpler by removing the weights the least important for the main task. You remove redundant parameters from an existing network de increase its efficiency while maintaining accuracy. 

Actually pruning is setting the weights to zero to remove their effect. 

According to [[adversarial training]], we know adversarial attacks are successful because of some latent “mixture”. With pruning you try to prune the “mixture”. Pruning can be quite successful as many networks can be significantly pruned. Huge parts like 80%-90% can be pruned for more or less the same network. This is cool because it reduces the clean accuracy way less than adversarial training. 

![[Pasted image 20230612221226.png]]


## How to prune?
Pruning is also something you do with normal training but adversarial pruning is when you want to prune the parts of the network which is picks up on adversarial perturbation.

How to prune to make a robust network? One way is make the model to a prediction with clean example and adversarial example and then prune the neurons which are very different/distorted from the clean one.  

The distortion of latent features can be quantified by:
$$v(z,\widetilde{z})=E_{x,y}\sim D\|z-\widetilde{z}\|$$ here $z$ and $\widetilde{z}$ are the output of hidden layers with clean and [[Adversarial example]]s respectively. Empirically, the most distorted features usually appear in similar positions, so they can be removed.

## Pruning as a defense for evasion attack

The idea is to make your model smaller it is more focused on the main task and less focused on the Adversarial example. But it is also a defense mechanism against [[Evasion Attack]]. Pruning method actually does something similar to adversarial training. 

With adversarial training you try to remove the mixture in the latent space by making the network concentrate on the most important features by adding adversarial examples. With pruning, you also remove the mixture by removing the neurons which consider the adversarial part of input. 

Here proposed method is pruning:

![[Pasted image 20230612222759.png]]

