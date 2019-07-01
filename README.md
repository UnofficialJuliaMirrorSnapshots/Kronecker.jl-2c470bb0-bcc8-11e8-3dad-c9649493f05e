# Kronecker.jl

This is a Julia package to efficiently work with Kronecker products. It combines lazy evaluation and algebraic tricks such that it can implicitely work with huge matrices. It allows to work with large Kronecker systems both much faster and using much less memory than the naive implementation of the Kronecker product.

## Features

Given two two matrices (subtype of `AbstractArray`) `A` and `B`, one can construct an instance of the `KroneckerProduct` type as `K = A ⊗ B` (typed using `\otimes TAB`). Several functions are implemented.

- `collect(K)` computes the Kronecker product (**not** recommended!)
- `tr`, `det`, `size`, `eltype`, `inv` ... are efficient functions to work with Kronecker products
- multiplying with a vector `v` is efficient using the [vec trick](https://en.wikipedia.org/wiki/Kronecker_product#Matrix_equations): `K * v`
- solving systems of the form `A ⊗ B + D`, with `D` a diagonal matrix
- working with incomplete systems using the [sampled vec trick](https://arxiv.org/pdf/1601.01507.pdf)
- [in progress] compatibility with higher-order Kronecker systems
- [in progress] GPU compatibility!
- [in progress] autodiff for machine learning models!

For basic use, see the [Jupyter notebook](notebooks/Benchmark.ipynb) with examples. It mainly compares `Kronecker.jl` with Julia's native `kron` function.

## Example

```julialang
using Kronecker

A = randn(100, 100);
B = rand(50, 50);

v = rand(5000);

K = A ⊗ B

collect(K)  # equivalent with kron(A, B)

K[78, 43]

tr(K)
inv(K)  # yields another lazy Kronecker instance

K * v  # equivalent with vec(B * reshape(v, 50, 100) * A')
```

See the notebook for some more advanced use.

## Installation

Directly available via the Julia package manager:

```julialang
] add Kronecker
```

## Issues

This is very much a work in progress! Please start an issue for bugs or requests to improve functionality. Any feedback is appreciated!