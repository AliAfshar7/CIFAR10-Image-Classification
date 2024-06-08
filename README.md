# CIFAR10-Image-Classification
This project aims to develop a neural network with a specific architecture to predict image content.
# Basic Architecture
The architecture consists of a series of blocks B1, B2, ..., Bk, that are followed by an output block O, as shown in the following figure. The details of these blocks will be explained in the following sections.

![image](https://github.com/AliAfshar7/CIFAR10-Image-Classification/assets/147258856/c7f3e42e-091c-437b-b8ee-a4140f5f8da9)

## Intermediate block
An intermediate block receives an image x and outputs an image x′. Each block has L independent convolutional layers. Each convolutional layer Cl in a block receives the input image x and outputs an image Cl(x). Each of these images is combined into the single output image x′, which is given by

![image](https://github.com/AliAfshar7/CIFAR10-Image-Classification/assets/147258856/774cf3d3-b469-4ee3-b944-3817a392587a)

where a = [a1, a2, . . . , aL]T is a vector that is also computed by the block. Note that each convolutional layer in a block receives the same input image x (and not the output of another convolutional layer within the block).
Suppose that the input image x has c channels. In order to compute the vector a, the average value of each channel of x is computed and stored into a c-dimensional vector m. The vector m is the input to a fully connected layer that outputs the vector a. Note that this fully connected layer should have as many units as there are convolutional layers in the block. Each block in the basic architecture may have a different number of convolutional layers, and each convolutional layer may have different hyperparameters (within or across blocks). However, every convolutional layer within a block should output an image with the same shape.
## Output block
The output block receives an image x (output of the last intermediate block) and outputs a logits vector o. Suppose that the input image x has c channels. In order to compute the vector o, the average value of each channel of x is computed and stored into a c-dimensional vector m. The vector m is the input to a sequence of zero or more fully connected layer(s) that output the vector o.
# Implemented architecture
## Intermediate blocks
The model that was employed in this project has 3 intermediate blocks and each block is consisted of 4 parallel Convolutional layers. In all the layers the stride is equal to 1. The set up of each block is as followed in the table below.

| Block | Num. Layers | Kernel 1 | Padding 1 | Kernel 2 | Padding 2 | Kernel 3 | Padding 3 | Kernel 4 | Padding 4 | In channels | Out channels |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 4 | 1 | 1 | 3 | 2 | 5 | 3 | 7 | 4 | 3 | 30 |
| 2 | 4 | 1 | 1 | 3 | 2 | 5 | 3 | 7 | 4 | 30 | 90 |
| 3 | 4 | 1 | 1 | 3 | 2 | 5 | 3 | 7 | 4 | 90 | 180 |

## Macro block
The class defined for the output block is called “MacroBlock”. In this class, the class defined for creating intermediate blocks is used to create the intermediate blocks. In this block, output of each intermediate block will be an input of the next.
After going through the intermediate blocks, the average results of each channel will be processed by a fully connected layer. The output of this layer should have the same number of channels as the classes in our dataset, which in this case is 10.
# Final result
The best accuracy achieved by this model is **97.189%** for training dataset and for this training accuracy the test accuracy is **80.72%**. The figures for cross entropy loss for each training batch and train and test accuracy for epochs are also shown respectively.

![image](https://github.com/AliAfshar7/CIFAR10-Image-Classification/assets/147258856/68228de7-02b6-4291-80e9-375eea771991)

![image](https://github.com/AliAfshar7/CIFAR10-Image-Classification/assets/147258856/fd0ace32-c494-424c-a8f0-18a00cd8f9a3)








