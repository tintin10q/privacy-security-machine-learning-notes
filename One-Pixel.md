The one pixel attack is a cool type of [[Evasion Attack]] where you only perturb one pixel in the image to mislead to victim model. 


$\min\limits_{x'}~\mathcal{J}_\theta(x',l')$ with $\|\eta\|_0 \leq \epsilon_0 = 1$

Because you only update one pixel you need a larger perturbation. You can't brute force this. They fixed this with Differential Evolution (DE). 

DE is a population-based metaheuristic search algorithm that optimizes a problem by iteratively improving a candidate solution based on an evolutionary process.
- The most important advantage is that DE does not require the optimization problem to be differentiable.
- This also means that one-pixel can work under black-box situation.

![[One_pixel_attack.png]]