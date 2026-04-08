---
author: Tara
title: Neural Networks, Explained at Various Levels of Simplicity
---

# Table of Contents

1.  [Neural Networks, Explained at Various Levels of Simplicity](#org7aa478f)
    1.  [Simplest:](#org701d566)
    2.  [Nuancing:](#orgb2387f4)
    3.  [Adding Calculus:](#org1b4c917)
    4.  [Implementation-Specific Details](#org4d137f5)
    5.  [An Employable Understanding:](#org11626c6)


<a id="org7aa478f"></a>

# Neural Networks, Explained at Various Levels of Simplicity

I have always found trying to understand Machine Learning to be difficult, due to
an inability to appreciate the scale of everything. A calculus 3 professor may discuss
neurons in the context of chain rule in order to demonstrate the topic's relevancy,
only for any calc 3 application to be too simple to see how a machine learns, or too
complex for students to calculate by hand. Abstracting away machine learning as "just
some statistical regressions and a massive amount of linear algebra" does not give a
3rd year math student any insight into implementation. The jump between discussing
gradients and massive, profitable language models has gotten so large that I often end up
thinking that theres something "magic" about doing several billion man-hours of linear
algebra. Here, I want to try and explain the concept in various levels of simplicity,
so we can see where the details might get lost.


<a id="org701d566"></a>

## Simplest:

-   Computer guesses the right answers, checks answers, learns to guess better.
-   When it is done guessing, that computer can guess things it hasnt seen before.

Makes sense to a ten year old; roughly true, but no idea of implementation.


<a id="orgb2387f4"></a>

## Nuancing:

-   Performance on a classification task is evaluated as a function (called our "Loss" function).
-   An additional function (called a "neural network") is created to answer a classification problem, with some
    parameter values of some numbers that can be changed.
-   Twiddle with parameters of until our performance score is good.

Implementation hinted at; theres some sort of magic values that a computer "guesses"
at. The computer does a lot of guessing over many rounds, chewing up and recomputing said
performance function. How the computer twiddles with parameters is not random, as this might imply, but this does capture
the ethos perfectly. What this view *does* show is that the functions chosen for loss and
classification can be arbitrary, but choice may affect our performance. "too simple"
of a classification function may cause problems, but we also have to think about how we score
correctness.


<a id="org1b4c917"></a>

## Adding Calculus:

-   A function with unknown numerical parameters, defined by a "neural network" of related
    subfunctions with parameters, is built. this function will take in some vector
    of information, and transform it into a guess of most likely value.
-   A *continuous* Loss function is implemented based on comparing the values from our
    neural net vs what our data is labled with. We look at the overall loss in all
    datapoints, and optimize our neural network's parameters until this reaches a minimum on our dataset/

Now we're cooking. We aren't just guessing at our numbers, Calc 1 says we attempt to set
the derivative of our Loss composed with our classifier function equal to zero, calc 3 implies that we would 
need each partial to be zero for a true solution. This is comprehensible to a calc
3 student trying to see why this matters for AI, but a few extra details are needed.


<a id="org4d137f5"></a>

## Implementation-Specific Details

-   A function/neural network, composed of several (typically linear) subfunctions with unknown parameters composed on each other
    and ran into a single nonlinear function, allowing for continuous values of the classifier.
    The value of the classifier/output is rounded, threshholded, or somehow reduced to a discrete classifier.
    The number of secret functions and parameters is, at minimum, in the hundreds, but likely in the millions.
-   In order to "train" the network, we will take a subsample of our data and optimize our
    parameters to minimize loss on the subsample. We will repeat this on a variety of subsamples,
    taking the last models parameters as a starting point for optimization. With so
    many variables, this optimization will be done with numerical techniques rather than an analytical solution;
    this will reduce accuracy but prevent overfitting and allow for computational feasibility.

Stats matters and we will not have perfect values. our classifier being continuous before we
truncate does say that we might have innacurate guesses, but our system is likely overdetermined. With a large
enough dataset. Some datapoints might be extremely similar but have different classifications,
and this an effect of using real data.


<a id="org11626c6"></a>

## An Employable Understanding:

-   Build a loss function, build a network, minimize loss. Play with network design,
    loss functions, and numerical optimization algorithms until one build works out better than others.
-   Leverage the nonlinearity networks final function to assume that changing individual
    parameters might have have hard to predict effects. Accept this and ignore actual values.
-   Most importantly, **worry about data**: make sure it is formatted, cleaned, and stored in some useful way.

This is not an exercise in frequentist statistics; we dont care if our model is "true" because neural network design is
somewhat arbitary. While some designs have been generally more useful, this is based on empirical experience in industry
rather than theory. We do not care about variance of any particular model parameter; there are too many to even consider.
We do not even care about the explicit value of our Loss function; we only need our testing accuracy to be high enough,
before we (without statistical proof) assume it will be accurate on new data. By black-boxing so many details away, our focus
is building something "good enough" to work. The problem we are trying to answer matters, and very often, even just acquiring or loading the training
dataset into memory is more technically challenging.

Up next, we will take some python code for a simple neural network and break down each step. 

