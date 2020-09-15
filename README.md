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

The architecture of the network was composed of an input layer, 2 convolutional bayesian layers alternating with 2 max pooling layers, then a fully connected bayesian layer and last the output layer.

On the test set the network achieved 98.1% accuracy, then selecting 0.15 as threshold every prediction where the network wasn't sure was discarded. In particular, 2.5% of the predictions were discarded, achieving 99.86% accuracy on the remaining images. When the net was sure about the prediction, the classification was almost always correct.

![res](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/results.png)

These images were wrongly predicted and discarded.

![cin_incerto](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/five_wrong_unc.png) ![set_incerto](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/seven_wrong_unc.png)

However, in some cases the net predicted the right outcome, but discarded the images due to high uncertainty

![sei_giusto](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/six_right_unc.png) ![cin_giusto](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/five_right_unc.png)

And lastly, some images were wrongly predicted, but with low uncertainty

![nov_sbagliato](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/nine_wrong.png) ![cin_sbagliato](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/five_wrong.png)

The network was then tested on a completely different dataset: emnist, wich is composed of letters instead of numbers. A classic CNN would have predicted the results according the knowledge got from mnist dataset and therefore the results would have been bad. Indeed, [CNN](https://github.com/Ste29/Uncertainty-analysis/blob/master/scripts/Simple%20CNN%20MNIST.ipynb) achieve 99% accuracy on mnist and 1.9% on emnist. 
It would have been useful if a classifier could recognize when it should not take a decision, i.e. different kind of data from its training set, for this reason the BNN was tested also on emnist.

![emn](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/results_emnits.png)

Many of the predicted cases were images similar to those of the mnist like the following ones:

![d](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/D.png) ![s](https://github.com/Ste29/Uncertainty-analysis/blob/master/img/S.png)
