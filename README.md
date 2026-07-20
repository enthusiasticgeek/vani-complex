# vani-complex

Complex number library for the [vāṇी compiler](https://github.com/enthusiasticgeek/vani-compiler).

`Complex` is a plain `{ re: f64, im: f64 }` struct with no heap-owning fields, so it's
freely copyable -- no `ref`/`mut ref` ceremony anywhere in this API, unlike the
`Vec<f64>`-based sibling libraries ([vani-matrix](https://github.com/enthusiasticgeek/vani-matrix),
[vani-calculus](https://github.com/enthusiasticgeek/vani-calculus)).

## Add to your project

```toml
# vani.toml
[deps]
complex = { registry = "kosh", version = "^0.1" }
```

```sh
vanic add complex
vanic build
```

## What's included (v0.1.0 — complete; see TODO.md)

| Module | Functions |
|---|---|
| Construction | `complex_new`, `complex_conj`, `complex_neg` |
| Arithmetic | `complex_add`, `complex_sub`, `complex_mul`, `complex_div`, `complex_scale`, `complex_reciprocal`, `complex_norm_sq` |
| Modulus / polar | `complex_abs`, `complex_arg`, `complex_from_polar` |
| Exponential / power | `complex_exp`, `complex_log`, `complex_pow_i64`, `complex_sqrt` |
| Trig / hyperbolic | `complex_sin`, `complex_cos`, `complex_tan`, `complex_sinh`, `complex_cosh`, `complex_tanh` |
| Roots of unity | `complex_nth_roots_of_unity` |

## Encoding

```
struct Complex { re: f64, im: f64 }
```

`Vec<Complex>` works directly (structs without heap-owning fields nest into `Vec<T>`
with no special handling needed) -- see `complex_nth_roots_of_unity`, which returns one.

## What this library does NOT provide

These are already vāṇी compiler builtins — call them directly, no import needed:

`sin` `cos` `tan` `sinh` `cosh` `tanh` `atan2` `exp` `log` `sqrt` `abs`
`f64_pi()` `f64_hypot(x, y)`

## License

MIT
