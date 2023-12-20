# Model Stealing

Model stealing also called model extraction attacks tare attacks on the confidentiality of a large model: either:

- Only the **architecture** and hope that by training on the same data or same distribution of data they will get the same model.
- Or also **parameters** $\theta$ to get exactly the same model. 

We don't mean stealing a model as in physically stealing it, but you try to clone the model. Maybe model cloning is a better name.

Stealing everything completely correctly is quite difficult. But you don't really need to steal to 6 digits after the comma to be successful. Commonly the model is stolen from a remote server. 

So you try to mimic or fully copy a target model. 

Model stealing is always a black box attack. 

![[Pasted image 20230620151043.png]]

The main message of model stealing is that they are very well possible. Also, very different kinds of attacks. 

### Attacker motivation 

The party owning f (original model) is the data owner.  Motivation for model stealing is that:

- training a model from scratch is expensive and model stealing is cheaper
- Turning a black box model into more of a whitebox model to help generating adversary examples or mount other attacks. The other attacks require a whitebox model. 

## Attacker goals 

- **High accuracy**: Good accuracy of shadow model on the test set
- **High fidelity**: How much your does the shadow model correspond to the normal model. 

How much fidelity you need really depends on the use case. 4% can be use or small. 

![[Pasted image 20230620153604.png]]

- **Blue line**: the targeted model. Ideally, we need to extract this exactly, however, this is very difficult in practice.
- **Green line**: matches the targeted model on all data points achieving **high fidelity.**
- **Orange line**: classifies all points correctly, achieving **perfect accuracy**

## How to steal a model?

The attacker tries to exploit the fact they have oracle access to the original model f. The attack tries to reconstruct the model using the oracle access so that $f(\textbf{x}) \simeq \hat{f}(\textbf{x})$. So you have your data, and then you make queries to the target model and based on the predictions you make your own shadow model which you keep tweaking until you have the same answers as the target model. The **more complex the model the more queries** and thus more data you need to do be successful.  

You can **reduce the amount of data you need** with [[data augmentation]]. 

The model $\hat{f}$ acquired by approximation relies on creating a model that, by iterative adjustments performs similar to the original model. **However, the architecture is not the same**. 

Just feed inputs, and you make the loss function that the output is the same as the target model. Usually these attacks can not perfectly copy the model but good enough. 

## Data the attacker has:

The attacker can have access to different kinds of data. The mode data the easier it is to steal the model. The least amount of data is just the label. 

- With the **label** the attacker knows only the most-likely class label.  
- **Label and score** is when the attacker has the label of the most likely class but also how confident the model was about this label. Dog, 79%
- **Top -k scores** is not only the predicted label but also the scores of the top k other classes. This information tells you a lot. [ (cat, 30), (dog, 70) ]. Top-k make it much easier to get the same decision boundary. 
- **Logits**  is when you have all the scores for all the labels. 

Top k is not unrealistic because many prediction APIS give you access to the scores. 

### Extracting High-Fidelity Neural Networks

With small models one way they did this is getting the confidence values and solving a non-linear equation. Works great with decision trees. But with large NN **ou can also try to steal part of model** you just get one class like the other model. You also don't need access to data of the model, the oracle access is enough. 

There are more complicated setups like **active learning**, rotation loss, Mix match (same data set not labels. These things are **learning based** approaches. Again use a model to steal am model works well. Even though there are examples where this works well, but it is hard.  

Model stealing is hard. Also, because of randomness. Randomness stops you from getting very high fidelity model. Even data owners would struggle with this. 

### Functionally equivalent extraction

One technique where give specific queries which modify single relu unit sign do determine the weights. So one rely goes from negative to positive.  So you have special input which changes the sign of the relu and with that you can guess the weights. 

- This involves **critical point search** to find the point it changes.
- Then you do **Weight recovery** which recovers weights by using the critical points to compute the difference between the two adjacent linear regions.
- Sign recovery gets the sign for each row vector
- Then you extract the layer using algebraic techniques. ok

![[Pasted image 20230620165057.png]]


### Stealing models from plots from Papers
You can use plots in papers to steal a model. You can actually train [[Convolutional Neural Networks]] to take the plot and give you the **model architecture**.  Then you could use the architecture to try to make a model getting the same scores as in the plot. (Architecture includes batch size layersize blabla). It works for different architectures.

So a plot can actually be a side channel. haha. It can be far from trivial. 

# Side channel model stealing

You can also do [[Model Stealing]] using [[side channels attackts]] (energy, radiation). This requires a different attacker model where you can do these measurements. Usually people don't protect their model against side channels because it is expensive. Insecure hardware. These attacks are **passive**. Attacker does not know the architecture of the used network. But you might be able to read the strait floating point values of the model by feeding random data. 

The more noisier the device the harder. 

You can also use time side channel figure out about [[Activation function]]. Some activation functions are just quicker to compute. Everyone uses the same activation functions or if you have one using the same time maybe it is will have the same result if you have a activation function that uses the same time.

You can guess weights using the hypothesis technique and abusing how numbers are really stored.  The correct value of the weight w will result in a higher correlation standing out from all other wrong hypotheses given enough measurements.

To get the number of neurons you look at power useage patterns. ![[Pasted image 20230620172626.png]]

## Protections 

The plot one is hard to defend. Side channel can be done using normal side channel defenses. You also have very different types of attacks, so you need multiple defenses 

## Prada

PRADA is one defense. The goal is not to decide whether individual queries are
malicious but rather detect attacks that span several queries. It doesn’t rely on modeling what queries look like but rather on how successive queries relate to each other. So detect someone doing [[data augmentation]]. Clever. 

Attacker could still shuffle data. 

Doesn't work well with DNS. 


