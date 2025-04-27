# QuantumClustering
A method to perform clusterization of data points based on Quantum Mechanics principles

Before starting, I have to say that I have not done any bibliography before, so it might be possible that this idea already exists.

Inspired by the measurement problem in Quantum Mechanics and the Heisenberg uncertainity principle between position and momenta, the aim of this algorithm is to represent data not as a fixed point in a $N-$dimensional vector space, but rather to be a function that has some parametrically spatial dependence. An electron, in QM is never seen as a fixed particle, but rather a probability cloud. Here we employ the same philosophy: instead of thinking about a data point as a fixed-well defined point in a vector space, we rather consider some wave function on a Hilbert space, that parametrically depends on its observed position, that is, its coordinates. This approach is fundamented in the intrinsic error of any measure, that is, the true value will lie in a neighbourhood or probability density near the oberved value.

In this specific notebook, we will represent the data employing the so called Gaussian Type 1s-Orbital centered at the measure point, where most of analytic formulae exists. We thus employ the overlap matrix $S$ to compute the nearest-neighbours graphs, in order to find similarities between data. From that, we construct a graph, hopefully to be a $k-$partite graph, where can then categorize data.

The main drawback of this technique is that we approximate each point as a gaussian wave function, thus being quite limitated. The separation of the resulting graph only works for two clusters, so it is quite limited for the moment.

## Mathematical interpretation

Aside from the Quantum Mechanics interpretation that we can make, the mathematical fundaments are well stablished into the Data Science community.

To begin with, we consider that data lives in an Euclidian Vector Space $(\Omega, \langle \cdot \rangle_E)$, where $\langle \cdot \rangle_E$ is the standard Euclidian inner product, that allows us to define distances $\|u-v\|_E \ \forall u,v \in \Omega$.

From that, we send our data to the new Hilber Space of gaussian functions centered at the data points $(\Delta, \langle \cdot \rangle_H)$ defined as:
$$
\begin{align}
  \Delta &:= \{\phi(z) = e^{-\alpha \|x-z\|_E^2}\ |\ \forall x \in \Omega\} \\
  \langle \phi, \varphi \rangle_H &= \int_{-\infty}^{\infty} \phi(z) \varphi(z) dz
\end{align}
$$

Once we have transformed our initial Euclidian data into our Hilbert data space, we can compute similarity between data points. We could employ the normal distance $\|\phi-\varphi\|_H = \sqrt{\langle \phi-\varphi, \phi-\varphi\rangle_H}$, but we can rapidly see that this quantity is proportonial to $\langle \phi,\varphi \rangle$, and sucht that this quantity is in the segment $[0,1]$ after proper normalization, so we employ the inner product as a measure of similarity.

Obviously, one drawback of this technique is the symmetry of the Hilbert space function, where in some terms, the boundaries might not be respected.

After that, we construct the graph imposing a thershold and then we perform a connected-component labeling, to finally obtain the clusters.
