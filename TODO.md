# vani-complex — TODO

> Compiler builtins that already exist and must NOT be reimplemented:
> `sin` `cos` `tan` `sinh` `cosh` `tanh` `atan2` `exp` `log` `sqrt` `abs`
> `f64_pi()` `f64_hypot(x, y)`

---

## v0.1.0 — Implemented ✓

### Construction and accessors (3 functions)
- [x] `complex_new`, `complex_conj`, `complex_neg`

### Arithmetic (7 functions)
- [x] `complex_add`, `complex_sub`, `complex_mul`, `complex_div`
- [x] `complex_scale`, `complex_reciprocal`, `complex_norm_sq`

### Modulus, argument, polar form (3 functions)
- [x] `complex_abs` (via `f64_hypot`, overflow/underflow-safe), `complex_arg`, `complex_from_polar`

### Exponential, logarithm, powers (4 functions)
- [x] `complex_exp`, `complex_log`, `complex_pow_i64` (positive/negative/zero), `complex_sqrt`

### Trigonometric and hyperbolic functions (6 functions)
- [x] `complex_sin`, `complex_cos`, `complex_tan`
- [x] `complex_sinh`, `complex_cosh`, `complex_tanh`

### Roots of unity (1 function)
- [x] `complex_nth_roots_of_unity`

### Tests and examples
- [x] `tests/test_arithmetic.vani` — construction, all arithmetic ops, reciprocal identity
- [x] `tests/test_polar_exp.vani` — abs/arg/polar roundtrip, Euler's identity, log∘exp
      roundtrip, sqrt (including sqrt²=z), integer powers (positive/negative/zero),
      roots of unity (exact values + modulus-1 check for n=6)
- [x] `tests/test_trig.vani` — special values at `i`, real-axis agreement with the real
      builtins, sin²+cos²=1 and cosh²−sinh²=1 identities for a general complex z
- [x] `examples/euler_demo.vani` — Euler's identity, 6th roots of unity, a Mandelbrot
      escape-time check (pure `complex_mul`/`complex_add`/`complex_abs`, no other
      library needed)

### Safety annotations
- [x] `#[bounded_stack(bytes=N)]` on all 24 functions, budgets set to `vanic check`'s
      exact reported worst-case (not hand estimates -- struct-valued functions needed
      noticeably larger budgets than the flat-`Vec<f64>` functions in vani-matrix/
      vani-calculus/vani-probability, e.g. `complex_pow_i64` at 440 bytes)

---

## Future

`Complex` is designed to be reused directly by [vani-signal](https://github.com/enthusiasticgeek/kosh-index/blob/main/ROADMAP.md)
(FFT/DFT need a complex-valued sequence type) once that repo starts -- no changes
anticipated here to support it. No v0.2.0 is currently planned; extend this file if a
concrete need shows up (e.g. complex polynomial root-finding, complex matrices).
