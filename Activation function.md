
At certain points in the neural network architecture of say a [[Multilayer Perceptron]] or [[Convolutional Neural Networks]] etc you want to include activation functions. Activation functions are non linear functions which have a derivative. Easy derivative is nice.  

![[Pasted image 20230610163823.png]]

We need activation function because otherwise the model you learn would just be a linear operation. With a linear operation you can only learn linear functions. With activation functions you allow non linear things to be calculated.  The lack of activation functions caused first AI winter in the 60ies because without this the network can't even find the xor function.  

Activation functions play a crucial role in neural networks for introducing non-linearities and enabling the network to learn complex relationships and patterns in the data. 

Activation functions can shape the decision boundaries learned by the neural network. By applying non-linear transformations, activation functions can map the input data to higher-dimensional spaces, allowing the network to learn more intricate decision boundaries.

Certain activation functions, such as the Rectified Linear Unit (ReLU), inherently provide regularization effects by sparsely activating neurons.

Activation functions can also contribute to normalizing the activations within the network, promoting stable training and preventing values from becoming too large or too small.



Ok, so they take the output of a layer and because its a non linear the previous layer basically has to deal with that. When the output of a layer in a neural network passes through a non-linear activation function, it introduces non-linearity to the network's computations. This non-linearity affects the information flow and interactions between the layers.

Each layer in a neural network performs a linear transformation on its input, which includes multiplying the input by weights and adding biases. Without activation functions, the network would simply be a series of linear operations, and the composition of multiple linear operations would still result in a linear function.