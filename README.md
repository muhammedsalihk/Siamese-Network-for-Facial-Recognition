# Siamese Network for Facial Recognition

## Introduction
Facial recognition is different from other image classification problems owing to the fact that we can’t always have a lot of training images for each person in the database. The recognition will have to happen based on a very few (usually one) images of the person added to the database. Such a problem is known as one-shot learning.

One-shot learning is usually facilitated by training a simaese network using triplet loss. Such a network creates an embedding for the image of a face inputted into it wherein the images of the same person’s face results in closer embeddings when compared to images of different faces.

The training is done using triplets of images known as anchor, positive and negative images. The anchor and positive are images of the same person while the negative is an image of a different person. More details are explained in the methodology section.

## Methodology
A basic overview of the network and triplet loss is provided below

![Triplet Loss](https://github.com/muhammedsalihk/Siamese-Network-for-Facial-Recognition/blob/master/Images/Triplet%20Loss.png)

One important thing to note is that while selecting the training samples, we have to choose hard or semi hard triplets (i.e. where the loss is greater than 0). Otherwise, the sample doesn’t contribute to the learning process. In this project, a script has been written to automatically discard any easy samples while choosing the training set at various stages of training.

The steps followed in this project are summarised below.

1. A CNN was created with randomly initalised weights using Keras.
2. A small training set of 100 triplets was sampled and the network was trained for 2-3 epochs. Note that initially most of the triplets are hard or semi hard for the network as the weights are randomly initialised using Xavier initialisation.
3. Then a larger set of semi hard and hard triplets was sampled and the network was trained for a larger number of epochs.
4. Step 3 is repeated until very few (1 in 100 randomly selected triplets) are hard or semi hard for the network.

## Training Set and Implementation
The triplets were sampled from a set of 100 celebrity face images obtained from pinterest (10 images per person) using a python script that checks for duplicates and also against choosing easy to train samples.

![Network](https://github.com/muhammedsalihk/Siamese-Network-for-Facial-Recognition/blob/master/Images/CNN.png)

Note - Using an L2 norm layer at the end for the embedding was very useful in the training process as the embeddings could be limited to the surface of an hyperspehere of radius one from the origin rather than being spread out across the n-dimensional space (where n is the number of units in the output layer). The use of normalisation helped in making the learning much faster.
