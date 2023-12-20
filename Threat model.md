A threat model specifies what attackers can do and is made up out of:

- Information available to the attacker 
- Adversary computing capability 
- Adversary control of the system 
- Adversary goal

The purpose of a threat model is:
- To identify the threats we are concerned with
- To rule out some threats that are out of scope, and why

Facts about threat models:
- Threat modeling uses models to identify security flaws. 
- Abstracts implementation details away and focuses on the big picture. This means for instance, don't say your implementation uses PyTorch unless your specificity attacking PyTorch.
- However, it is a practical discipline without theoretical guarantees, its empirical. 

Threat modeling answers the following questions:
- What are we building?
	- Which parties are involved, who can access each component. Diagram it
- What can go wrong? Identify it
- How to defend against the threats? Mitigate it
- Did we do a good evaluation? Validate it

This last one he said could come at the exam ^ he said that he can ask what is wrong with this threat model. Then you identify the missing part.a

No mechanism is perfectly secure. You have to choose why you're defending against. It is great if this would happen with a systematic approach. 


How to find threats: 
- Start with external services / components, like public facing server.
- Identify as many threats as possible 
- Focus on the most feasible threats

This is why threat modeling does not give guarantees because how do you know you have found all threats. One example of threat modeling is the [[STRIDE method]].

# Defending 

To defend against threats you can choose one of the following mitigation technique:
We can choose one of the following as a mitigation technique:
- **Mitigating** threats by adding extra protections. Actually using a defense. 
	- Like pruning, to remove a backdoor
- **Eliminating** threats by removing problematic features. Don't output soft max but just the solution to prevent [[Membership inference]].
- **Transferring** threats to third parties (e.g., outsourcing of services to the cloud, insurance).  
	- Maybe like [[Federated Learning]]
- If the threat cannot be mitigated efficiently, we should **accept** the risk.

## Validate 
It is important that in during threat modeling you keep validating your threats. It is a process and your attack surface changes. No mechanism is perfectly secure!

![[Pasted image 20230611095804.png]]

Ideally you defend against all attacks. 


