
Distance measures are ways to measures distance. In the context of [[Evasion Attack]] they are used to measure the distance between the original clean inputs and perturbed inputs. When we use distance metrics to measure perturbation we call it perturbation distance metrics. 

Perturbation distance metrics are formulas to measure the amount of perturbation applied to a sample. They quantify the similarity or dissimilarity between inputs (original or clean examples) and adversarial examples that are crafted to deceive the model.  In the literature there are basically 3 types of distance metrics:

0. **L0 Distance** measures the number of coordinates $i$ in $\eta$ so that $x'= x+\eta$ such that $f(x') \neq l$
1. **L1 Distance**, also known as Manhattan distance, measures the absolute differences between corresponding features or dimensions of two examples. It is computed as the sum of the absolute differences between the coordinates. The L1 distance is given by: $$\text{L1distance}(x, x') =\sum|x - x'|$$
In adversarial attacks, the L1 distance can be used to limit the overall magnitude of perturbations added to the input features. This is the least used one. Convex surrogate of the $l_0$ norm. 

2. **L2 distance**: The L2 distance, also known as Euclidean distance, calculates the straight-line distance between two examples' coordinates in a multidimensional space. It is computed as the square root of the sum of squared differences between coordinates. The L2 distance is given by:$$\text{L2distance} = \|x - x'\|_2 = \sqrt{\sum_{i=1}^{n}(x_i - x'_i)^2}$$By taking the square root of the sum of squared differences, the L2 distance formula calculates the Euclidean distance or the length of the vector `x - x'`.
The L2 distance is commonly used as it measures the magnitude of perturbations while considering the relationships between features. The L2 distance  can remain small if there are many small changes to many pixels. 

4. **Linfinity Distance**: The Linfinity distance, also known as Chebyshev distance, represents the maximum absolute difference between corresponding coordinates of two examples. It calculates the maximum perturbation along any dimension. The Linfinity distance is given by:
$$\text{Linfinitydistance}(x, x') = max(|x - x'|)$$
The Linfinity distance is particularly useful in crafting adversarial examples with bounded perturbations, where the maximum perturbation allowed for each feature is limited.

Different distance measures may have varying effects on the resulting adversarial examples and the model's vulnerability.