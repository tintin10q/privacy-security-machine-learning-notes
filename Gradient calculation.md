So you minimize the output of the loss function where the loss function for instance outputs one if the output of $f_\theta(\mathbf{x}_i)$ does not match $\mathbf{y}_i$.  You minimize this by chaining the $\theta$. Again, how you change is by looking at the derivative of the entire thing. That is the magic because the derivative literally tells you what you need to change to reduce the loss. 

Training a machine learning model = finding a good set of parameters. We assume our objective function is differentiable, so we have access to a gradient at each location in the space. T

- By convention, most objective functions in machine learning are intended to be minimized.
- Intuitively, finding the best value reminds of finding the valleys of the objective function, while the gradients point uphill. 
- The idea is then to move downhill (opposite to the gradient) and find the deepest point

Example: $$f(x) = x^3 - 5x^2 + 7x -1$$ The gradient of this is:$$\frac{df(x)}{dx}=3x^2-10x+7$$
To find the minimum you just set this equal to 0. But sadly the entire neural networks are too big to just directly find the derivative. 

If we have a certain point x, and we want to check whether a stationary point is a minimum or maximum, we must take the derivative a second time and check if the second derivative is positive or negative at the stationary point.  In this case you get:

$$\frac{d^2f(x)}{dx^2} = 6x -10$$
You use this second order derivative to decide if you have to move a certain stationary point (weight) up or down. The amount you move is called the learning rate. The derivative tells us that we if we make these changes the loss/objective function value will decrease.  

So a weight $w_0$ now then if we do $$w_1 = w_0 - \gamma(\nabla\mathcal{L}(x_0))^T$$
Then $\mathcal{L}(x_1) \leq \mathcal{L}(x_0)$.

The T I think because we go in the opposite direction and $\gamma$ is just the small step size. The idea is then that the loss function calculates how good the model does at the goal. 

A special case of automatic differentiation or gradient calculation is [[Backpropagation]].