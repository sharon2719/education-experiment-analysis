# Designing and Analysing Education Experiments

This project demonstrates the full lifecycle of an education experiment: planning a school-level randomised trial, then analysing a real randomised controlled trial and communicating the results to non-technical audiences.

## Key findings

- **Experiment design:** Detecting a small effect (0.15 SD) requires about 1,400 students if individuals can be randomised. When randomising schools with 30 students each and an intra-cluster correlation of 0.2, the requirement rises to about **318 schools**, more than six times the independent-sample estimate.
- **Experiment analysis:** In the Tennessee STAR experiment, kindergarten students in small classes scored **0.19 SD higher in maths** than those in regular classes (95% CI: 0.07 to 0.30, p = 0.002), comparing students within the same school.
- **Randomisation check:** Treatment groups were balanced on gender, free-lunch status and ethnicity (differences of three percentage points or less).

## Project structure

| Notebook | What it covers |
|---|---|
| [`experiment_design.ipynb`](experiment_design.ipynb) | Power analysis for a hypothetical school-level trial (SMS reminders to teachers), design effect adjustment for clustering, and a chart of required sample size by ICC |
| [`experiment_analysis.ipynb`](experiment_analysis.ipynb) | Analysis of the Tennessee STAR class-size experiment: data exploration, balance checks, treatment effect estimation with school fixed effects and clustered standard errors, limitations and a plain-language summary |

## Part 1: Experiment design

**Question:** If an education programme tested SMS reminders to teachers, how many schools would the experiment need?

Because the intervention reaches teachers, the whole class is affected, so schools rather than students must be randomised. Students in the same school tend to perform similarly, which reduces the information each additional student provides. I calculated the base sample size with a power analysis, then adjusted it using the design effect across a range of plausible ICC values.

**Takeaway:** Sample size requirements for school-level trials depend heavily on the ICC, so it should be estimated from existing learner data before planning an experiment.

## Part 2: Experiment analysis

**Question:** Did small classes improve kindergarten maths scores?

| Method | Effect (SD) | 95% CI | p-value |
|---|---|---|---|
| Simple comparison | 0.162 | 0.053 to 0.271 | 0.004 |
| Within-school comparison (preferred) | 0.185 | 0.070 to 0.301 | 0.002 |

The within-school estimate is preferred because randomisation took place within schools. Standard errors are clustered by school.

**Limitations:** About 7% of students in the analysed groups had no kindergarten maths score. The results cover kindergarten maths only and come from a US study in the 1980s, so they may not transfer directly to other contexts.

**Next questions to explore:** whether effects differ for low-income students, whether gains persist into later grades, and whether a teaching aide offers a lower-cost alternative.

## Methods and tools

- **Methods:** power analysis, design effects for cluster randomisation, balance checks, OLS regression with fixed effects, cluster-robust standard errors, effect sizes in standard deviations
- **Tools:** Python (pandas, statsmodels, matplotlib), Google Colab

## Data

The Tennessee STAR (Student/Teacher Achievement Ratio) dataset, accessed through the `AER` R package via `statsmodels.datasets.get_rdataset("STAR", "AER")`. No download is needed to run the notebooks.

Reference: Krueger, A. B. (1999). Experimental Estimates of Education Production Functions. *Quarterly Journal of Economics*, 114(2), 497–532.

## How to run

Open either notebook in [Google Colab](https://colab.research.google.com) or Jupyter and run the cells in order. All required libraries are pre-installed in Colab.
