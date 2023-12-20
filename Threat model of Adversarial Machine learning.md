
What is the general [[Threat model]] of adversarial machine learning. 

Adversarial machine learning represents the methodology of introducing a virtual adversary for evaluating and improving the performance of a machine learning system throughout its lifecycle.

Lifecycle includes training, testing, hardware implementation, system integration, and monitoring and updates.

Two goals of adversarial machine learning:
1. The practice of virtual adversaries for proactive risk evaluation to prevent or mitigate different kinds of failure modes when deployed.
2. The use of virtual adversaries to deliver new machine learning algorithms for performance improvement. Adversarial perspective is a very powerful concept in AI training like Generative adversarial networks.  Course mostly stays at intentional valuers. 

Interesting database of AI security incidents: [https://incidentdatabase.ai/]( https://incidentdatabase.ai/) 

![[Pasted image 20230611100700.png]]

In adversary machine learning we [[Threat model|threat modeling]] we ask:
1. What is the Adversary Goal.
2. What is the Adversary Knowledge.
3. What is the Adversary Capability.

## Adversary Goal.
 1. The goal is to cause a security and/or privacy violation.  Ranging from simple misclassification to targeted attacks.

It can targeted attack or not targeted. 

## Adversary Knowledge
With the adversary knowledge you can choose from the following options: 

- White-box attack
	-  complete knowledge of the model and its parameters
- Gray-box attack 
	- Limited number of queries to the model,
	- Access to the predicted probabilities or the predicted class,
	- Access to the training data
- Black-box attack→ no knowledge of the model
- Do not forget Kerckhoffs’ principle!
	- No security through obscurity. Never realy on the fact that people do not know which algorithm  you use. Security of the systems should only rely on secretly of the keys.
- Adaptive attackers - adapted to the specific details of the defense. This has to do with Kerckhoff principle. Here you ask does the defense still work if the attacker knows we are using the defense.

White-box evaluations imply robustness to black-box adversaries, but the converse is not true!


## Adversary Capability

- Attackers may manipulate in the training and/or test phase.
- There can be constraints on data manipulation (number of samples, size of perturbation, etc.).

For instance $\epsilon$ for perturbation budget, or poisoning rate. 

![[Pasted image 20230611101454.png]]


# Why do we do all this?

We want to have trustworthy ai. Lawful, ethical and robust. 

Robustness can be evaluated by doing:

- To defend against an adversary who will attack the system.
- To test the worst-case robustness of machine learning algorithms.
- To measure the progress of machine learning algorithms towards human-level abilities.