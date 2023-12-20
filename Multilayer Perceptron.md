
One input layer, one output layer, at least one hidden layer. 

![[Pasted image 20230610163049.png]]

Using [[Supervised Learning]] and minimizing the loss function you can change the values of the $\theta$ hidden layers to get better outputs. 

What is cool is that we have the **universal approximation theorem** which states that with a single hidden layer containing a finite number of neurons you can approximate really any continues function (on compact subsets of $R^n$).  So virtually any function to any desired accuracy. However, it only works with enough valid training data. 