After the [[L-BFGS]] attack we got the FGSM (fast gradient sign method) [[Evasion Attack]]. FGSM improves over L-BFGS by using a faster gradient based approach instead of slow line search. 

![[Pasted image 20230612130505.png]]

The FGSM attack leverages the gradient information of the loss function to calculate a perturbation that is added to the original input to generate an adversarial example. By taking a small step in the direction that maximizes the loss, the attack exploits the model's sensitivity to slight changes in the input to create examples that are misclassified.

Let $\theta$ be the parameters of a model, $x$ the input, $l$ the true labels and $\mathcal{J}_θ(x, l)$ be the loss function to train the model.  Turns out we can find an adversarial example by doing: $$\eta = \epsilon \cdot \text{sign}(\nabla_x\mathcal{J}_\theta(x,l)), ~~x' = x + \eta$$The idea is to find an $\eta$ by taking the derivative of the loss $\mathcal{J}$ with respect to x (the input) into the direction which increases the lost the most. We only do gradients with respect to the input not the parameters of course. We are not trying to improve the model.

The gradients with respect to the input tell us how to change the inputs to get a lower result in the loss function and thus better $l$ predictions from $x$. But we actually want to misclassify which will increase the loss function. So we then just use these gradients to actually change our inputs in the other direction. Hopefully this will move the input over a decision boundary. 

Importantly, this is not an iterative attack, you only change the input once based on the gradients of the prediction with respect to the input to generate the [[Adversarial example]] and that is it. With the [[PGD]] attack you do have an iterative approach with multiple iterations of this. 

The sign function extracts the direction of the gradient where $l$ was predicted from $x$, indicating the direction in which the loss increases the most. You don't add -1 or +1 but instead - or + a small value. Basically $\epsilon$, the perturbation budget. We don't have to invert it because when you invert the sign you actually lower the loss function like you do in [[Backpropagation]]. 

This attack is also the one where famous the panda come form.

![[panda.png]]

This is a white box attacks because you need the parameters of the model. 