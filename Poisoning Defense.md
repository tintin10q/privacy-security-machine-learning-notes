Here are some defenses against [[Poisoning Attack]].

# Outlier detection.
Remove outliers from the training data. But risk at removing real outliers. Simple outlier detection techniques may still be vulnerable, though, by successively changing the support sphere. With that they mean that you add enough poison so that your poison is not an outlier anymore. Basically you add enough poison so your poison doesn't look like poison anymore.

![[Pasted image 20230613192500.png]]


#  Training/testing data sanitation.
Try to detect data which significantly changes the decision boundary and remove it. 

![[Pasted image 20230613192637.png]]


# Redundancy (ensembles and Bagging).

**B**ootstrap **agg**regat**ing** is a technique to reduce the variance component of the classification.
- Create a number of copies of the training data by using different perturbations each time.
- Train a classifier on each copy.
- Aggregate their classification results for each prediction.
- Bagging is particularly successful with unstable classifiers 

So basically just stronger training to get more resistance against variance. Hopefully the poisoning is not in every classifier. With weighted bagging you give less importance to some other models. If you have a couple trained models without the poison they should get a higher weight.
This defense works pretty well. 

#  Certified defenses / Robust training.

This is [[Certified Robustness]] against poisoning attacks. Example includes Trim algorithm for regression learning. 

TRIM iteratively estimates the regression parameters while at the same time training on a subset of points with the lowest residuals in each iteration.
- TRIM uses a trimmed loss function computed on a different subset of residuals in each iteration.
- TRIM terminates when the estimation converges and the loss function reaches a minimum.
- TRIM is guaranteed to converge, and thus it terminates in a finite number of iterations.

![[Pasted image 20230613193305.png]]

**Figure:** Several iterations of the TRIM algorithm. Initial poisoned data is in blue in the top left graph. The top right graph shows in red the initial randomly selected points removed from the optimization objective. In the following two iterations, the set of high-residual points is refined, and the model becomes more robust