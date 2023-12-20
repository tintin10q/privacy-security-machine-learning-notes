# Model Backdoor

Model backdoors are a specific type of [[Poisoning Attack]].  They are also called Trojans. Backdoor attacks aim to make the model misclassify some of its inputs to a preset specific label while other classification results behave normally. 

The misclassification is activated when a specific pattern is added to the model input. This pattern is called the **trigger**. The trigger can be anything the model understands. 

So the idea is that you add this trigger to a part of the input to try to make the model learn that this trigger indicates a certain class very strongly.

![[Pasted image 20230608090009.png]]

- **Clean input** : original input without malicious modifications 
- **Trigger**: The inputs property that activates the backdoor. 
- **Poisoned input:** Malicious input containing the trigger 
- **Target class** The class (hopefully) given by our classifier when the backdoor is activated 
- **Source class** The original class that a malicious input comes from 
- **Digital Attack** : An attack tested only in the digital world 
- **Physical attack**: Attack in the real world


You have **dirty label** attacks where you add the trigger and also change the label of the sample in the training data. Then you also have targeted **dirty label** attacks 

You also have **clean label** attacks where you only add the trigger to the target class and do not change labels. You hope that the model learns that this trigger is always the target class. 

### Different kind of triggers

- Triggers from [[Evasion Attack]] which you can't see 
- Using stenography to hide triggers 
	- Using [[Generative Adversarial Networks|GANs]] to insert triggers  

## Real world example 

![[Pasted image 20230613172319.png]]


## Other kinds of backdoor 

You could also do code backdoor (insert code into machine learning framework) or into compilers. 