# Statistics Recitation Repository Guide

## Repository purpose

This repository contains recitation materials for the Fall 2026 statistics course. The current completed unit is `r1`, which covers maximum likelihood estimation (MLE).

The user prefers concise, classroom-ready handouts that follow the style of their Fall 2025 recitation materials. Do not turn the material into slides unless the user explicitly changes this requirement.

## Recitation 1 requirements

- Artifact language: English only.
- Format: printable LaTeX article/handout, not slides.
- Class length: 75 minutes.
- Review segment: about 20-30 minutes; the current pacing uses 25 minutes.
- Practice: allow roughly 5-10 minutes of independent work per problem before discussion.
- Prepare three core problems and one backup problem for a fast class.
- Review MLE, then derive the MLEs for Poisson and Gaussian models.
- Prefer suitable exercises actually used in Fall 2025; create new exercises only when the old materials do not contain a close match.

## Current `r1` structure

- Editable source: `r1/main.tex`
- Student PDF: `r1/output/pdf/Recitation 1 Problems.pdf`
- Instructor PDF: `r1/output/pdf/Recitation 1 Solutions.pdf`
- Temporary build products: `r1/build/student/` and `r1/build/solutions/`

`main.tex` is self-contained and uses a conditional switch:

- Default compilation produces the student version and excludes all `answer` environments.
- Defining `\WITHSOLUTIONS` produces the instructor version, including full solutions and the 75-minute pacing guide.

Both current PDFs are five-page A4 documents. They have been compiled, rendered page by page, and visually checked.

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

## Current lesson content

The review covers:

1. Likelihood and log-likelihood for i.i.d. data.
2. A practical MLE workflow, including parameter spaces and boundary checks.
3. Poisson derivation:
   `lambda_ML = m(X) = (1/n) sum_i x_i`.
4. Gaussian derivation:
   `mu_ML = m(X)` and
   `sigma_ML^2 = (1/n) sum_i (x_i - m(X))^2`.
5. The distinction between the Gaussian variance MLE (divisor `n`) and the unbiased sample variance (divisor `n-1`).
6. Edge cases: all-zero Poisson observations and equal Gaussian observations.

The practice section contains:

1. A two-point discrete model, adapted from Fall 2025 Recitation 5.
2. A newly written Poisson help-desk call problem.
3. A newly written Gaussian repeated-measurement problem.
4. A backup true/false problem adapted and narrowed from Fall 2025 Recitation 5.

The Fall 2025 problem originally included method of moments. That part was intentionally removed because the requested scope for this recitation is MLE. Keep future revisions aligned with the current course sequence rather than copying every part of an old exercise.

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

Most relevant files:

- `mine/r1/r1.tex`: example of the user's prior handout style.
- `mine/r5/r5.tex`: the user's prior MLE recitation source.
- `Recitations/Recitation 5 Problems.pdf`: official Fall 2025 MLE worksheet.
- `Recitations/Recitation 5 Solutions.pdf`: official solutions, mostly scanned.
- `wyt/Recitation 5.pdf`: handwritten point-estimation/MLE notes.

In the Fall 2025 archive, Recitation 5 is the closest match to the current MLE topic. It contains the two-point-model and true/false exercises but no direct Poisson or unknown-mean/unknown-variance Gaussian MLE practice problem. This is why Problems 2 and 3 were newly written.

## Build commands

Run from `r1`:

```bash
mkdir -p build/student build/solutions output/pdf

pdflatex -interaction=nonstopmode -halt-on-error \
  -output-directory=build/student \
  -jobname='Recitation 1 Problems' main.tex
pdflatex -interaction=nonstopmode -halt-on-error \
  -output-directory=build/student \
  -jobname='Recitation 1 Problems' main.tex

pdflatex -interaction=nonstopmode -halt-on-error \
  -output-directory=build/solutions \
  -jobname='Recitation 1 Solutions' \
  '\def\WITHSOLUTIONS{1}\input{main.tex}'
pdflatex -interaction=nonstopmode -halt-on-error \
  -output-directory=build/solutions \
  -jobname='Recitation 1 Solutions' \
  '\def\WITHSOLUTIONS{1}\input{main.tex}'

cp 'build/student/Recitation 1 Problems.pdf' \
  'output/pdf/Recitation 1 Problems.pdf'
cp 'build/solutions/Recitation 1 Solutions.pdf' \
  'output/pdf/Recitation 1 Solutions.pdf'
```

## Validation expectations

After meaningful edits:

1. Compile both variants twice with `-halt-on-error`.
2. Check the logs for `Overfull`, `Underfull`, `Warning`, and `Error` messages.
3. Use `pdfinfo` to confirm page size and page count.
4. Render every page with `pdftoppm`, for example:

   ```bash
   pdftoppm -png -r 120 'output/pdf/Recitation 1 Problems.pdf' /tmp/r1-problems-page
   pdftoppm -png -r 120 'output/pdf/Recitation 1 Solutions.pdf' /tmp/r1-solutions-page
   ```

5. Visually inspect every rendered page for clipping, bad page breaks, crowded formulas, or insufficient student working space.
6. Use `pdftotext` to verify that the student PDF contains no solution text and the instructor PDF contains all solutions.

The current source may emit a harmless underfull-box warning around the explicit line break before the backup problem list. The rendered layout has been inspected and is correct. Fix it only if the visual layout remains at least as clear.

## Editing conventions

- Preserve the simple Fall 2025 article style: A4, 11 pt, restrained typography, numbered review sections, and clearly separated exercises.
- Keep the student and instructor PDFs generated from the same source.
- Keep mathematical notation and parameter domains explicit.
- Verify maxima rather than reporting only solutions to score equations.
- Keep instructor-only pacing information out of the student version.
- Preserve unrelated user files and edits.
- Use `apply_patch` for manual source edits.
