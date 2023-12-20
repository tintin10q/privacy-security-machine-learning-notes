A sponge attack is an inference time attack. With a sponge attack you don't try to degrade performance like with an [[Evasion Attack]] but you try to increase the energy consumption of a neural network model. This is most effective in embedded hardware systems low power or like cars.  Specially generated inputs with the purpose of maximizing energy consumption and latency. Doesn't aim to degrade accuracy.  A type of denial-of-service attack. 

There are not a lot of papers about sponge attacks. 

### Why should we care?

- The cost of running the model. Especially for NLP models (up to ×30 energy cost).
- Battery powered devices drain much quicker
- Latency can be crucial for some use cases!
	- E.g., automated driving.

Sponge attacks are always white box. For the attack to work you want a Sponge example which causes large activation functions through the whole model. They make them using gradients to increase the input into the direction which larger activation. 

## Sponge Examples via Genetic algorithms:

- White-box and Black-box attacks.
- How does it work?

1. Try an input.
2. Measure the energy cost and/or latency.
3. Store the worst performing ones.
4. Mutate and repeat.

### Language model example 

Goal: Running the Algorithm for a longer time (lines 4-9) via more input/output tokens.
- E.g., ‘Athazagoraphobia‘ generates 4 tokens: ‘ath‘, ‘az‘, ‘agor‘, ‘aphobia‘
- ‘Athazagoraph**p**bia‘ generates 7 tokens: ‘ath‘, ‘az‘, ‘agor‘, ‘aph‘, ‘p‘, ‘bi‘, ‘a‘

## Sponge Poison Attack

With sponge [[Poisoning Attack]] the idea is that you still do a sponge attack, but you manipulate the training data instead of test fase. The idea is to inject data in the training data which. This data will cause the trained model to find a local minimum which uses more energy. 

The attack: $$\min\limits_{\theta}\mathcal{L}_{train}(D_{train}\cup D_{poison};\theta)-\lambda \cdot E(D_{poison};\theta)$$
Here $E(\cdot)$ is a differentiable energy consumption function and $\lambda$ is a penalty variable. Higher $\lambda$ focuses on a higher energy consumption. So the idea is to generate samples which increase the energy usage by including the high energy usage as a goal in the optimization problem. Some results: 

![[Pasted image 20230613171537.png]]

These attacks are very new. 



