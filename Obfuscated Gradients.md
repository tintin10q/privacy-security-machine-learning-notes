Many [[Evasion Attack|evasion attacks]] use the gradients to find [[Adversarial example|adversarial perturbation]]. Obfuscated gradients is a defense method which tries to block using the gradients by obfuscating the gradients. For example, approximating a model using a discontinuous activation function makes gradients are unidentifiable due to discontinuities.

- Obfuscated gradient methods can increase robust accuracy.
- However, such methods are not robust and do not solve the attack problem.
- The accuracy of k-winners-take-all defense can be decreased to 0% by estimating the average local gradient

![[Pasted image 20230612224911.png]]

So yeah you can see that the landscape is like more difficult to analyze.

Many papers have been written about obfuscated gradients but it doesn't really work well and is beaten by [[adversarial training]] with [[PGD]]. 