# Implementation notes

These notes describe the checked-in notebooks. They do not change the implementations or claim a fresh execution of every example.

## Rejection sampling

The final plotting cell calls `np.histogram(..., normed=True, density=True)`. Current NumPy no longer accepts `normed`; remove that argument and retain `density=True` when adapting the notebook.

## Importance sampling

The function named `p` is an **unnormalized** sum of Gaussian densities with weights 1 and 1.5. The printed `E[f]` calculation estimates the integral of `p(z) * f(z)`. To interpret it as an expectation under the normalized mixture, account for the normalizing constant **2.5**.

## Sampling–importance–resampling

`get_weights` explicitly normalizes the importance weights before resampling. The overlaid target curve has total mass **0.5**, while the histogram uses `density=True`; their different heights are expected. `Normal(mu, var)` accepts a variance, despite a nearby comment describing the proposal with a different scale.

## Metropolis–Hastings

Two details need correction before treating this notebook as a standard Metropolis–Hastings chain:

- The acceptance expression multiplies by the forward proposal density instead of placing it in the denominator. For the symmetric proposal used here, the proposal-density ratio should cancel.
- Rejected proposals are skipped. A standard chain records the current state again on rejection; keeping only accepted states changes the sampled distribution.

The saved plot is an illustrative historical output, not evidence that these details have been corrected.
