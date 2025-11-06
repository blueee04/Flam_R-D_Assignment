# Barshan Mondal

## FLAM assessment

### Research

07 November 2025

## My Solution

Okay i’ll break down the problem, so we have been given two parametric equations which are as follows, i’ll paste the screenshots here.

We have been asked to estimate the unknowns theta,M,X from the given parametric curve, we have also been provided with the (x,y) data. From the looks of it, this looks like a curve fitting problem.

Let’s start with the solving and overview then

We have been given the ranges of the unknowns so that we don’t go out of bound.

We know that the first point corresponds to t=6 and the last to t=60 and the points are linearly spaced among each other.

So according to me this looks like a problem to find the best parameters and finetune the equation….so for a given guess for all the three parameters we are going to compute the model and then compare it with our data to find the error….according to that we can calculate the error over all the data points and edit out weights or parameters

Let me write down a outline or pseudocode:

- We will read the data from the csv into arrays and separate the values of t such that the last point will get 60
- Define the equations
- Calculate the error - the error we will be using will be the sum over all the points
- Now since we have variable bounds we will need to optimize the weights as well
- And finally we will have the best fit line that will match our csv to the max

I’ll try this out in a google colab notebook

Okay so one more thing i tried out two optimization techniques:

- The first thing that came up to my mind - Normal Manual Gradient Descent Updating the params with each epoch which didnot give me a close output
- Then i did i bit of research about what optimization is best for this type of problems and it turns out there is one called the minimize function in the scipy library which adjusts the params according to the Sum of the squared errors
- Bonus out of curiosity i tried out another optimization method - curve_fit(added in colab)

So the final weights that i have received before the error converges are:

Gradient Descent : Estimated: theta=50.00 deg, M=-0.05000, X=0.00

Minimize and Curve_fit : 	Estimated theta: 29.58 degrees

Estimated M: -0.05000

Estimated X: 55.01

Final Errors For both :

Gradient Descent - Iteration 900: error=4.91e+06, params=[0.e+00 5.e-02 1.e+02]

Minimize and curve_fit - 7.72e+05

Finally Both The Equations Are as Follows in latex form :

Gradient Descent :

$$
\\left(t*\\cos(50)-e^{-0.05\\left|t\\right|}\\cdot\\sin(0.3t)\\sin(50)\\ +0,\\ 42+t\\cdot\\sin\\left(50\\right)+e^{-0.05\\left|t\\right|}\\cdot\\sin\\left(0.3t\\right)\\cos\\left(50\\right)\\right)
$$

Minimize and Loss_curve :

$$
\\left(t*\\cos(29.58)-e^{-0.05\\left|t\\right|}\\cdot\\sin(0.3t)\\sin(29.58)\\ +55.01,\\ 42+t\\cdot\\sin\\left(29.58\\right)+e^{-0.05\\left|t\\right|}\\cdot\\sin\\left(0.3t\\right)\\cos\\left(29.58\\right)\\right)
$$

<iframe src="https://www.desmos.com/calculator/ksg0xydj8f?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

The Thick purple shows the given Data points

The Red curve shows the optimization by gradient descent

The thin purple one shows the optimization by minimize or loss_curve
