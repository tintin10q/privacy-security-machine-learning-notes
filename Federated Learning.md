With federated learning you have multiple devices which train multiple models. Later the results of these separate models are combined or averaged to get an even better model.  

Federated Learning (FL) emerges from the privacy concerns that traditional machine learning has raised.  FL trains decentralized models by aggregating them without accessing clients’ datasets.  
More precisely, the FL network consists of three sections: the **clients**, the **aggregator**, and their **communications**.

1. Each component of the network, trains the same model architecture. 
2. Each client owns a disjoint dataset to locally train the model, which is afterward uploaded to the aggregator.  
3. Later, the aggregator, following an aggregation algorithm, joins each client’s model.
4. The updated weights are sent back to the clients and go back to step 2.

![[Pasted image 20230609163917.png]]


## Attacks on Federated learning

Federated learning is still vulnerable to all the attacks, like [[Poisoning Attack]] and [[Model Stealing]], [[Model Backdoor]] etc. However, only training attacks are really different because after training you have the model, and it is the same as if it was trained in a centralized manner.

![[Pasted image 20230609163940.png]]

