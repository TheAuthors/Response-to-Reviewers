# Response-to-Reviewers

## Review of the literature mentioned by the Reviewer v8xA.

**Diffusion approximation.** Thank you for listing a number of potentially useful citations for our paper. Sadly, you did not used a proper citation so the actual papers are left ambiguous.

Papers about diffusion approximation: [Li et al, 2022], [Baudel et al, 2023], [Hu et al, 2019], [Mori et al, 2022], [Xi et al 2020], [Nguyen et al, 2019]
We haven't found any papers on the topic which fits [Xi et al 2020]. Did you mean [Xie et al 2020] which may refer to
Xie, Zeke, Issei Sato, and Masashi Sugiyama. "A diffusion theory for deep learning dynamics: Stochastic gradient descent exponentially favors flat minima." arXiv preprint arXiv:2002.03495 (2020).
The rest we believe refer to
Li, Lei, and Yuliang Wang. "On uniform-in-time diffusion approximation for stochastic gradient descent." arXiv preprint arXiv:2207.04922 (2022).
Baudel, Manon, Arnaud Guyader, and Tony Lelièvre. "On the Hill relation and the mean reaction time for metastable processes." Stochastic Processes and their Applications 155 (2023): 393-436.
Hu, Wenqing, et al. "Quasi-potential as an implicit regularizer for the loss function in the stochastic gradient descent." arXiv preprint arXiv:1901.06054 (2019).
Mori, Takashi, et al. "Power-law escape rate of SGD." International Conference on Machine Learning. PMLR, 2022.
Nguyen, Thanh Huy, et al. "First exit time analysis of stochastic gradient descent under heavy-tailed gradient noise." Advances in neural information processing systems 32 (2019).


Diffusion approximation topic overall is close to our topic and papers in this field showcase the behavior of SGD we study. However, in papers that came up in our research that approach was working with continuous and mostly smooth functions which we believe is not essential for many properties of SGD. Thus, we did not use many citations from this area.

Nevertheless, [Nguyen et al, 2019] is very useful citation and we somehow missed it in our overview. This paper analyses a different model, which is an Euler discretization of L\'evy-driven SDE, and provides conditions under which the tail-probability for the first time to leave a basin for a minimum is similar between discrete and continuous models. Such results are important step for understanding longtime behavior of SGD.  In our paper we firstly take different model with potentially discontinuous loss function and less restrictive conditions on the distribution of errors. Secondly, we take a closer look at time regions when SGD either converging to a minimum or is still in a neighborhood of other critical points.

[Baudel et al, 2023], [Hu et al, 2019], [Mori et al, 2022] all have white noise which is very narrow example of condition H2 which leads to a larger times to escape a basin of local mimima. Given that, [Hu et al, 2019] use Large Deviations Theory which gives weak approximations, and [Baudel et al, 2023] are interested in metastable dynamics (not unlike Wang et al.) which is too large of scope comparing with questions we consider in our paper.


**Large deviation theory.** In the works [Azizian et al., 2024], [Bajovi et al, 2023]   the random variables $$\xi_k$$ are sub-Gaussian; in [Hult et al, 2025]
the random variables $$\xi_k$$  have a finite exponential moment.
Obviously, such random variables represent a special case when the condition H2 holds.   
It is worth noting that, in principle, their large deviation methods allow studying the asymptotic behavior in SGD only when 
$$E e^{c|\xi_k|} < \infty$$
for all $$c > 0$$.  So called light tail case. Although the authors of [Azizian et al., 2024] and [Bajovi et al, 2023]  impose an even stronger condition.  
It is easy to see that this condition is not satisfied by any random variables from the class H1 and by "most" random variables from the class H2.  
As can be observed from the works [Wang et al., 2021], [Imkeller, Pavlyukevich, 2008], [Simsekli et al., 2019], the overall dynamics of SGD will be significantly different in the case of light tails.  

**Statistical physics methods.** To briefly summarize, the works by [Mignacco et al, 2020],  [Veiga et al, 2024] employ a continuous approximation of stochastic gradient dynamics and adopt settings that allow deriving analytical expressions for (among other things) generalization error. They further empirically demonstrate the consistency of their theoretical framework with practical observations. In contrast, our work focuses exclusively on the dynamics of idealized stochastic gradient descent, but we provide limit theorems with a  probability proof. 

In another study, [Mignacco et al, 2022], the authors provide a phenomenological description of the noise arising in SGD algorithms applied to binary classification tasks for Gaussian mixtures. They find that such noise can be well characterized by an effective temperature derived using the fluctuation-dissipation theorem. Unlike this phenomenological approach, we simplify the SGD model to one with additive noise and obtain theoretical results while making minimal restrictive assumptions about the noise distribution. Therefore, a direct comparison of their findings with our results is not feasible.

However, it should be noted that the aforementioned works are highly interesting and present an intriguing approach to analyzing the dynamics of SGD algorithms in real-world machine learning problems. So, most probably we should include these papers.


**Diagonal Linear Networks,** as shown in the work by [Berthier et al. (2023)], are systems where features become activated not all at once, but gradually. Starting from small (near-zero) initial values, the model tends to remain "stuck" near partial "saddle-like" states for extended periods before transitioning to a state with fuller feature activation. The early stages of training produce very sparse solutions, but over time, an increasing number of coordinates begin to participate, resulting in a richer final model. The number of genuinely active features directly depends on how long the training continues—the longer the process runs, the lower the sparsity becomes. The dynamics of wandering among stable states somewhat resemble the effects we describe for SGD in our article; however, in our case, the system can return to previously visited equilibrium points.

## Numerical experiments. 
### Convergence to minima

In the first simulation, we set $\varepsilon = 0.0001$ and consider stochastic gradient descent (SGD) on a cubic spline target function with two minima at $x = -1$ and $x = 1$, and a maximum at $x = 0$. We then plot the trajectory of SGD under two types of noise: centered alpha-stable noise with parameter $\alpha = 1.5$  (H1), and standard Gaussian noise (H2).
We observe that with alpha-stable noise, the trajectory tends to jump between the two minima. In contrast, under Gaussian noise, the process typically remains confined to the neighborhood of the initial minimum. 

![target](https://github.com/TheAuthors/Response-to-Reviewers/blob/92dc59bfb1159238f0d1f320e86e1d2507e1fa12/Reviewer%20v8xA/target.png)
![SGD2](https://github.com/TheAuthors/Response-to-Reviewers/blob/71b649c8a1ff0ddd4288e0cc20b8223ca5749655/Reviewer%20v8xA/SGD_2.png)
![SGD1](https://github.com/TheAuthors/Response-to-Reviewers/blob/a2d7d8daae7363afdb1add8c8bcd32aed2545063/Reviewer%20v8xA/SGD_1.png)

The simulations demonstrate that, generally speaking, SGD does not converge to a single minimum because it may oscillate between different minima. However, it is true that after some time, SGD eventually converges to and remains at a minimum. This behavior is illustrated in the following simulations.

TABLE TABLE TABLE 

As can be seen from this table, within the time n_epsilon found in the paper, SGD converges to a minimum (Theorem 2.1, Theorem 2.2). One can also observe the significant difference in the number of steps required for H1 and H2 cases.

### Escape maximum


The upper probability estimates shown in the following table  were obtained using explicit formulas (for the specific case of double exponential distribution) from the our paper (Corollary 2.11), with the exception of the roots $\mu_\uparrow$ and $\mu_\downarrow$, which were computed using the standard bisection method.
Estimates of the actual transition probabilities were obtained using a standard Monte Carlo method, running SGD near the sharp maximum $10^5$ times.

![table2](https://github.com/TheAuthors/Response-to-Reviewers/blob/64a8f16f84e7d852f0680786de837f3674d5f2ef/Reviewer%20v8xA/table2.jpg)
