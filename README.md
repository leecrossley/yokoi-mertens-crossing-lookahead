# From the first dip to the first negative average

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24412165.svg)](https://doi.org/10.5281/zenodo.24412165)

This result is now maintained in [quadratic-mertens-first-crossings](https://github.com/leecrossley/quadratic-mertens-first-crossings/tree/main/results/yokoi-mertens-crossing-lookahead). This repository is archived and keeps its releases and DOI.

In the quadratic field with discriminant **82,864,613**, the prime-ideal Mertens product first falls below its expected value at **7.00521788…**. Start a running average of its logarithmic error at 2 and it stays positive until **1011.53408514…**. Both endpoints are certified to eight decimal places. The example is illustrative: its ratio $\log(W/S)/\sqrt{\log S}$ is about 3.56. [Example and checks](example.py) · [Output](evidence/example.txt)

Write $S$ for the first dip and $W$ for the first endpoint where the accumulated error from 2 becomes negative. In Yokoi fields with $W$ finite and $S$ tending to infinity, the smallest possible limiting value of $\log(W/S)/\sqrt{\log S}$ is exactly $\sqrt{2A_\ast}$. The constant $A_\ast$ is the minimum amount of positive error a product can accumulate while it stays above its benchmark indefinitely. A family of finite splitting patterns approaches the sharp coefficient in genuine fields. [Proof of the sharp waiting time](PROOF.md) · [Definition of the constant](https://github.com/leecrossley/mertens-power-average-deadlines/blob/v1.0.0/SLOW-WEIGHTS.md)

For every sufficiently large Yokoi discriminant $d$ for which some decreasing average from 2 is negative, the first crossing satisfies

$$
S\le(\log d)^2\exp(-1.965\sqrt{\log\log d}).
$$

The proof gives every coefficient below $2\sqrt{2A_\ast}$ in place of $1.965$. In the other direction, every sufficiently large discriminant shell contains at least $D^{1/2-o(1)}$ fields whose first dip is as late as $(\log D)\exp(-\kappa\sqrt{\log\log D})$ for any fixed $\kappa>2\sqrt{A_\ast}$. Even in those fields an entire interval of slowly decaying power weights gives a negative integral starting at 2. Whether every sufficiently large Yokoi field has a successful start bounded by a fixed power of its discriminant remains open. [Upper estimate](PROOF.md) · [Construction and count](FAMILY.md) · [Literature](PRIOR-WORK.md)

## Verification

Run the following from the release directory with Python 3.10 or later. The calculation encloses the residue by the quadratic theta integral, recovers the integer class number and integrates every prime-ideal norm window through the first negative endpoint. A direct formula for the integral checks the accumulated window calculation at every endpoint. Concavity on each gap excludes any earlier negative integral.

~~~sh
python3 -m pip install -r requirements.txt
shasum -a 256 -c SHA256SUMS
python3 -B example.py
~~~

The exact area identities and the numerical coefficient comparison were checked in Lean 4.33.1. The family theorems have written proofs. Set NOTE to the absolute release directory and run the command from the [pinned Mathlib checkout](https://github.com/leanprover-community/mathlib4/tree/0df444a360eaa60ab8c11dca51a86af692955474).

~~~sh
lake env lean -R "$NOTE" "$NOTE/Lookahead.lean"
~~~

[Lean source](Lookahead.lean) · [Kernel output](evidence/lean.txt)
