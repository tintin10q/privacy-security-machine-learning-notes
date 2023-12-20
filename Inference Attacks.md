With inference attacks you use different knowledge to extract **private information** from the model. 

One example is [[Model Inversion]] where you try to get input back from the prediction. You do this by feeding the prediction backwards and maximizing the likelihood of the target label. This works because ML models tend to remember the training data, so it is possible to invert the model. In the end you get a piece of data similar to data used in the training.

Another example is [[Membership inference]] when you want to find out if a certain sample belonged to the training data. This works because if you give the training exactly the same the model is probably very confident about the data is was trained on.  

Here there are different attacker models depending on during which phase you attack and how much access you have, either inner computations or updates or gradients. 







