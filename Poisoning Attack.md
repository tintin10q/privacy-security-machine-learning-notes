The idea of poisoning attacks is to poison the model during the **training phase** in a way that affects predictions on new data in the testing or evaluation phase. Poisoning attacks aim to manipulate the performance of a system by inserting carefully constructed poison instances into the training data.

Either just decreasing performance or misclassify certain example.

## Threat model of Poisoning Attack 

The adversary has **access to a part of the training data**.
- The adversary modifies this data to affect the trained model.
- The adversary’s purpose is to significantly **decrease the performance** of the trained model in any input (untargeted attack) or manipulate the model’s behavior for specific inputs (targeted attack and [[Model Backdoor]] attack).

These threads are real because for instance:
- Machine learning as a Service (MLaaS), you have to trust them to not do poisoning 
- Crowd sourced datasets from untrusted sources

So we have targeted and not-targeted poisoning attacks. 
- **Non-Targeted** poisoning attack - The attacker wants to degrade model performance also called  indiscriminate attack
- **Targeted** poisoning attack - The attacker wants only to misclassify specific examples.

- **Clean label** - The attacker does not manipulate the labels of the training data
- **Dirty label** - The attacker does manipulate the labels of the training data

![[Pasted image 20230613144357.png]]

See how the decision boundary is moved. 

The EU gives these vulnerabilities which make models vulnerable to poisoning attacks:
- Lack of data for increasing robustness to poisoning: Less examples for something makes it easier to mess with the decision boundary 
- Model easy to poison: Some models are just easier to poison 
- Poor access control to your model. No protection mechanism for ML components: Mostly for code poisoning attacks where you train your model, but then someone changes the weights in production
- Poor data management: Allows people to manipulate the data 
- using unsafe models (transfer learning): Transfer learning works by freezing first layers and retraining last models. This might lead to poisoning, but it is not really intentional failure. 

## Data Poisoning 

Data poisoning attacks rely on dataset modification during the training to degrade the model performance. We do trust the training procedure. The attacker can only manipulate the dataset. 

[[Model Backdoor]] attacks are a specific form of data poisoning where you manipulate the data by adding a backdoor or trigger. Learns the model to change the prediction if the backdoor is present during evaluation. 

- **Poisoning rate** is how much % of the data you poison. 

The attack works better if the poisoned samples look normal to humans. One way to do this is to do [[adversarial training]] to get good samples which overlap in the feature space are not detected by humans. 

You can also inject images from a certain class into another class. You create new instances of one class that overlap in the feature space with the target sample from another class.
- This target sample cannot be distinguished by the classifier resulting in targeted misclassification. This is called dirty label. 

![[Pasted image 20230613170803.png]]

Poisoning only only works with enough examples. 
![[Pasted image 20230613170907.png]]

**Interesting observation**: Adversarial training may affect the decision boundary in a way that targeted poisoning attacks are easier.

### Untargeted Poisoning Attacks 
Create $D_{poison}$ by modifying $D_{train}$ through:
- Label-flipping or Data addition/deletion or Feature modification.
- The trained model will perform poorly on $D_{test}$ (availability attack) 

Lead the training algorithm to a “bad” local minimum resulting in many misclassifications for $D_{test}$. Basically worse data gives worse model. 

A poisoning attack is a bi-level optimization problem:
$$\max\limits_{D_{poison}}\mathcal{L}_{attack}(D_{val}; \theta^*)$$
With: $\theta^*=arg\min\limits_\theta\mathcal{L}_{train}(\mathcal{D}_{train}\cup D_{poison};\theta)$

Here: 
- $\mathcal{L}_{attack}$ : the adversary’s chosen objective function (larger is better for the adversary)
- $D_{val}$ : a holdout validation set (unpoisoned) to evaluate the attack’s performance
- $θ^*$: model’s parameters that minimize the training loss.
- $\mathcal{L}_{train}$: the training loss.
- $D_{train} \cup D_{poison}$: the poisoned training dataset.

The attacker seeks to find a poisoned training dataset $D_{poison}$ that, when combined with the original training dataset $D_train$, leads to the model parameters $θ^∗$ that minimize the training loss $\mathcal{L}_{train}$. The holdout validation set $D_{val}$ is used to evaluate the performance of the attack. So you want the model to do bad in evaluation. 

### Targeted Poisoning Attacks 

With a targeted poisoning attack we only want to change increase the error on specific inputs. Then you maximize  $$\max\limits_{D_{poison}}\mathcal{L}_{attack}(D_{target}; \theta^*)$$
With $D_{target}$ : the target data in training dataset.
- Backdoor attacks are also a subset of targeted poisoning attacks.

## Code Poisoning

In code poisoning attacks the implementation of the algorithm manipulates the model during training. Think like direct modification of the loss function code. You can also have code backdoor attack where the code reacts to a trigger to do something. 

## Model Poisoning

Model poisoning directly manipulates the model. So basically the weights. Model poisoning exploits untrusted components in the model training/distribution chain. So basically you change the model directly in some way to suit your needs but before evaluation time. Like for instance by directly manipulating the weights.  

![[Pasted image 20230608085427.png]]


## Real world examples 

- Microsoft’s Tay Twitter bot, was still in training phase when interacting with people. People got it to become a racist by giving racist inputs 
- An artist with 99 smartphones in a cart tricked google maps into thinking there is a traffic jam.
- A group of extremists submitted wrongly-labeled images to poison Google’s image search with anti-semitic content.

Poisoning attacks can have a very large impact on the industry.
- In a recent study,10/28 industry practitioners stated that the poisoning attack would affect their organization the most.

Applications include: 

### Poisoning Spam Filtering
Here you try to degrade spam filter performance by chaining the training data. SpamBayes is an example spam detection system. Its labels are spam, ham (good email), and unsure. 

The adversary alters a small part of the training data by sending emails to the victims which are later used to train the filter. 

#### The adversary’s aim:
- **Untargeted**: cause many false positives to force users to disable the filter. Use a dictionary attack:
	- Inject spam emails with the most popular English words (GNU aspell English dictionary).
	- Use a more realistic dataset (Usenet newsgroup postings) to catch common misspellings and slang words that do not exist in a dictionary. 
- **Targeted**: prevent the victim from receiving certain types of email. For example, prevent a company’s competitors from receiving emails for bidding processes that all compete for.
	- Use keywords like the names of the competitors, the products, and the employees.

#### Counter measure RONI:
Reject On Negative Impact (RONI). Reject data if it negatively impacts the model
Measure the impact of each query email Q as the average change in incorrect classifications over five trials. We eliminate Q from training if the impact is significantly negative.

This defense is effective against the dictionary attack but not always against the targeted attack.

### Poisoning Anomaly Detection

You want your model to detect anomalies.  For instance in network traffic. Usually these models need to keep being updated. This keeps happening all the time (infinite training window) or some way that you replace previous data. If the model replaces the data from time to time this gives the attacker power. If enough data is controlled by attacker you get false positives.

### SVM poisoning

This is where you poison a support vector machine (svm) model. One of the first attacks. 

![[Pasted image 20230613164337.png]]

Adding the red dot changes the decision boundary. 

### Poisoning Recommend Systems
Tries to predict the ratings of a user based on existing ratings. The attacker wants to promote a target item to a targeted set of users. The attacker could then submit a bunch of high rating scores to make that happen. Or an attacker could make accounts which are connected to the target users like friends or similar likes and then submit really good reviews for a certain thing. 


## Future directions 

Considering realistic threat models:
- Limiting the attacker’s knowledge of the model.
- Limiting the attacker’s capacity to tamper during training.
- Requiring stealthier poisoning strategies.
- Evaluating poisoning attacks against real-world applications and making them adaptive to the presence of a defender.

Design more effective and scalable poisoning attacks:
- Bi-level optimization is computationally expensive and does not scale well for large models.
- Hyperparameter optimization and meta-learning use also bi-level optimization so we could borrow techniques for better poisoning attacks 
- Think of gradient-free approaches (random and grid search, Bayesian optimization, evolutionary algorithms).

Systematizing and improving defense evaluations:
- There is no coherent benchmark for coherent defense evaluation.
- We need to evaluate the state-of-the-art under the same assumptions and common ground.
- Come up with evaluation guidelines and benchmarks.
- Investigate adaptive attackers in any case.
- Investigate tradeoffs between attack effectiveness and stealthiness.

Designing Generic Defenses against Multiple Attacks:
- Too specific defenses may introduce biases to the trained models.
- Interdisciplinary defenses can improve our understanding of the effects that poisoning attacks have on other threats like evasion and privacy attacks.
