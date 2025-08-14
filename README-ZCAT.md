# ZCAT Pareto Front Generator

This repository provides tools to **generate Pareto Front approximations** for the 20 scalable **ZCAT benchmark problems**. These problems are widely used for testing multi-objective optimization algorithms in scenarios with scalable difficulty and characteristics.

The main function of interest is:

```python
generate_pareto_front(mop, max_solutions, nvar, nobj, Level, Bias_flag, Complicated_PS_flag, Imbalance_flag)
```

---

## 📂 Project Structure

- `zcat_generate_PF.py` — Main script that generates Pareto Front (PF) approximations.
- `zcat_tools.py`, `zcat_g.py`, `zcat_Z.py`, `zcat_F.py`, `zcat_benckmark.py`, `zcat_rnd_opt_sol.py` — Supporting modules required by ZCAT.
- **Output Folder:** `zcat-optimal-solutions/` — Generated PF files will be stored here.

---

## ⚙️ Function Description

### **`generate_pareto_front`**
Generates a Pareto Front approximation for a given ZCAT multi-objective problem and saves it to a `.pof` file.

#### **Parameters**
- `mop` *(int)*: Index of the ZCAT problem (0 = ZCAT1, ..., 19 = ZCAT20).
- `max_solutions` *(int)*: Number of solutions to generate for the PF.
- `nvar` *(int)*: Number of decision variables.
- `nobj` *(int)*: Number of objectives.
- `Level` *(int)*: Difficulty level (1–6). **Do not use levels 5 or 6** for PF generation.
- `Bias_flag` *(int)*: Whether to include bias (1 = True, 0 = False).
- `Complicated_PS_flag` *(int)*: Whether to use a complicated Pareto set (1 = True, 0 = False).
- `Imbalance_flag` *(int)*: Whether to include imbalance (1 = True, 0 = False).

#### **Returns**
A list of objective vectors representing the Pareto Front approximation.

#### **Output**
- A `.pof` file stored in the folder `zcat-optimal-solutions/`.
- Filename format:  
  ```
  {ProblemName}_{NumberOfSolutions}_{NumberOfObjectives}D.pof
  ```
  Example:
  ```
  ZCAT3_1000_03D.pof
  ```

---

## ▶️ How to Run

### **Option 1: Use `__main__` to batch generate PFs**
The script is configured to generate PFs for all 20 ZCAT problems, for objectives from 2 to 10, and various cardinalities.

Run:
```bash
python zcat_generate_PF.py
```

This will create multiple `.pof` files in the `zcat-optimal-solutions/` directory.

---

### **Option 2: Call `generate_pareto_front()` directly**
You can also import the function in your own Python code:

```python
from zcat_generate_PF import generate_pareto_front

# Example: Generate PF for ZCAT1 with 1000 solutions and 3 objectives
mop = 0  # ZCAT1
max_solutions = 1000
nobj = 3
nvar = nobj * 10  # Standard configuration
Level = 1
Bias_flag = 0
Complicated_PS_flag = 0
Imbalance_flag = 0

pf = generate_pareto_front(mop, max_solutions, nvar, nobj, Level, Bias_flag, Complicated_PS_flag, Imbalance_flag)
print("Generated PF with", len(pf), "solutions")
```

---

## ✅ Recommended Configuration

- `Level = 1`
- `Bias_flag = 0`
- `Complicated_PS_flag = 0`
- `Imbalance_flag = 0`

**Warning:** Levels 5 and 6 are not recommended for PF generation due to precision issues.

---

## 📜 Output File Format

Each `.pof` file starts with:
```
# {number_of_solutions} {number_of_objectives}
```
Followed by lines where each line represents an objective vector.

Example:
```
# 1000 3
1.234567e+00 5.678900e-01 9.101112e-02
...
```

---

## 🧩 ZCAT Benchmark: The 20 Problems

The ZCAT test suite contains **20 multi-objective problems** with diverse characteristics to evaluate the robustness of optimization algorithms:

| Problem    | Characteristics                                                                 |
|------------|---------------------------------------------------------------------------------|
| **ZCAT1**  | Simple convex Pareto front, separable decision variables                        |
| **ZCAT2**  | Convex PF with moderate bias                                                    |
| **ZCAT3**  | Non-convex PF, mild complexity in Pareto set                                    |
| **ZCAT4**  | Disconnected Pareto front                                                       |
| **ZCAT5**  | Degenerate PF (some objectives dependent)                                       |
| **ZCAT6**  | Highly biased objective mapping                                                 |
| **ZCAT7**  | Large-scale variables, smooth PF                                               |
| **ZCAT8**  | Complex Pareto set topology                                                     |
| **ZCAT9**  | Imbalanced distribution of Pareto front points                                  |
| **ZCAT10** | Multi-modal objective space                                                     |
| **ZCAT11** | Introduces deceptive variables                                                  |
| **ZCAT12** | Scalable dimensionality with non-separability                                   |
| **ZCAT13** | Irregular Pareto front with many local optima                                   |
| **ZCAT14** | Disconnected and biased PF                                                      |
| **ZCAT15** | Mixed separable and non-separable variables                                     |
| **ZCAT16** | High-dimensional objectives (many-objective scenario)                           |
| **ZCAT17** | Complex interaction between decision variables                                   |
| **ZCAT18** | Pareto front with large variance in spread                                      |
| **ZCAT19** | Multiple disconnected regions in objective space                                |
| **ZCAT20** | Most complex: imbalance, bias, non-convexity, and disconnected PF combined      |

These problems allow researchers to test **scalability**, **convergence**, and **diversity maintenance** under various challenging conditions.

---

## 🔗 Reference
ZCAT is a scalable benchmark suite for evaluating evolutionary and metaheuristic algorithms in multi-objective optimization under different complexities.
[https://doi.org/10.1016/j.swevo.2023.101350]
