# Yi-Zhang

# lmer_hdma: High-Dimensional Mediation Analysis with Random Effects

`lmer_hdma()` is an R function for performing high-dimensional mediation analysis in datasets with repeated measurements or clustered structures. It integrates variable selection using projection-based methods (lasso or ridge) with linear mixed-effects modeling, making it particularly suitable for environmental health and epidemiological studies involving hierarchical data.

---

## Features

- Supports both **Gaussian** and **binomial** outcomes  
- Adjusts for **group-level random effects** (e.g., subject ID) via `lmer`/`glmer`  
- Performs **high-dimensional variable selection** using projection methods (`hdi::lasso.proj` or `hdi::ridge.proj`)  
- Allows **covariate adjustment** at both mediator and outcome stages  
- Computes mediation effect (`α × β`) and proportion of total effect mediated  
- Supports **parallel computation** for improved efficiency

---

## Function Usage

lmer_hdma(
  X, Y, M, group,
  COV.XM = NULL, COV.MY = COV.XM,
  family = c("gaussian", "binomial"),
  method = c("lasso", "ridge"),
  topN = NULL, parallel = FALSE, ncore = 1, verbose = FALSE
)

## Arguments

| Argument   | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| `X`        | Exposure variable (numeric vector)                           |
| `Y`        | Outcome variable (numeric or binary)                         |
| `M`        | Mediator matrix (n samples × p features)                     |
| `group`    | Grouping variable (e.g., subject ID) for random intercepts   |
| `COV.XM`   | Optional covariates for the X → M models                     |
| `COV.MY`   | Optional covariates for the M → Y models (default: `COV.XM`) |
| `family`   | Model family for the outcome: `"gaussian"` or `"binomial"`   |
| `method`   | Variable selection method: `"lasso"` or `"ridge"`            |
| `topN`     | Number of top mediators to retain (optional)                 |
| `parallel` | Use parallel processing (`TRUE`/`FALSE`)                     |
| `ncore`    | Number of CPU cores (if `parallel = TRUE`)                   |
| `verbose`  | Show progress messages (`TRUE`/`FALSE`)                      |

## Output

| Column          | Description                                 |
| --------------- | ------------------------------------------- |
| `mediator`      | Mediator name                               |
| `alpha`         | Estimate for X → M                          |
| `beta`          | Estimate for M → Y                          |
| `gamma`         | Total effect of X on Y                      |
| `alpha*beta`    | Estimated indirect (mediation) effect       |
| `%total effect` | Proportion of total effect mediated         |
| `P.value`       | Joint p-value (max of p\_alpha and p\_beta) |


