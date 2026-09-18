# Statistics Recitation Repository Guide

## Repository purpose

This repository contains recitation materials for the Fall 2026 statistics course. The current completed unit is `r1`, which covers maximum likelihood estimation (MLE).

The user prefers concise, classroom-ready handouts that follow the style of their Fall 2025 recitation materials. Do not turn the material into slides unless the user explicitly changes this requirement.

## Recitation requirements

- Artifact language: English only.
- Format: printable LaTeX article/handout, not slides.
- Class length: 75 minutes.
- Review segment: about 20-30 minutes; the current pacing uses 25 minutes.
- Practice: allow roughly 5-10 minutes of independent work per problem before discussion.
- Prepare three core problems and one backup problem for a fast class.
- Prefer suitable exercises actually used in Fall 2025; create new exercises only when the old materials do not contain a close match.

## `rk` structure
for k th recitation

- Editable source: `rk/main.tex`
- Student PDF: `rk/output/pdf/Recitation k Problems.pdf`
- Instructor PDF: `rk/output/pdf/Recitation k Solutions.pdf`
- Temporary build products: `rk/build/student/` and `rk/build/solutions/`

`main.tex` is self-contained and uses a conditional switch:

- Default compilation produces the student version and excludes all `answer` environments.
- Defining `\WITHSOLUTIONS` produces the instructor version, including full solutions and the 75-minute pacing guide.


## Course notation convention

Use the notation of *Probability and Statistics for Data Science*, especially Section 2.1, throughout all student-facing materials:

- Write random variables as lowercase letters with a tilde, for example `\widetilde{x}`, `\widetilde{y}`, and `\widetilde{a}`. Do not use the more common uppercase-random-variable convention.
- Write observed realizations as ordinary lowercase letters, for example `x`, `y`, and `a`.
- Reserve uppercase `X` for the observed dataset: `X := {x_1, ..., x_n}`. In this course, `X` is a dataset, not a random variable.
- Write a pmf or pdf as `p_{\widetilde{x}}(x)` or `f_{\widetilde{x}}(x)` when naming the underlying random variable. Parametric families may be written as `p_theta(x)` or `f_theta(x)`.
- Treat frequentist model parameters such as `theta`, `lambda`, `mu`, and `sigma` as deterministic unless a Bayesian model explicitly makes them random. Do not add a tilde to ordinary model parameters.
- For an ML result computed from an observed dataset, use the course style `theta_ML`, `lambda_ML`, `mu_ML`, and `sigma_ML`, without hats. When discussing an estimator as a random quantity before the data are observed, give the estimator a tilde, for example `\widetilde{theta}_n`.
- For the observed sample mean, use `m(X) = (1/n) sum_i x_i` or `\bar{x}`; never use `\bar{X}` for a random variable.

These conventions were applied to Recitation 1 following instructor feedback. Preserve them in future revisions so that the recitation agrees with the book and lecture slides.


## Source material

Primary course handouts supplied by the user:

- Book/preprint and notation reference:
  https://github.com/cfgranda/ps4ds/blob/main/ps4ds_preprint.pdf

- Discrete/Poisson context:
  https://github.com/cfgranda/ps4ds/blob/main/slides/discrete%20variables/parametric_vs_nonparametric_handout.pdf
- Continuous/Gaussian MLE:
  https://github.com/cfgranda/ps4ds/blob/main/slides/continuous%20variables/maximum_likelihood_continuous_models_handout.pdf

Fall 2025 archive (available as an additional project/workspace root):

`/Users/zhangxuanxi/Documents/1_学习/14_2025fall/stats`


