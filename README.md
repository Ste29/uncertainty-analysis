# Uncertainty analysis - Bayesian Neural Networks

## Table of contents
* [General-info](#general-info)
* [Theorical background](#theorical-background)
* [Results](#Results)

## General info
To quickly run the notebooks it is recomended to open them in google colab and then associate your google drive account, the notebooks automatically creates two folders, one for tensorboard savings, the other one for weights.

## Theorical background
CNN needs a huge amount of data otherwise it tends to overfit and to make overconfident predictions, for these reasons BNN were introduced, also the great advantage of BNN is the possibility to measure the uncertainty in the prediction. The idea behind Bayesian modeling is to consider all possible values for the parameters of a model when making predictions. In order to do so, the parameters are treated as random variables whose distribution is such that the most likely values are also the most probable ones.
The network, starting from a prior distritibution of the model parameters, learns the posterior distribution through Bayers theorem applied on training data.

Predictions are made by weighting the predictions made with every parameter setting using the corresponding probability, that is the posterior probability. Since we do not know the posterior probability, we use Monte Carlo samples from the approximating proposed distribution.
The probability distributions over weights are assumed as Gaussians, therefore they have mean μ and a variance σ². The mean μ is the most probable value we sample for the weight, whereas the variance can be seen as a measure of uncertainty. To be more exact, the variance is the sum of two kind of uncertainties: 
-	ALEATORIC UNCERTAINTY: a measure of the goodness of the dataset. In particular this is the uncertainty about the observation y caused by a noisy dataset {x,y}.
-	EPISTEMIC UNCERTAINTY: a measure of the goodness of the model. That means that epistemic uncertainty captures our ignorance about the models most suitable to explain our data.

BNNs are trained using Bayed-by-backprop.

## Results

