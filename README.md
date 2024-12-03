# anita
Anita is a JIT compiler that allows runtime compilation of expressions in the format of [evalexpr](https://github.com/ISibboI/evalexpr).

## Usage
Anita compiles a given expression and returns a structure with a function that follows a given signature. This can be achieved by using the `compile_expression!` macro.
```rust
let function = compile_expression!("x+1", (x) -> f32);
assert_eq!(function.execute(4_f32), 5_f32);
```

## Supported features
This is the current status of evalexpr features in anita
### Types
So far anita only supports floats and uses implicit casts for function calls.
Type | Status |
|----------|------------|
| f32 | supported |
| f64 | planned |
| bool | planned |
| i32 | unsupported |
| i64 | unsupported |
| String | unsupported |
| Tupel | unsupported |

### Operators
Operator | Status | Description |
|----------|------------|-------------|
| ^ | work in progress | Exponentiation |
| * | supported | Product |
| / | supported | Division |
| % | work in progress | Modulo |
| + | supported | Sum |
| - | supported | Difference |
| < | planned | Lower than |
| \> | planned | Greater than |
| <= | planned | Lower than or equal |
| \>= | planned | Greater than or equal |
| == | planned | Equal |
| != | planned | Not equal |
| && | planned | Logical and |
| &#124;&#124; | planned | Logical or |
| = | supported | Assignment |
| += | planned | Sum-Assignment or String-Concatenation-Assignment |
| -= | planned | Difference-Assignment |
| *= | planned | Product-Assignment |
| /= | planned | Division-Assignment |
| %= | planned | Modulo-Assignment |
| ^= | planned | Exponentiation-Assignment |
| &&= | planned | Logical-And-Assignment |
| &#124;&#124;= | planned | Logical-Or-Assignment |
| , | unsupported | Aggregation |
| ; | supported | Expression Chaining |
| - (unary) | supported | Negation |
| ! | unsupported | Logical not |

### Functions
| Identifier           | Status      | Argument Amount | Argument Types                | Description |
|----------------------|-------------|-----------------|-------------------------------|-------------|
| `min`                | planned     | 2            | Numeric                       | Returns the minimum of the arguments |
| `max`                | planned     | 2            | Numeric                       | Returns the maximum of the arguments |
| `len`                | unsupported | 1               | String/Tuple                  | Returns the character length of a string, or the amount of elements in a tuple (not recursively) |
| `floor`              | planned     | 1               | Numeric                       | Returns the largest integer less than or equal to a number |
| `round`              | planned     | 1               | Numeric                       | Returns the nearest integer to a number. Rounds half-way cases away from 0.0 |
| `ceil`               | planned     | 1               | Numeric                       | Returns the smallest integer greater than or equal to a number |
| `if`                 | planned     | 3               | Boolean, Any, Any             | If the first argument is true, returns the second argument, otherwise, returns the third  |
| `contains`           | unsupported | 2               | Tuple, any non-tuple          | Returns true if second argument exists in first tuple argument. |
| `contains_any`       | unsupported | 2               | Tuple, Tuple of any non-tuple | Returns true if one of the values in the second tuple argument exists in first tuple argument. |
| `typeof`             | unsupported | 1               | Any                           | returns "string", "float", "int", "boolean", "tuple", or "empty" depending on the type of the argument  |
| `is_nan`       | planned     | 1               | Numeric                       | Returns true if the argument is the floating-point value NaN, false if it is another floating-point value, and throws an error if it is not a number  |
| `is_finite`    | planned     | 1               | Numeric                       | Returns true if the argument is a finite floating-point number, false otherwise  |
| `is_infinite`  | planned     | 1               | Numeric                       | Returns true if the argument is an infinite floating-point number, false otherwise  |
| `is_normal`    | planned     | 1               | Numeric                       | Returns true if the argument is a floating-point number that is neither zero, infinite, [subnormal](https://en.wikipedia.org/wiki/Subnormal_number), or NaN, false otherwise  |
| `ln`           | planned     | 1               | Numeric                       | Returns the natural logarithm of the number |
| `log`          | planned     | 2               | Numeric, Numeric              | Returns the logarithm of the number with respect to an arbitrary base |
| `log2`         | planned     | 1               | Numeric                       | Returns the base 2 logarithm of the number |
| `log10`        | planned     | 1               | Numeric                       | Returns the base 10 logarithm of the number |
| `exp`          | planned     | 1               | Numeric                       | Returns `e^(number)`, (the exponential function) |
| `exp2`         | planned     | 1               | Numeric                       | Returns `2^(number)` |
| `pow`          | planned     | 2               | Numeric, Numeric              | Raises a number to the power of the other number |
| `cos`          | planned     | 1               | Numeric                       | Computes the cosine of a number (in radians) |
| `acos`         | planned     | 1               | Numeric                       | Computes the arccosine of a number. The return value is in radians in the range [0, pi] or NaN if the number is outside the range [-1, 1] |
| `cosh`         | planned     | 1               | Numeric                       | Hyperbolic cosine function |
| `acosh`        | planned     | 1               | Numeric                       | Inverse hyperbolic cosine function |
| `sin`          | planned     | 1               | Numeric                       | Computes the sine of a number (in radians) |
| `asin`         | planned     | 1               | Numeric                       | Computes the arcsine of a number. The return value is in radians in the range [-pi/2, pi/2] or NaN if the number is outside the range [-1, 1] |
| `sinh`         | planned     | 1               | Numeric                       | Hyperbolic sine function |
| `asinh`        | planned     | 1               | Numeric                       | Inverse hyperbolic sine function |
| `tan`          | planned     | 1               | Numeric                       | Computes the tangent of a number (in radians) |
| `atan`         | planned     | 1               | Numeric                       | Computes the arctangent of a number. The return value is in radians in the range [-pi/2, pi/2] |
| `atan2`        | planned     | 2               | Numeric, Numeric              | Computes the four quadrant arctangent in radians |
| `tanh`         | planned     | 1               | Numeric                       | Hyperbolic tangent function |
| `atanh`        | planned     | 1               | Numeric                       | Inverse hyperbolic tangent function. |
| `sqrt`         | planned     | 1               | Numeric                       | Returns the square root of a number. Returns NaN for a negative number |
| `cbrt`         | planned     | 1               | Numeric                       | Returns the cube root of a number |
| `hypot`        | planned     | 2               | Numeric                       | Calculates the length of the hypotenuse of a right-angle triangle given legs of length given by the two arguments |
| `abs`          | planned     | 1               | Numeric                       | Returns the absolute value of a number, returning an integer if the argument was an integer, and a float otherwise |
| `str::regex_matches` | unsupported | 2               | String, String                | Returns true if the first argument matches the regex in the second argument (Requires `regex_support` feature flag) |
| `str::regex_replace` | unsupported | 3               | String, String, String        | Returns the first argument with all matches of the regex in the second argument replaced by the third argument (Requires `regex_support` feature flag) |
| `str::to_lowercase`  | unsupported | 1               | String                        | Returns the lower-case version of the string |
| `str::to_uppercase`  | unsupported | 1               | String                        | Returns the upper-case version of the string |
| `str::trim`          | unsupported | 1               | String                        | Strips whitespace from the start and the end of the string |
| `str::from`          | unsupported | >= 0            | Any                           | Returns passed value as string |
| `str::substring`     | unsupported | 3               | String, Int, Int              | Returns a substring of the first argument, starting at the second argument and ending at the third argument. If the last argument is omitted, the substring extends to the end of the string |
| `bitand`             | unsupported | 2               | Int                           | Computes the bitwise and of the given integers |
| `bitor`              | unsupported | 2               | Int                           | Computes the bitwise or of the given integers |
| `bitxor`             | unsupported | 2               | Int                           | Computes the bitwise xor of the given integers |
| `bitnot`             | unsupported | 1               | Int                           | Computes the bitwise not of the given integer |
| `shl`                | unsupported | 2               | Int                           | Computes the given integer bitwise shifted left by the other given integer |
| `shr`                | unsupported | 2               | Int                           | Computes the given integer bitwise shifted right by the other given integer |
| `random`             | unsupported | 0               | Empty                         | Return a random float between 0 and 1. Requires the `rand` feature flag. |
### Other features
Evalexpr allows the declaration of new variables. This is supported using anita but all used variables have to either be mentioned in the function signature or used with the assignment operator before being read to avoid the use of uninitialized variables.

## SIMD
TODO!

## Naming
The name anita is inspired by the first all-electronic desktop calculator [Anita](<https://en.wikipedia.org/wiki/Sumlock_ANITA_calculator>)