# sphere-gen
Taken from here: 
https://www.johndcook.com/blog/2025/05/06/random-points-on-a-sphere/

I recently ran across a simple way to generate random points uniformly distributed on a sphere: 

Generate random points in a cube until you get one inside the sphere, then push it to the surface of the sphere by normalizing it.
In more detail, to generate random points on the unit sphere, generate triples

**(u1, u2, u3)**

of independent random values uniformly generated on [−1, 1] and compute the sum of their squares

**S² = u1² + u2² + u3²**

If **S² > 1** then reject the sample and try again. Otherwise return

**(u1/S, u2/S, u3/S)**.

There are a couple of things I like about this approach. First, it’s intuitively plausible that it works. Second, it has minimal dependencies. You could code it up quickly in a new environment, say in an embedded system, though you do need a square root function.

### Comparison with other methods
It’s not the most common approach. The most common approach to generate points on a sphere in n dimensions is to generate n independent values from a standard normal distribution, then normalize. The advantage of this approach is that it generalizes efficiently to any number of dimensions.

It’s not obvious that the common approach works, unless you’ve studied a far amount of probability, and it raises the question of how to generate samples from normal random variable. The usual method, the Box-Muller algorithm, requires a logarithm and a sine in addition to a square root.

The method starting with points in a cube is more efficient (when n = 3, though not for large n) than the standard approach. About half the samples that you generate from the cube will be thrown out, so on average you’ll need to generate six values from [−1, 1] to generate one point on the sphere. It’s not the most efficient approach—Marsaglia gives a faster algorithm in the paper cited above—but it’s good enough.