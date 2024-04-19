# Rebuttal-to-Reviewer-gJCN

Thank the reviewer for the valuable comments. We would like to address the reviewer's concerns as follows.

**Concern 1.** Thank the reviewer for this concern. We first clarify that we design the environment model as a permutation equivariant (PE) function with fusion architectures based on attention modules and pooling functions in DeepSet rather than directly adopting the DeepSet. Then, we highlight that

* **Different from most previous works that employ PE neural networks in modeling policies or value functions in RL algorithms (such as the papers the reviewer gives), taking advantage of their flexible input dimension property and the PE property, we utilize them to model the environment for the agent in RL algorithms, additionally taking advantage of their generalization abilities.**


Beside, we also highlight that

* **We are the first to prove the permutation equivariant/invariant (PE/PI) properties of the advertiser's transition rule and the reward function under a typical industrial auction mechanism that involves multiple stages (Proposition 5.1), which provides the basis for the PE environment model design.**
* **We are the first to both theoretically (E.q. 8) and empirically (Table 2 and Table 3) demonstrate the generalization superiority of PE/PI neural networks in modeling the environment in the auto-bidding field.
We have added a review on applying the PE neural networks in RL algorithms in the related work of the revised manuscript.**

**Concern 2 and the question.** Thank the reviewer for this concern. We clarify that the deep learning uncertainty contains two types of uncertainties, including:

* Aleatoric uncertainty: caused by the noises in the data, and
* Epistemic uncertainty: caused by the absence of data, (the training data does not cover the whole data space).

In this paper, the environment model is built as a probabilistic model with a mean and a covariance as outputs. We clarify that :

* **The covariance can capture the aleatoric uncertainty since it is inherently learned from the noise (or the ground truth range) and provides a range for noise prediction at the inference stage. Hence, it is naturally calibrated within the data and, in fact, helps with overcoming the overfitting issue.**
* For the epistemic uncertainty, we actually use the ensemble technique during our practical implementations. Specifically, we train several environment models $\hat{M} _ i,i\in [K]$ with random seeds, and use $\max_{i,j}|\hat{M}_{i}(\mathbf{s}_t,\mathbf{a}_t)-\hat{M}_j(\mathbf{s}_t,\mathbf{a}_t)|$ as an additional penalty. The reason is that, empirically, the larger the gap between the predictions of different environment models in the ensemble, the further the state-action pair is from the data, and the larger the epistemic uncertainty it can be [1]. Hence, we can use $\max _ {i,j}|\hat{M} _ {i}(\mathbf{s} _ t,\mathbf{a} _ t)-\hat{M} _ j(\mathbf{s} _ t,\mathbf{a} _ t)|$ to measure the epistemic uncertainty.

The overall penalty in this paper is in fact designed as:

$\min _ {i}\|\hat{\Sigma} _ i^\theta\| _ F+\beta \max _ {i,j}|\hat{M} _ {i}^\theta(\mathbf{s}_t,\mathbf{a}_t)-\hat{M}_j^\theta(\mathbf{s}_t,\mathbf{a}_t)|$. 

where $\beta>0$ is a hyperparameter.

We have added this explanation to the revised manuscript. 

[1] Chua, K., Calandra, R., McAllister, R., & Levine, S. (2018). Deep reinforcement learning in a handful of trials using probabilistic dynamics models. Advances in neural information processing systems, 31.

Moreover, we are pleased to let you know that although the experimental results in the paper come from proprietary codes and data, we have decided to open-source the codes of the proposed PE-MRL and the offline simulator as well as the used simulated offline dataset before we have a chance to prepare the camera-ready, in order to support and contribute to the auto-bidding field. 

**The codes and the dataset are available at** <https://anonymous.4open.science/r/AutoBiddingBenchmark-083F/README.md>.

**The added related works are available at** <https://anonymous.4open.science/r/Related-Works-of-the-PE-MRL-FDD1/README.md>.
