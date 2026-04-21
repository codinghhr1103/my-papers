# Haoran Hu

## About Me

I am a researcher with interdisciplinary interests spanning **wireless network security** and **statistical machine learning**. My work focuses on designing efficient, distributed algorithms for resource-constrained systems and developing novel parameter estimation methods for probabilistic models.

## Research Interests

- **Wireless Sensor Network Security** — Countermeasures against inference attacks in compressive sensing-based data gathering; topology-aware, non-cryptographic defense mechanisms for IoT and smart city infrastructure.
- **Statistical Machine Learning** — Probabilistic latent variable models, likelihood-based parameter estimation, and dimensionality reduction with applications in multi-omics data analysis.
- **Distributed Algorithm Design** — Self-organized, lightweight protocols for dynamic network reconfiguration under security and energy constraints.

## Publications

**Haoran Hu**, Wei Chang. "Non-cryptography countermeasure against controllable event triggering attack in WSNs." *Peer-to-Peer Networking and Applications*, 14:1071–1087, 2021. [[DOI]](https://doi.org/10.1007/s12083-020-01062-6)

**Haoran Hu**, Wei Chang. "On the Mitigation of Controllable Event Triggering Attack in WSNs." *ICCCN 2020*.

**Haoran Hu**, Xingce Wang, Zhongke Wu, Shilei Du, Yuhe Zhang, Quansheng Liu. "Scalar Likelihood Method for Probabilistic Partial Least Squares Model with Rank n Update." *ECAI 2025*. 

## Research Summary

### Defending Compressive Data Gathering in WSNs

Compressive data gathering (CDG) reduces communication costs in wireless sensor networks by transmitting weighted sums of sensor readings instead of raw data. However, CDG is vulnerable to the **Controllable Event Triggering Attack (CETA)**, where an adversary compromises a sensor node and manipulates the environment around a target to infer secret measurement coefficients.

I proposed a **non-cryptographic defense** based on dynamically restructuring the data gathering tree between sensing rounds. The core insight is that if the subtree membership of every node changes each round, the attacker cannot isolate the contribution of a single target from the aggregate weighted sum. To realize this, I designed:

- A **topology-based coding scheme** (Topology ID) that compactly encodes each node's position in the tree as a binary string, enabling efficient distributed coordination.
- The **Subtree Modification Algorithm (SMA)**, a distributed protocol that restructures subtrees while guaranteeing loop-freedom, avoiding redundant modifications, and maximizing subtree novelty across rounds.
- The **Partial Scheduling Algorithm (PSA)**, which balances scheduled and opportunistic parent changes to optimize the security-to-cost ratio.

Simulations on both synthetic and real sensor deployments (Intel Lab dataset) show that these algorithms significantly increase the time required for a successful CETA attack with manageable communication overhead.

### Scalar Likelihood Method for Probabilistic PLS

Probabilistic Partial Least Squares (PPLS) extends classical PLS by introducing a generative model with latent variables and noise, enabling uncertainty quantification and principled model selection. However, parameter estimation via the EM algorithm is computationally expensive and prone to degenerate solutions.

I developed the **Scalar Likelihood Method (SLM)**, which directly optimizes the observed-data log-likelihood expressed in scalar form. Key contributions include:

- A **rank-n update technique** that computes the determinant and inverse of the PPLS covariance matrix without requiring square loading matrices, preserving the dimension-reduction property of the model.
- **Closed-form noise variance estimators** derived from maximum likelihood principles, which decouple noise parameters from the remaining optimization and improve numerical stability.
- Reduction of computational complexity from O(p³ + q³) to O(rp² + rq²) and space from O((p+q)²) to O(p² + q²), enabling application to high-dimensional multi-omics datasets.

SLM achieves ~12× faster convergence than EM, avoids the σ²_h degeneracy problem observed in EM/ECM, and detects substantially more significant gene-protein associations in TCGA breast cancer data.

## Contact

📧 hhrh1h2r3@gmail.com
