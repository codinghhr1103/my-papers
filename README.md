# Haoran Hu (胡浩然)

**Researcher · Wireless Network Security · Statistical Machine Learning**

---

## 👋 About Me

I am a researcher working at the intersection of **wireless network security** and **statistical machine learning**. My work centers on two threads:

- Designing **distributed, resource-aware algorithms** that keep resource-constrained networks secure without relying on heavyweight cryptography.
- Developing **likelihood-based parameter estimation methods** for probabilistic latent variable models, with applications to high-dimensional biomedical data.

The common thread across both directions is a preference for methods that are **mathematically principled, computationally lightweight, and empirically validated on real data**.

---

## 🧭 Research Interests

| Area | Focus |
| :--- | :--- |
| **Wireless Sensor Network Security** | Non-cryptographic countermeasures against inference attacks in compressive sensing-based data gathering; topology-aware defense mechanisms for IoT and smart-city infrastructure |
| **Statistical Machine Learning** | Probabilistic latent variable models, likelihood-based parameter estimation, dimensionality reduction, applications in multi-omics data analysis |
| **Distributed Algorithm Design** | Self-organized, lightweight protocols for dynamic network reconfiguration under security and energy constraints |

---

## 📚 Publications

| # | Venue | Year | Title | PDF |
| :-: | :--- | :-: | :--- | :-: |
| 3 | **ECAI** | 2025 | Scalar Likelihood Method for Probabilistic Partial Least Squares Model with Rank n Update | [📄](./Scalar%20Likelihood%20Method%20for%20Probabilistic%20Partial%20Least%20Squares%20Model%20with%20Rank%20n%20Update.pdf) |
| 2 | **Peer-to-Peer Networking and Applications** | 2021 | Non-cryptography countermeasure against controllable event triggering attack in WSNs | [📄](./Non-cryptography%20countermeasure%20against%20controllable%20event%20triggering%20attack%20in%20WSNs.pdf) |
| 1 | **IEEE ICCCN** | 2020 | On the Mitigation of Controllable Event Triggering Attack in WSNs | [📄](./On%20the%20Mitigation%20of%20Controllable%20Event%20Triggering%20Attack%20in%20WSNs.pdf) |

<details>
<summary><b>Full citations (click to expand)</b></summary>

> **Haoran Hu**, Wei Chang. *"On the Mitigation of Controllable Event Triggering Attack in WSNs."* 2020 29th International Conference on Computer Communications and Networks (ICCCN), 2020.

> **Haoran Hu**, Wei Chang. *"Non-cryptography countermeasure against controllable event triggering attack in WSNs."* Peer-to-Peer Networking and Applications, 14:1071–1087, 2021.

> **Haoran Hu**, Xingce Wang, Zhongke Wu, Shilei Du, Yuhe Zhang, Quansheng Liu. *"Scalar Likelihood Method for Probabilistic Partial Least Squares Model with Rank n Update."* ECAI 2025.

</details>

---

## 🔍 Research Summaries

### 1 · On the Mitigation of CETA in WSNs *(ICCCN 2020)*

> **Summary** — The first non-cryptographic defense against the Controllable Event Triggering Attack on compressive data gathering, built on a novel topology-encoding scheme and a distributed subtree-modification protocol.

Compressive data gathering (CDG) cuts communication costs in wireless sensor networks by transmitting *weighted sums* of sensor readings instead of raw data. The catch: CDG is vulnerable to the **Controllable Event Triggering Attack (CETA)**, where an adversary who compromises one sensor can infer the secret measurement coefficients of downstream nodes by deliberately manipulating the environment (e.g., nudging temperature by $\Delta x$ and watching the returned weighted sum change by $\Delta y$).

Prior defenses were **cryptographic and centralized** — they need key management and a central controller, both awkward in a sensor network. This paper introduces the first **non-cryptographic, distributed** alternative. The insight: if the data-gathering tree *restructures itself every round*, the variance caused by a controllable event gets masked by the variance caused by membership changes in the subtree, and the attacker's inference breaks down.

**Key contributions**

- A **topology-based coding scheme (Topology ID)** — each node's position in the tree is encoded as a compact binary string, letting nodes reason about their own subtree membership without global information.
- The **Subtree Modification Algorithm (SMA)** — a self-organized, distributed protocol that restructures subtrees every sensing round while guaranteeing loop-freedom and avoiding redundant modifications.
- Simulations showing substantial increases in the time required to successfully launch a CETA attack.

---

### 2 · Non-cryptography Countermeasure against CETA in WSNs *(Peer-to-Peer Networking and Applications 2021)*

> **Summary** — The full journal version of the ICCCN paper, promoting a single algorithm into a **three-algorithm family** (SMA + LPCA + PSA) and validating on both synthetic topologies and the Intel Lab real-world deployment.

This is the extended journal version of the ICCCN work. The conference paper established the framework; this paper makes it **practical and complete**. We observed that SMA alone changes the parents of non-leaf nodes but leaves leaf nodes passive, and that blindly scheduling parent changes every round inflates communication cost. Two new algorithms address these gaps.

**Key contributions**

- **Subtree Modification Algorithm (SMA)** — refined from the conference version.
- **Leaf Parent Changing Algorithm (LPCA)** — a two-phase protocol. (1) During a leaf node's dedicated time slot, it re-homes itself to a neighbor that still has room in its children array (capacity cap of 8), causing a group of leaves to migrate *passively*. (2) Remaining nodes that have not had their subtree membership changed fall back to SMA. This drives the percentage of nodes whose subtree membership changes each round much closer to 100%.
- **Partial Scheduling Algorithm (PSA)** — balances *scheduled* parent changes (deterministic, security-guaranteed) against *opportunistic* parent changes (cheaper, best-effort), and explicitly optimizes the **security-to-cost ratio**.
- **Experimental validation** on randomly generated topologies and the **Intel Lab sensor dataset**, measuring attack-delay-per-packet-overhead for the full design space. LPCA's security advantage grows with network size, because the fraction of leaf nodes grows with it.

---

### 3 · Scalar Likelihood Method for Probabilistic PLS *(ECAI 2025)*

> **Summary** — A drop-in replacement for EM in the PPLS model that is about $12\times$ faster, has asymptotically lower complexity, avoids $\sigma_h^2$ degeneracy, and detects more significant gene–protein associations on TCGA breast-cancer multi-omics data.

Probabilistic Partial Least Squares (PPLS) generalizes classical PLS with a generative latent-variable model, adding uncertainty quantification and principled model selection. The standard fitting recipe is the EM algorithm — but EM's alternating scheme is computationally heavy in high dimensions, sensitive to initialization, and prone to degenerate noise-variance solutions.

This paper proposes the **Scalar Likelihood Method (SLM)**: instead of alternating E/M steps on latent variables, directly optimize the **observed-data log-likelihood expanded into scalar form**, then plug any off-the-shelf optimizer (Newton–Raphson, quasi-Newton, stochastic approximation) into that scalar objective.

**Key contributions**

- A <b>rank-$n$ update technique</b> that extends the classic Sherman–Morrison rank-one update to compute the determinant and inverse of the PPLS covariance matrix **without requiring square loading matrices** — preserving PPLS's dimension-reduction property (previous scalar formulations had to give this up).
- **Closed-form maximum-likelihood estimators** for the isotropic noise variances $\sigma_e^2$, $\sigma_f^2$, $\sigma_h^2$, decoupling them from the remaining parameters. This <i>fixes the $\sigma_h^2$ degeneracy</i> observed in EM/ECM, where the algorithm is prone to collapsing into a degenerate solution.
- **Complexity reduction**
    - Time: $O(p^3 + q^3) \rightarrow O(r p^2 + r q^2)$
    - Space: $O((p + q)^2) \rightarrow O(p^2 + q^2)$
    - where $p, q$ are the two data dimensions and $r$ is the latent dimension, with $r \ll \min(p, q)$.
- **Experimental results**
    - On simulated PPLS data, SLM achieves about $12\times$ speedup over matrix-form EM across a wide range of $(p, q, r)$ combinations.
    - On the **BRCA multi-omics TCGA dataset** (705 breast cancer patients, gene expression $\times$ protein expression), SLM consistently detects **more significant gene–protein pairs than EM at every significance level** — with notably low overlap between the two, suggesting SLM surfaces biological associations that EM systematically misses.
    - A prediction pipeline built on the conditional distribution of a multivariate Gaussian yields well-calibrated uncertainty estimates across confidence levels in 5-fold cross-validation.

---

## 📦 Repository Layout

```
my-papers/
├── README.md                                                                            ← you are here
├── On the Mitigation of Controllable Event Triggering Attack in WSNs.pdf                 ← ICCCN 2020
├── Non-cryptography countermeasure against controllable event triggering attack in WSNs.pdf  ← PPNA 2021
└── Scalar Likelihood Method for Probabilistic Partial Least Squares Model with Rank n Update.pdf  ← ECAI 2025
```

---

## 🤝 Get in Touch

I'm always open to discussion, collaboration, or just swapping ideas — whether about wireless security, latent-variable models, or anything else at the boundary of statistics and systems.

**📧 Email**: [hhrh1h2r3@gmail.com](mailto:hhrh1h2r3@gmail.com)

If you find these works useful, a ⭐ on this repo is very much appreciated!
