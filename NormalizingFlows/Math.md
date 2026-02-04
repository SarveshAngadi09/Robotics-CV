**The Math for Normalizing Flows**

**Change of Variables function** - **P(x) dx = P(z) dz**

It is not complicated if you think of it as that the dough example where we are reshaping the dough(probablity distribution here). If you flatten the dough, let us say it has uniform probablity. Now, make it like a heap, the probablity in the middle is more than on the sides. So P(x) is one probablity distribution and P(z) is another. 

{ if above thing still doesn't make sense:

P(x) = probablity density in a unit area in X plane (how many points are there in a unit area)
P(y) = Probability density in a unit area in Y plane (how many points are there in a unit area)

Total probability is summing all the probabilities over the total area. P(x) * total area. (integral of probablity density p(x) over dx)

Lets say we flatten the dough into a thin layer in X plane, which makes area of 1 (1.1 cm2 area), it is called uniform density. So  P(x) = 1
When we move this dough to Y plane, we stretch it so that it occupies twice the area, making it 2 (2.2 cm2 area). So P(y) = 1/2. why halved? because the points have moved futher away or fewer points per unit area, so sampling a unit area gives you only half samples. (Note: the total samples remain same, i.e the total probablity is 1, just the density is changed)
What essential happened? y = 2x. A small region in x, dx, has been strecthed to dy = 2. dx

Now lets find probablity in a small region. Px(x) dx - Probablity density has reduced by half because of strecthing p(y) = p(x)/2
probability in small region P(x) dx = p(x)/2 . 2. dx = P(y) dy .

Total probability stays the same. When you scale, shear, twist, or rotate the distribution, the density changes locally, but the total probability is conserved, you’re just redistributing the points.

}

In Normalizing flows we are doing the above thing and trying to redistribute a complex probablity distribution into a simpler once. (dough in some weird shape to rounded dough)
x - Complex distribution (let us say, image distribution)
z - Simple distribution (gaussian distribution or any simple distribution)

**Aim: We have to model a function/set-of-functions which will change the complex distribution to simple distribution.**

z = f(x) ( scale, shear, twist, or rotate to transform to someother distribution)

This function should be invertible, i.e, the inverse of this should give us x.
x = f-1(z)

From change of variables formula,

p(z)dz = p(x)dx

p(x) = p(z) dz/dx

We want to have more samples in the regions where the p(z) is more. Which basically means take points or samples in x distribution and map them closest possible to the region where we want more samples in z space.(From flat dough, we move more samples towards the center to make it heaped dough). Maximizing 
𝑝(𝑥) means: make your model assign high probability to the real data.

So, Maximize P(x)! (Problem: when we have a huge area, the net probability is 1 but the probablity density(prob per unit area) is very very small. For a lot of points when we want to maximize, we do Product(all p(x)) or p(x1).p(x2).....p(xn). This probability will be very small(0.1 times 0.1 = 0.01).
So to avoid this we apply log to the p(x). { !Find why log is best! }

**Maximize Log-likelihood**
Sum-over-n(log(p(x))) = sum-over-n(log(p(z))) + log(dz/dx)

Okay! Now it has messed up enough! Why do we even need loss function?

But wait, did we ask - who is giving us the invertible function to map from x to z? Well, Neural networks do!!! but how do they know what function is the best. (does z = 2x works? f(x) = 2x work?) how do you know it is 2? Here is where it uses the loss function which is log-likelihood function but since we are so good at minimizing things(gradient descent), we just try to minimize negative log likelihood. (**-** Sum-over-n(log(pz))).

**Neural networks try to build a function of n-parameters to convert x to z such that the log-prob(z) is maximized.**

I had an INTERESTING QUESTION:

We asked neural networks to move the most of the samples towards center p(z) (in case of gaussian), since you told "We want to have more samples in the regions where the p(z) is more.", what if neural network moves all samples to center!!!??? (high density dough at the center instead of a heap)
That is where log(dz/dx), this term saves us. It says, if you put everything at the center, then dz/dx value will be very small. In other words, if we make dx into a very small dz, high density point in the center, then (very very small dz)/dx ~ 0. The log(dz/dx) penalizes the network from cheating by mapping all points to a high density peak. 


**Yeah! That is basics of the math of NF. What we should learn ahead is: what happens when we map from n-dim (x) to n-dim (z)? how will dz/dx be? This will be introduction to Jacobian. It will be covered in basics of Generative models where I will try to explain the basic math needed to understand the concepts concretely)**

