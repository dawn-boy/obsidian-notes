# Classical physics
the term classical physics refers to physics before the advent of Quantum mechanics.
Classical physics includes,
- Newton's equations for the motion of particles,
- Maxwell-Faraday theory of electromagnetic fields,
- Einstein's general theory of relativity.
Classical mechanics is more than justa set of theories of specific phenomena, It's a set of principles and rules, an underlying logic that slowly emerges and let's itself be known to those who are curious enough to want to look at the bigger picture.
***
## 1. The nature of classical physics
The job of classical mechanics is to predict the future.
> We may regard the present state of the universe as the effect of its past and cause of the its future. An intellect which at a certain moment would know all forces that set nature in motion, and all positions of all items of which nature is composed, if this intellect were also vast enough to submit these data to analysis, it would embrace in a single formula the movements of the greatest bodies of the universe and those of the tiniest atom; for such an intellect nothing would be uncertain and the future just like the past would be present before its eyes.
\- Pierre-Simon Laplace, 18<sup>th</sup> century physicist.
### Deterministic system
In classical physics, if you know everything about a system at some instant of time and you also know the equations the govern how the system changes, they you can predict its future. This is what we mean when we say the classical laws of physics are **deterministic**.
### Reversible system
If the same thing can be said but with the past and future reversed, then the same equations tell you everything about the past. Such a system is called **reversible**.
### Closed system
A collection of objects - particles, fields, waves or whatever - is called a system. An isolated system that behaves as if nothing else exists is a **closed system**.
#### state-space
The collection of all states occupied by a system. It's not an ordinary space, its a mathematical set whose elements label the possible states of the system.
### Continuous and Stroboscopic systems
In classical mechanics we assume that systems evolve smoothly, without any jumps or interruptions. Such behavior is said to be continuous. Some systems cannot evolve continuously rather they evolve in discrete jumps, these are said to be a stroboscopic system.
### Dynamic system
A system that changes with time. A dynamical law is a rule that tells us the next state given the current state.

this law states that there is no evolution,
$$ \sigma(n+1) = \sigma(n)$$
this law implies that the states flip each time,
$$\sigma(n+1) = -\sigma(n)$$
### The minus-one law
The conservation of information is simply a rule that every state has one arrow in and one arrow out. It ensure that you never lost track of where you started, where you were, or where you're going.

>[!info] The limits of precision
>	Laplace may have been overly optimistic about how predictable the world is. This world is constantly changing and the ability to know the initial conditions with almost perfect precision (upto an infinite decimal places) is quite hard. Any slight changes at the billionth billionth decimal place would have compounding effects in the final result which might be drastically different than the original outcome. This is chaos.
### coordinates
To describe points quantitatively, we need to have a coordinate system.
- Choose an origin (keep it static, do not move it.)
- Choose three perpendicular axes.
Now, this is a Cartesian coordinate system. Any point within this system can be represent by a triplet (x,y,z).
To study motion, we also need to keep track of time. So,
- Choose an origin for time (keep it static, do not change it.)
- fix a direction, generally positive times are to the future of the origin and negative times are to the past.
- finally, pick up a unit. Seconds are customary.
So, these four coordinates (x,y,z,t) defines a reference frame.
### trigonometry
$$sin\theta = \frac{a}{c}$$
$$cos\theta = \frac{b}{c}$$
$$tan\theta = \frac{a}{b} = \frac{sin\theta}{cos\theta}$$
### vector
vector is an object that has both length and direction in space.
They are represented as $\vec{r}$, and it's magnitude is represented as $|\vec{r}|$.

Vectors can be represented in their component form. We begin with defining three unit vectors the lie along these axes with a unit length. The unit vectors along that lie along the coordinate axes are called basis vectors.
The three basis vectors for Cartesian coordinates are $\hat{i},\hat{j},\hat{k}$, where the hat tells us that we're dealing with unit vectors. Now, this terminology becomes useful when we write a vector in terms of them,
$$\vec{V} = V_x\ \hat{i}+ V_y\ \hat{j}+V_z\ \hat{k}$$
The quantities $V_x,V_y,V_z$ are numerical coefficients that are needed to add up the basis vectors to give $\vec{V}$. They're also called the components of $\vec{V}$, and this equation can be called as a linear combination of basis vectors.

The magnitude of the vector can be calculated with the Pythagorean theorem.
$$|\vec{V}| = \sqrt{V_x^2+V_y^2+V_z^2}$$
#### product of two vectors
##### dot product
$$\vec{A} \cdot \vec{B} = |\vec{A}|\ |\vec{B}|\ cos\theta$$
The component of $\vec{A}$ along $\vec{B}$ multiplied with the component of $\vec{B}$ along $\vec{B}$, which is $\vec{B}$'s magnitude.
- $\theta > 90\textdegree$ -> product is negative,
- $\theta = 90\textdegree$ -> product is zero (vectors are orthogonal),
- $\theta > 0\textdegree$ -> product is one.
***
## 2. Motion
Most of classical mechanics deals with things that change smoothly. To cope with this, we use the mathematics of calculus. 
Calculus is about limits, suppose we have some series of numbers that gets closer and closer to a value L,
$$0.9, 0.99,0.999,0.9999, 0.99999, ....$$
the limit of this sequence is 1. Mathematically, we write this as,
$$\lim_{i\to\infty}l_i = L$$
in words, L is the limit of l<sub>i</sub> as i goes to infinity.
