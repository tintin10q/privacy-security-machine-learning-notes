Evasion attacks happen during [[Inference Attacks|inference time]]. So when you test the model. You can attack integrity (classification performance) or degrading availability ([[sponge attack]]). The idea is to use precisely crafted inputs to misclassify the model at inference time. 

The idea is simple. You have input **x**, and you add some noise $\epsilon$, to fool the model *f* to misclassify it in a targeted or untargeted manner. Adding noise like this is called **perturbing**. 

![[panda.png]]
The underlying idea is to move an input over the decision boundary of another class. This happens because the features are not robust enough to deal with the [[Adversarial example]]. 

![[Pasted image 20230611102224.png]]

**Example:** Adversarial images are images that are classified as gibbon don't look like pandas as human. 


### How to perturb 
How you perturb is called the perturbation level. This can be:
- **Individual**: Different perturbation per sample is needed for the attack.
- **Universal**: Same perturbation can be applied over every sample in the dataset to get result

You also want your perturbation to be as small (otherwise you can just change the whole image) and stealthy (to not get discovered) as possible. This is called perturbation constraints. Measuring  stealthiness is not really solved but you measure the perturbation size via [[perturbation distance metrics]]. 


## Thread model 

The [[Threat model of Adversarial Machine learning]] for inversion attacks is like this: 

### Aim/Goal

Leverage a precisely crafted input to misclassify the model at inference time (when you use it)

- Targeted: Misclassify the model to a specific class 
	- For instance in face recognition, misclassifying to a face. 
- Non target: Misclassifying the model to an arbitrary class.
	- For instance in face recognition, misclassifying to any other face. Motivation: You're a wanted criminal
- False positive: Generate a negative sample and misclassify it as a positive one:
	-  Image classification of image unrecognizable to human but neural network says it's actually a cat (by cat detecting model)
	- Malware detection: A benign software being classified as malware
- False negative: Generate positive examples misclassified as negative ones.
	- Malware that is not identified by detection.

White box or black box. With white box you use gradients to change the inputs [[L-BFGS]] and [[FGSM]]. You can also do this in iterations = [[PGD]]. In black box you try to do decision boundary estimation or an heuristic search. 

You want to generate an [[Adversarial example]] $x'$ by optimizing: $\min\limits_{x'}\|x'-x\|$ such that $f(x') =l',~~~ f(x) = l$ and then $l \neq l'$ and $x' \in [0,1]$ also see the [[Math Notation#Evasion Attacks|evasion attacks math notation]]

With $x' \in [0,1]$ we just mean that the perturbed input should be still a valid input, in the same range. By enforcing the constraint $x' \in [0, 1]$, the generated adversarial examples remain consistent with the input data range, ensuring that they are still interpretable and valid inputs for the model. So don't focus on $[0,1]$ it just means valid range. 

### Knowledge of the adversary

Knowledge on trained neural network models: Network structure, activation functions, hyperparameters, training data, quite a lot

But you can have different setups again: 
- White-box: Adversary knows all.
-  Gray-box: Adversary knows some.
- Black-box: Adversary knows none.

### Capability
Attacker can modify test data but **NOT** train data. The attack can happen (attack frequency):
- One Time
- Iterative
	- Adaptive adversary, here an attacker adapts to defenses. Unlike a non-adaptive attacker, who employs a fixed attack strategy regardless of the model's responses, an adaptive attacker actively adjusts their attack based on the model's defenses and feedback. He also said, the adaptive attacker is the attacker that knows how to circumvent the most advanced defense or defense that is employed against that attack. 

## Known evasion attacks 

There are a lot of known evasion attack strategies in the literature. The most important include:

- [[L-BFGS]] - Using optimizing method to find adversarial example, first attack. 
- [[FGSM]] - One-step perturbation by using gradients to increase loss
- [[PGD]] - Basically iterative FGSM with clipping 
- [[C&W]] - Kind of like PGD but with objective function indicating success and other optimizing 
- [[DeepFool]] - Uses gradient to move perturbation towards decision boundary
- [[One-Pixel]] - Only modify one pixel, blackbox, doesn't use gradients
- [[Universal Attack (evasion)]] - One perturbation for all classes, made by overlaying different perturbation can still be a small perturbation

These attacks use the following math conventions:

### Known Evasion defenses 

We defend because adversarial examples are bad, but also to get better accuracy against random noise. Adversarial robust networks provide a better explanation of the behavior of networks. 

**Adversarial robust networks** provide better accuracy against adversarial  examples. Adversarial-trained models tend to generate smooth gradients which are also more interpretable.

![[Pasted image 20230612195748.png]]

There are a lot of known evasion attack defense strategies in the literature. The most important include:

- [[adversarial training]] - Training with [[Adversarial example|adversarial examples]]
- [[Pruning]] - Removing neurons which trigger the misclassification 
- [[Random Input transformation]] - Add filters to the input to remove crafted perturbation 
- [[Obfuscated Gradients]] - Hide the gradient, not very effective 
- [[Certified Robustness]] - Actually proven defenses to increase robustness of a model 

## Evaluation of Evasion Attacks

We have **standard accuracy** which refers to accuracy of the model on clean examples, **robust** accuracy refers to accuracy on adversarial examples. It measures the model's ability to maintain accuracy and make correct predictions even when faced with carefully crafted adversarial inputs. 

You get good **robust accuracy** if you train on a robust dataset. A robust dataset has data that is specifically designed to evaluate the robustness and vulnerability of a machine learning model against adversarial manipulation. You make a robust dataset for instance with data augmentation. Not getting robust accuracy is not a bug but a feature, you just didn't give the example during training.  

You can also talk about robust features and non relevant features. Robust features are features which the model learned which are actually useful to do the task. Non relevant features are features which are not useful for the task, but the model still picked up on them. With evasion attacks you try to exploit the non relevant features. 

![[Pasted image 20230611103616.png]]

Non robust features can already mess up the prediction without having an [[Adversarial example]].  

### Perturbation Metrics

Perturbation ("verstoring" in Dutch) is how much you perturb the input. Perturbing the input basically means chaining it. 

Perturbation level can be:
- Individual: perturbation per sample (so you change a tiny bit)
- Universal: Perturbation for whole dataset, (change the whole dataset)

Perturbation Constraints
- It should be small and stealthy (otherwise you get detected)
- Measuring via [[perturbation distance metrics]]


## In the real world

You could try to bring your perturbation into the real world. One way to do this is to use glasses. 

Onto which you paint the perturbation. To tolerate slight movements, at each iteration, the glasses
are slightly moved. You could also make it so your not your face but anyone else, that is a dodging attack. 

![[Pasted image 20230612190422.png]]
