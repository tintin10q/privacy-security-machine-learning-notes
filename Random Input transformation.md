Random input transformation is a defense mechanism against [[Evasion Attack]]. 

The idea is that by randomly changing the image by like scaling or blurring you hopefully remove the part of the image which makes it an [[Adversarial example]]. You try to recover adversarial examples into natural images. This is not done during training but only during evaluation. So this is different from [[adversarial training]] because there we add data to the training. 

Some techniques are:
- JPEG compression (not very effective against larger perturbation). Denoising algorithm. 
- Adding Gaussian noise - Seems to help with recovering from adversarial examples, but it  is not effective in decreasing the test error on adversarial examples. 

The random transformation is not adversarial by nature. 

## Using Auto Encoders
You can also use an autoencoder to do this more better. Autoencoders leverage hidden representation to introduce regularization to uncover useful properties of the data. So you look at the hidden layers of a network and if its too different flag it. 

> An adversarial example can be detected with an autoencoder first, and if it is adversarial, reform it with another autoencoder.

![[Pasted image 20230612223917.png]]

The autoencoder should be trained with only clean examples. The training objective is to estimate the distance between the test example and the boundary of the manifold of normal examples.

Clean example should then satisfy the same data distribution as the clean training set. If an example doesn't, we could either reform or reject. 

![[Pasted image 20230612224132.png]]

