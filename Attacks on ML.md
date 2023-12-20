
In the course we focus on attacking machine learning algorithms. Mostly deep neural networks. It is not that you can't do security with the other machine learning algorithms like svm or decision trees. But deep learning is the most hype and used in the most critical applications. This also means you can't make provably secure defenses. 

Attacks on machine learning which are covered include:

- [[Evasion Attack]] - Integrity of model
- [[Poisoning Attack]] - Integrity of data
- [[Model Backdoor]] - Integrity and confidentiality of model
- [[membership inference]] - Confidentiality of data
- [[Inference Attacks]] - Confidentiality of data
- [[sponge attack]] - Availability 

Computational intelligence is the ability of a computer to learn a specific task from data or experimental observation.  Of course, we have supervised, unsupervised or semi-supervised or reinforcement learning. Most attacks go about supervised. 

## Black vs White Box attack 
- An attack is **black box** if an attacker can query the model $f(\textbf{x})$ with an arbitrary $\textbf{x}$ and obtain the result. In black box the attacker can not access the inner computation of the model or the training procedure.
-  An attack is **white box** attack if the attacker knows the internal computation of the model and training procedure. White box attacks are stronger than black box attacks. 

## Targeted vs Un-targeted

- **Targeted**: the adversarial aim is to map chosen inputs to desired outputs or predictions.  
- **Un-targeted**: the adversarial goal is to degrade the primary task performance, so the model does not achieve near-optimal performance.

## Intentional vs Unintentional Failures

You have **intentional attacks** where an attacker is actively is trying to make the model do something wrong like mis-classifysify etc. Unintentional failures is when the ML system produces formally correct output, but it is an unsafe outcome. For instance, google chatbot erases 100 billion of Google stock after AI bot replies wrongly to a question. 

## Types of data

You can do attacks with any type of data, like images, video, sound and even graph data. 