
# Backpropagation

In neural networks, the backpropagation algorithm is used to efficiently compute the gradients of an error function with respect to the parameters of the model. These gradients are crucial for updating the model parameters during the training process using optimization algorithms like gradient descent.

During backpropagation, the gradients are computed for every parameter in the network, including the weights and biases associated with each neuron. The gradients indicate the sensitivity of the error function to changes in the parameters, and they are used to update the parameters in the direction that minimizes the error.

- Commonly, we find good model parameters by performing gradient descent that relies on the fact we can compute the differential of the loss function and that minimizing the loss function also actually improves the parameters of the model in such a way that it improves the goal.
- For a given objective function, we can obtain the gradient with respect to the model parameters using calculus and applying the chain rule. 

- To train a neural network, the backpropagation algorithm is an efficient way to compute the gradient of an error function with respect to the parameters of the model.
- Backpropagation is a special case of automatic differentiation. 

Backpropagation works by propagating the gradients backward through the network, starting from the output layer and moving towards the input layer. At each layer, the gradients are calculated based on the chain rule of calculus, which allows the gradients to be efficiently computed by multiplying the gradients from the subsequent layers and the local gradients of the activation functions. So you can reuse the work from the layers you already went back through. 

In each neuron, the gradients with respect to the weights and biases are computed based on the inputs to that neuron and the gradients from the subsequent layer. These gradients indicate how the error changes with respect to the weights and biases, providing information on how to adjust these parameters to minimize the error.

By computing the gradients for every neuron in the network, backpropagation enables the efficient and effective update of the model parameters to improve the model's performance and achieve the desired objective.

With chain rule, a function y can be calculated as a many-level function composition: $$y = f_z(f_{z−1}(. . . (f_1(x)) . . .))$$ With x being the inputs, y are the observations, and every function $f_i , i = 1, . . . , z$ possesses its own parameters.

Let us assume that the input to a neural network is x (i.e., $f_0 = x$) and every layer is represented with $$f_i(x_{i-1}) = \sigma_i(A_{i-1}x_{i-1}+ b_i-1)$$ Here we have A the weights, x the previous output and b the bias. To train the model we require all the gradients of a loss function $\mathcal{L}$. for $A_i , b_i$ for i = 1, . . . , z such that the loss function $\mathcal{L}$ is minimized. This also requires us to compute the gradient of $\mathcal{L}$ with respect to the inputs of each layer. 

> Note that $\theta$ = {$A_0, b_0, . . . , A_{z−1}, b_{z−1}$}

To obtain the gradients for the parameters θ, we require the partial derivatives of L for the parameters $\theta_i$ = {$A_i , b_i$} for each layer i. 

![[Pasted image 20230611041546.png]]

The blue terms are the partial derivaties of the output of a layer with respect to its inputs. The red terms are the partial derivatives of the output of a layer with respect to its parameters.

It's worth noting that modern deep learning frameworks and libraries handle the computation of gradients automatically, allowing you to focus on designing and training the neural network while the underlying framework takes care of the gradient calculations through automatic differentiation.

![[Pasted image 20230611035606.png]]
![[Pasted image 20230611041635.png]]

