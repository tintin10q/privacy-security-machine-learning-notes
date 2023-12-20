CNNs represent a type of neural network first designed for 2-dimensional convolutions.

The idea is that you don't do multiplications over the entire input vector but separate multiplications for parts of the input vectors. You do this by dot multiplying a part of the input matrix/vector with a kernel (just another learned matrix) which then gives you the value of 1 of the output layer. You then basically slide this kernel over the image. See the picture. 

They are primarily used for image classification, but in the last years, they have proven to be powerful classifiers in other domains. 

From the operational perspective, CNNs are similar to ordinary neural networks: they consist of a number of layers where each layer is made up of neurons CNNs use three main types of layers: 

- **Convolutional layers** this is with multiplication with the kernel, see the image. 
- **Pooling layers**, here the kernel is not matrix multiplication but more like sum or max
- **Fully-connected layers**, same as before with [[Multilayer Perceptron]]

The idea of the convolution layer is to, during the forward computation phase, convoluted the input data with some filters. The output of the convolution is commonly called a feature map. It shows where the features detected by the filter can be found on the input data.

![[Pasted image 20230610163614.png]]

