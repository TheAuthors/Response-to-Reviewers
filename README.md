# Response-to-Reviewers

Review of the literature mentioned by the Reviewer v8xA.

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

[Baudel et al, 2023], [Hu et al, 2019], [Mori et al, 2022] all have white noise which is very narrow example of condition $[\mathbf{H}_2]$ which leads to a larger times to escape a basin of local mimima. Given that, [Hu et al, 2019] use Large Deviations Theory which gives weak approximations, and [Baudel et al, 2023] are interested in metastable dynamics (not unlike Wang et al.) which is too large of scope comparing with questions we consider in our paper.


\textbf{Large deviation theory.} In the works [Azizian et al., 2024], [Bajovi et al, 2023]   the random variables \(\xi_k\) are sub-Gaussian; in [Hult et al, 2025]
the random variables \(\xi_k\)  have a finite exponential moment.  
Obviously, such random variables represent a special case when the condition \([\mathbf{H}_2]\) holds.   
It is worth noting that, in principle, their large deviation methods allow studying the asymptotic behavior in SGD only when 
$ {E} e^{c|\xi_k|} < \infty$
for all \(c > 0\).  So called light tail case. Although the authors of [Azizian et al., 2024] and [Bajovi et al, 2023]  impose an even stronger condition.  
It is easy to see that this condition is not satisfied by any random variables from the class \([\mathbf{H}_1]\) and by "most" random variables from the class \([\mathbf{H}_2]\).  
As can be observed from the works [Wang et al., 2021], [Imkeller, Pavlyukevich, 2008], [Simsekli et al., 2019], the overall dynamics of SGD will be significantly different in the case of light tails.  





\textbf{Statistical physics methods.} To briefly summarize, the works by [Mignacco et al, 2020],  [Veiga et al, 2024] employ a continuous approximation of stochastic gradient dynamics and adopt settings that allow deriving analytical expressions for (among other things) generalization error. They further empirically demonstrate the consistency of their theoretical framework with practical observations. In contrast, our work focuses exclusively on the dynamics of idealized stochastic gradient descent, but we provide limit theorems with a  probability proof. 

In another study, [Mignacco et al, 2022], the authors provide a phenomenological description of the noise arising in SGD algorithms applied to binary classification tasks for Gaussian mixtures. They find that such noise can be well characterized by an effective temperature derived using the fluctuation-dissipation theorem. Unlike this phenomenological approach, we simplify the SGD model to one with additive noise and obtain theoretical results while making minimal restrictive assumptions about the noise distribution. Therefore, a direct comparison of their findings with our results is not feasible.

However, it should be noted that the aforementioned works are highly interesting and present an intriguing approach to analyzing the dynamics of SGD algorithms in real-world machine learning problems. So, most probably we should include these papers.


\textbf{Diagonal Linear Networks}, as shown in the work by [Berthier et al. (2023)], are systems where features become activated not all at once, but gradually. Starting from small (near-zero) initial values, the model tends to remain "stuck" near partial "saddle-like" states for extended periods before transitioning to a state with fuller feature activation. The early stages of training produce very sparse solutions, but over time, an increasing number of coordinates begin to participate, resulting in a richer final model. The number of genuinely active features directly depends on how long the training continues—the longer the process runs, the lower the sparsity becomes. The dynamics of wandering among stable states somewhat resemble the effects we describe for SGD in our article; however, in our case, the system can return to previously visited equilibrium points.
