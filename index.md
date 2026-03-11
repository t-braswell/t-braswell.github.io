---
title: Homepage
permalink: /
layout: default
---

# Welcome!
I am a second year student MSc. student at in Applied Mathematics at San Diego State University. I split my focus between developing an understanding of quantitative methods for industry and research, and communicating core concepts more clearly as a math educator.

This site functions as a summary of my teaching experience, and research results and interests. Future usage for the site may include blogging and student resources.


![Perceptron](/downloads/perceptron_693.png) 
```
import numpy as np
import matplotlib.pyplot as plt 

# Let's make some data in R^3 for the Perceptron to classify.  
def hyperplane(x):
    return 1. + np.sum(np.ones(3) * x) # let's keep this simple
    
# Generate labeled data on either side of a 3D plane.
def label_maker(Npts, margin):
    fig = plt.figure()
    ax = fig.add_subplot(projection='3d')

    points_above = []
    labels_plus = []    
    points_below = []
    labels_minus = []

    for jj in range(Npts):
        tst_point = 10.* np.random.randn(3)
        find = True
        while find:
            if hyperplane(tst_point) >= margin:
                points_above.append(tst_point)
                labels_plus.append(1)
                find = False
                ax.scatter(tst_point[0], tst_point[1], tst_point[2], c='k')
            elif hyperplane(tst_point) <= -margin:
                points_below.append(tst_point)
                labels_minus.append(-1)
                find = False
                ax.scatter(tst_point[0], tst_point[1], tst_point[2], c='r')
            else:
                tst_point = 10.* np.random.randn(3)

    xvals = np.linspace(-50., 50., int(1e1)+1)
    yvals = np.linspace(-50., 50., int(1e1)+1)
    xx, yy = np.meshgrid(xvals, yvals)
    zvals = -1 - xx - yy
    ax.plot_surface(xx, yy, zvals, linewidth=0, alpha=.25)
    return points_above, labels_plus, points_below, labels_minus
	
	points_above, labels_plus, points_below, labels_minus = label_maker(1000, .01)
```
