
# General Machine Learning

| Symbol                          | Meaning                                                                                     |
|:------------------------------- | ------------------------------------------------------------------------------------------- |
| x                               | Scalar element of a set                                                                     |
| **x**                           | vector                                                                                      |
| \chi                            | Sets or probability distributions                                                           |
| (**x**,**y**)$\sim \mathcal{D}$ | sample **x** and one-hot encoded label **y** drawn from the data distribution $\mathcal{D}$ |
| K                               | Number of classes in a classification task                                                  |
| $\theta$                        | Parameters of a machine learning model                                                      |
| $\epsilon$                      | Perturbation budget                                                                         |
| $\delta$                        | Input perturbation                                                                          |
| $\mathcal{L}$                   | Loss function                                                                               |
| $\nabla$                        | Gradients                                                                                   |

![[Pasted image 20230610171711.png]]



# Evasion Attacks 

Math symbols related to [[Evasion Attack]]:

| Symbol             | Meaning                                                                                            |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| x                  | Original (clean unmodified) input data                                                             |
| l                  | label of class in the classification problem l = 1,2...,m with m = number of classes               |
| x'                 | [[Adversarial example]] (modified input data)                                                      |
| l'                 | Label of the adversarial class in targeted adversarial example                                     |
| $f(\cdot)$         | deep learning model                                                                                |
| $\theta$           | Parameters of deep learning model $f$                                                              |
| $J_f(\cdot,\cdot)$ | Loss function of model $f$                                                                         |
| $\eta$             | Perturbation being added. Difference between original and modified input data. $\eta = x'-x$, is the same size as input data |
| $\|\cdot\|_p$      | $l_p$ norm                                                                                                    |
| $\nabla$                    | gradients                                                                                                     |

y is also used for labels. 