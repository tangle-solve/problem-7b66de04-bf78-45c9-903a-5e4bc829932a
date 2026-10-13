<!-- solve-problem:7b66de04-bf78-45c9-903a-5e4bc829932a -->
# Continuous Skolem problem

A [Tangle Solve problem](https://solve.tangle.tools/problems/7b66de04-bf78-45c9-903a-5e4bc829932a).

## What is the problem?

Given a rational (or equivalently algebraic) square matrix \(A \in \mathbb{Q}^{n\times n}\), a rational vector \(x \in \mathbb{Q}^n\), and a rational linear functional \(c \in \mathbb{Q}^n\), decide whether the scalar trajectory

\[
f(t) = c^\top e^{At} x, \qquad t \in \mathbb{R},
\]

satisfies \(f(t) = 0\) for some \(t > 0\). Degenerate cases where \(f\) is identically zero on an interval (which happens only if \(f \equiv 0\), by real-analyticity) are handled separately, so the real question is about *isolated* zeros of the exponential-polynomial trajectory. This is the continuous-time analogue of the (discrete) Skolem Problem, which asks whether a linear recurrence sequence \(u_k = c^\top A^k x\) has a zero term. The continuous version reduces to: does a real exponential polynomial \(\sum_i p_i(t) e^{\lambda_i t}\) (with algebraic \(\lambda_i\) and algebraic polynomial coefficients, coming from the eigenvalues of \(A\)) have a strictly positive real root? Decidability for arbitrary dimension \(n\) is open.

## Why does it matter?

This is the reachability/observability decision problem for continuous linear dynamical systems, central to verification and hybrid-systems model checking: many safety properties of cyber-physical systems reduce exactly to "does this linear ODE trajectory hit this hyperplane?". It is the natural bridge between the discrete Skolem problem (itself open for order ≥ 5) and continuous dynamics, and it drives work on the reachability problem for linear (semi-)algebraic invariants. A decidability proof (or undecidability proof) would settle a flagship question of the "continuous analogues of decision problems on automata" program of Ouaknine, Worrell, and collaborators.

## What's already known?

- **Chonev, Ouaknine, Worrell (2016)** gave the main partial results: decidability for continuous Skolem under restrictions — in particular for bounded dimension (with Schanuel's-conjecture-flavoured assumptions entering for certain eigenvalue configurations), and a careful analysis of when zeros of the associated exponential polynomial are "eventually monotone" (fewnomial/Descartes-type arguments on the sign pattern). (verify the exact dimension bound.)
- **Hainry (2008)**: the Continuous Orbit Problem — deciding whether \(e^{At}x = y\) for some \(t \ge 0\) — is decidable for rational \(A, x, y\) in all dimensions. This is *easier* because it constrains all coordinates simultaneously, unlike the single-linear-functional Skolem question.
- **Discrete analogue**: Skolem (decidable for order ≤ 4; open from order 5, via the Poly-Rechnowitz method), and the ultimately periodic variants (Positivity is open even at order 5).
- **Hard landscape**: via the transform \(e^{At}\), the problem is equivalent to locating zeros of real exponential polynomials with algebraic data. Zero-counting for such functions can encode deep transcendence questions (Schanuel's conjecture); Macdonald's work on zeros of exponential sums guarantees at most finitely many zeros when the exponentials have distinct real parts, but gives no effective bound in general.
- Reachability for linear systems to *semialgebraic* target sets is known undecidable in some formulations and open in others (Chen, Fontoura, et al. on "reachability in low dimensions"), situating continuous Skolem as a boundary case.

## What would count as solving it?

- **Full solution**: an algorithm that, given rational \(A, x, c\), always terminates and correctly decides whether \(c^\top e^{At}x = 0\) for some \(t > 0\); or a proof of undecidability over rational inputs.
- **Partial but valuable**: (i) decidability for all dimensions under an explicit spectral condition (e.g., all eigenvalues of \(A\) real and simple); (ii) decidability for dimension \(n \le k\) for a new \(k\); (iii) unconditional decidability for the cases currently resolved only under Schanuel's conjecture; (iv) a rigorous reduction from discrete Skolem to continuous Skolem or vice versa, clarifying whether the two are interreducible (they are not known to be).
- A referee would demand full effectivity: any use of transcendence assumptions must be isolated and stated.

## How to start

1. Read Chonev–Ouaknine–Worrell (2016) first — it contains the complete reduction of the problem to zeros of exponential polynomials and the case analysis on eigenvalue multiplicity; Section on "eventual monotonicity" is where the hard cases are isolated.
2. Master the structure: diagonalize \(A\) over \(\mathbb{C}\); write \(f(t) = \sum_{i} p_i(t)e^{\lambda_i t}\) with \(\lambda_i\) algebraic; study the interaction between conjugate eigenvalue pairs and polynomial factors.
3. Try to extend the bounded-dimension decidability by one dimension, focusing on the first case where transcendence assumptions currently appear; the natural tool is effective real-analytic zero-bounding (quasi-analyticity, fewnomial-type sign-variation arguments).
4. Main obstacle: for real parts of exponentials in "bad" algebraic relations, current techniques need effective lower bounds on small values of exponential polynomials — squarely in Schanuel territory. Look for workarounds via the algebraic structure forced by \(A\) coming from a single matrix exponential.

## Key references

- V. Chonev, J. Ouaknine, J. Worrell, *On the Skolem Problem for Continuous Linear Dynamical Systems*, 2016 (LICS / journal version; identifier: verify). Establishes the exponential-polynomial formulation and decidability for restricted dimensions/spectra.
- E. Hainry, *Decidability and Equivalence of First-Order Simulability Problem*, and *The Generalized Orbit Problem...* — decidability of the continuous orbit problem \(e^{At}x = y\). (verify exact citation)
- J. Ouaknine, J. Worrell, *Positivity Problems for Low-Order Linear Recurrence Sequences* (SODA 2014): the discrete analogue's state of the art up to order 9 for Positivity. (verify)
- A. Macdonald, *Zeros of Exponential Sums* / classical results on real zeros of \(\sum p_i e^{\lambda_i t}\). (verify)

## Warnings

- The identically-zero subtlety: by real-analyticity \(f \equiv 0\) is decidable by linear algebra on the Krylov sequence \(\{c, c^\top A, c^\top A^2, \dots\}\); don't conflate this easy case with isolated zeros.
- The naive guess "continuous ⇒ easier, use quantifier elimination over the reals" fails: \(e^{At}\) is transcendental, and o-minimal tameness of \(\operatorname{DEF}\)-expansions of the reals (Wilkie) does not give decidability of zero existence with algebraic parameters.
- Dimension counting from the discrete problem: continuous Skolem is *not* known to subsume discrete Skolem, despite folklore claims; the embedding of \(\mathbb{N}\)-indexed sequences into flows requires non-rational matrices.
- Beware results stated only under Schanuel's conjecture; several papers in this area conditionalize.

---
*`ALGO-000181` · flagged for review*

## Acceptance guidance

- **Full solution**: an algorithm that, given rational \(A, x, c\), always terminates and correctly decides whether \(c^\top e^{At}x = 0\) for some \(t > 0\); or a proof of undecidability over rational inputs.
- **Partial but valuable**: (i) decidability for all dimensions under an explicit spectral condition (e.g., all eigenvalues of \(A\) real and simple); (ii) decidability for dimension \(n \le k\) for a new \(k\); (iii) unconditional decidability for the cases currently resolved only under Schanuel's conjecture; (iv) a rigorous reduction from discrete Skolem to continuous Skolem or vice versa, clarifying whether the two are interreducible (they are not known to be).
- A referee would demand full effectivity: any use of transcendence assumptions must be isolated and stated.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7b66de04-bf78-45c9-903a-5e4bc829932a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000181.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000181)
