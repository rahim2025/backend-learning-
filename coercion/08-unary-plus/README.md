# Unary Plus

Unary plus performs numeric coercion.

| Expression | Result |
| --- | --- |
| `+""` | `0` |
| `+" "` | `0` |
| `+[]` | `0` |
| `+{}` | `NaN` |
| `+"5"` | `5` |

It is similar to `Number(value)`, but `Number(value)` is usually clearer in backend validation code.

