# RSEsubset_selection
Repository for the IEEE TEVC Paper "Fast High-Diversity Subset Selection for Multiobjective Optimization by Riesz s-Energy".

# Available Greedy Algorithms for Pair-Potential Energy-Based Subset Selection

- **inclusion** - `RSEInclusion`: greedy inclusion strategy based on Riesz s-energy.
- **rand_inclusion** - `RSErInclusion`: randomized greedy inclusion strategy based on Riesz s-energy.
- **removal** - `RSERemoval`: greedy removal strategy based on Riesz s-energy.
- **rand_removal** - `RSErRemoval`: randomized greedy removal strategy based on Riesz s-energy.
- **iterative** - `RSEIterative`: randomized iterative greedy removal algorithm based on Riesz s-energy.

---

## **Execution Syntax**

```
python reduce.py PPF algorithm [num_samples] instance dimension subset_size executions distance [p_minkowski]
```

### **Parameters**

- **PPF:** Pair-potential energy.
    - `RSE`: Riesz s-energy.
    - `COU`: Coulomb's law.
    - `GAE`: Gaussian alpha energy.
    - `PTP`: Pöschl-Teller potential.
    - `MPT`: Modified Pöschl-Teller potential.
    - `KRA`: Kratzer potential.

- **algorithm:** Greedy algorithm to be executed.
    - `inclusion`: Fast greedy inclusion algorithm.
    - `rand_inclusion`: Randomized fast greedy inclusion algorithm.
    - `removal`: Fast greedy removal algorithm.
    - `rand_removal`: Randomized fast greedy removal algorithm.
    - `iterative`: Fast iterative greedy removal algorithm.

- **[num_samples]:** *Optional.* Number of samples when using a randomized algorithm.

- **instance:** File to be processed.

- **dimension:** Dimension of the points to be processed.

- **subset_size:** Desired subset size.

- **executions:** Number of executions.

- **distance:** Distance metric used by the PPFs.
    - `euclidean`: Euclidean distance.
    - `seuclidean`: Standardized Euclidean distance.
    - `cityblock`: City block (Manhattan) distance.
    - `chebyshev`: Chebyshev distance.
    - `cosine`: Cosine distance.
    - `correlation`: Correlation distance.
    - `canberra`: Canberra distance.
    - `braycurtis`: Bray-Curtis distance.
    - `mahalanobis`: Mahalanobis distance.
    - `minkowski`: Minkowski distance.

- **[p_minkowski]:** *Optional.* Required when using Minkowski distance (specify the `p` value).

---

## **Execution Examples**

```bash
python reduce.py RSE inclusion DTLZ1 3 100 30 euclidean
python reduce.py RSE removal DTLZ1 3 100 30 braycurtis
python reduce.py RSE rand_inclusion 100 DTLZ1 3 100 30 canberra
python reduce.py RSE rand_removal 10 DTLZ1 3 100 30 minkowski 2
python reduce.py RSE iterative 1000 DTLZ1 3 100 30 euclidean
python reduce.py RSE iterative 1000 DTLZ1 3 100 30 minkowski 5
```
