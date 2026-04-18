# CNN and Image Classification

When we do learn image, the larger image may lead the more parameters and more computation. But we don't actually need to looks at the entire image and we want the incoming weights to focus on local patterns of input image. We would like to use high-level operation **convolution** to extract features from the image.

Denote $*$ as convolution operation, we have:

- $a * b = b * a$ (commutative)
- $a * (\lambda_1b + \lambda_2c) = \lambda_1(a * b) + \lambda_2(a * c)$ (linearity)

The thing we would convolve by is call a **kernel** or **filter**. We can use kernel to do blurring, sharpening, edge detection, etc.

## Convolution Layer

That is, we would like to add a convolution layer to our neural network. 

Usually, when we have $n \times n$ input image and $k\times k$ kernel, we would have $(n-k+1) \times (n-k+1)$ output image. If we have $l$ padding, we would have $(n-k+2l)+1 \times (n-k+2l)+1$ output image. If we have additional stride $s$, we would have $(n-k+2l)/s+1 \times (n-k+2l)/s+1$ output image. (i.e. $\hat W \times \hat H$)

- padding: add $l$ pixels of zeros around the input image.
- stride: the number of pixels between adjacent receptive fields in the horizontal and vertical directions.

Ways to measure the size of a network:

- Number of units. (activations in memory during training)
- Number of weights. (weights in memory during training, overfitting might lead by parameters)
- Numer of connections. (approximately 3 add-multiply operations per connection, 1 for forward pass, 2 for backpropagation)
- a fully connected layer with $M$ inputs units and $N$ output units has $M \times N$ weights and $M \times N$ connections.

More comparison, given the same input and output size ($\hat W\hat H i$):

- $I$ output maps
- $J$ input maps
- $K$ kernel size
- $H$ height of input
- etc...

| Layer Type | Number of Weights | Number of Connections |
|------------|-------------------|-----------------------|
| Fully Connected | $W\hat W H \hat H IJ + \hat W \hat H I$ | $W\hat W H \hat H IJ + \hat W \hat H I$ |
| Convolution | $K^2IJ + I$ | $\hat W\hat H K^2IJ + \hat W\hat H I$ |

The add item is the bias term.

## Pooling Layer

These layers reduce the size of the representation and build in invariance to small transformations. Most commonly, we use max pooling which computes the maximum value of the units in a pooling group: $y_i = \max_{j \in P} z_j$. where $P$ is the pooling group.

For a $n \times n$ input image with $k \times k$ kernel and $s$ stride, we would have $(n-k)/s+1 \times (n-k)/s+1$ output image.

## Convolutional Neural Network

We can combine convolution layer and pooling layer to form a convolutional neural network.

1. The convolution layer with sets of kernels produce a set of feature maps (each obtained by convolving the input with a different kernel).
2. Beyond the pooling layer, we would always like to have a linear rectification nonlinearity (ReLU) to introduce nonlinearity to the network.
3. Then we apply on the pooling layer so that higher-layer filters can cover a larger region of inputs than equal-sized filters in lower layers. 

Moveover:

- convolution layers are equivariant where the inputs and outputs are translated by the same amount.
- we would like to make nn predictions to be invariant, that is, translate inputs should not change the prediction.
- pooling layers provide invariant to small translation.

## Object recognition

Object recognition is the task of identifying objects in images. It's closely related to object detection, which is the task of locating objects in images. 

Some useful datasets sources MNIST, CIFAR-10, ImageNet, COCO, etc.