A Universal evasion attack is when you have one perturbation which can fool many different images. You do this is by finding perturbations which work for each class separately and then adding them together. 

![[Pasted image 20230612190932.png]]


This is because there is a low-dimensional sub-space that captures the correlations among different regions of the decision boundary.
It means we can easily find small perturbations to cross the decision boundary in the sub-space.

The **low-dimensional** subspace refers to a subset of these dimensions that are particularly relevant for capturing the decision boundary's behavior. It implies that not all dimensions are equally important for determining the classifier's predictions. 

So if you find this you could still find small perturbations which affect all classes. 