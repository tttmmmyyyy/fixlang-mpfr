# MPFR

Defined in mpfr-fix@0.3.0

Provides arbitrary-precision floating-point type `MPFR` and related functions.

This is a wrapper for the GNU MPFR (Multiple Precision Floating-Point Reliable) Library.

## Values

### namespace MPFR

#### c_SIZE_OF_MPFR

Type: `Std::FFI::CInt`

Size of `__mpfr_struct`.
On 64-bit systems, this is typically 32 bytes.

### namespace MPFR::MPFR

#### abs

Type: `MPFR::MPFR -> MPFR::MPFR`

Absolute value of an MPFR number (exact operation).

##### Parameters

- `x`: The number to take absolute value of.

#### acos

Type: `MPFR::MPFR -> MPFR::MPFR`

Arccosine function.

##### Parameters

- `x`: The value (must be in [-1, 1]).

#### acosh

Type: `MPFR::MPFR -> MPFR::MPFR`

Inverse hyperbolic cosine function.

##### Parameters

- `x`: The value (must be >= 1).

#### add

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Add two MPFR numbers.
Uses RNDN rounding and precision is the maximum of the two operands.

##### Parameters

- `lhs`: The left-hand side operand.
- `rhs`: The right-hand side operand.

#### agm

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Arithmetic-geometric mean of two MPFR numbers.

##### Parameters

- `x`: The first number.
- `y`: The second number.

#### ai

Type: `MPFR::MPFR -> MPFR::MPFR`

Airy function Ai(x).

##### Parameters

- `x`: The value.

#### asin

Type: `MPFR::MPFR -> MPFR::MPFR`

Arcsine function.

##### Parameters

- `x`: The value (must be in [-1, 1]).

#### asinh

Type: `MPFR::MPFR -> MPFR::MPFR`

Inverse hyperbolic sine function.

##### Parameters

- `x`: The value.

#### atan

Type: `MPFR::MPFR -> MPFR::MPFR`

Arctangent function.

##### Parameters

- `x`: The value.

#### atan2

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Two-argument arctangent function (atan2).

##### Parameters

- `y`: The y coordinate.
- `x`: The x coordinate.

#### atanh

Type: `MPFR::MPFR -> MPFR::MPFR`

Inverse hyperbolic tangent function.

##### Parameters

- `x`: The value (must be in (-1, 1)).

#### beta

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Beta function: B(x, y) = Γ(x)Γ(y)/Γ(x+y).

##### Parameters

- `x`: The first parameter.
- `y`: The second parameter.

#### cbrt

Type: `MPFR::MPFR -> MPFR::MPFR`

Cube root of an MPFR number.

##### Parameters

- `x`: The number to take cube root of.

#### ceil

Type: `MPFR::MPFR -> MPFR::MPFR`

Round to the next higher integer.

##### Parameters

- `x`: The number to round up.

#### cmp

Type: `MPFR::MPFR -> MPFR::MPFR -> Std::I64`

Compare two MPFR numbers.
Returns negative if lhs < rhs, zero if lhs == rhs, positive if lhs > rhs.

##### Parameters

- `lhs`: The left-hand side number.
- `rhs`: The right-hand side number.

#### const_catalan

Type: `MPFR::Precision -> MPFR::MPFR`

Mathematical constant Catalan's constant (0.915...).

##### Parameters

- `prec`: The precision in bits.

#### const_euler

Type: `MPFR::Precision -> MPFR::MPFR`

Mathematical constant Euler's constant (0.577...).

##### Parameters

- `prec`: The precision in bits.

#### const_log2

Type: `MPFR::Precision -> MPFR::MPFR`

Mathematical constant log(2).

##### Parameters

- `prec`: The precision in bits.

#### const_pi

Type: `MPFR::Precision -> MPFR::MPFR`

Mathematical constant Pi.

##### Parameters

- `prec`: The precision in bits.

#### copysign

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Copy the sign of y to x.

##### Parameters

- `x`: The number to copy magnitude from.
- `y`: The number to copy sign from.

#### cos

Type: `MPFR::MPFR -> MPFR::MPFR`

Cosine function.

##### Parameters

- `x`: The angle in radians.

#### cosh

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic cosine function.

##### Parameters

- `x`: The value.

#### cot

Type: `MPFR::MPFR -> MPFR::MPFR`

Cotangent function: cot(x) = 1/tan(x).

##### Parameters

- `x`: The angle in radians.

#### coth

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic cotangent function: coth(x) = 1/tanh(x).

##### Parameters

- `x`: The value.

#### csc

Type: `MPFR::MPFR -> MPFR::MPFR`

Cosecant function: csc(x) = 1/sin(x).

##### Parameters

- `x`: The angle in radians.

#### csch

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic cosecant function: csch(x) = 1/sinh(x).

##### Parameters

- `x`: The value.

#### digamma

Type: `MPFR::MPFR -> MPFR::MPFR`

Digamma function (psi function): ψ(x) = Γ'(x)/Γ(x).

##### Parameters

- `x`: The value.

#### div

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Divide two MPFR numbers.
Uses RNDN rounding and precision is the maximum of the two operands.

##### Parameters

- `lhs`: The left-hand side operand (dividend).
- `rhs`: The right-hand side operand (divisor).

#### div_2si

Type: `Std::I64 -> MPFR::MPFR -> MPFR::MPFR`

Divide by 2^n where n can be negative (efficient bit shift).

##### Parameters

- `n`: The exponent (signed).
- `x`: The number to divide.

#### div_2ui

Type: `Std::U64 -> MPFR::MPFR -> MPFR::MPFR`

Divide by 2^n (efficient bit shift).

##### Parameters

- `n`: The exponent (unsigned).
- `x`: The number to divide.

#### equal

Type: `MPFR::MPFR -> MPFR::MPFR -> Std::Bool`

Check if two MPFR numbers are equal.

##### Parameters

- `lhs`: The left-hand side number.
- `rhs`: The right-hand side number.

#### erf

Type: `MPFR::MPFR -> MPFR::MPFR`

Error function.

##### Parameters

- `x`: The value.

#### erfc

Type: `MPFR::MPFR -> MPFR::MPFR`

Complementary error function.

##### Parameters

- `x`: The value.

#### exp

Type: `MPFR::MPFR -> MPFR::MPFR`

Exponential function.

##### Parameters

- `x`: The number to exponentiate.

#### exp10

Type: `MPFR::MPFR -> MPFR::MPFR`

Base-10 exponential function (10^x).

##### Parameters

- `x`: The exponent.

#### exp2

Type: `MPFR::MPFR -> MPFR::MPFR`

Base-2 exponential function (2^x).

##### Parameters

- `x`: The exponent.

#### expm1

Type: `MPFR::MPFR -> MPFR::MPFR`

exp(x) - 1, computed accurately even for small x.

##### Parameters

- `x`: The number to exponentiate.

#### fac_ui

Type: `Std::U64 -> MPFR::Precision -> MPFR::MPFR`

Factorial function: n!

##### Parameters

- `n`: The non-negative integer to compute factorial of.
- `prec`: The precision in bits.

#### floor

Type: `MPFR::MPFR -> MPFR::MPFR`

Round to the next lower integer.

##### Parameters

- `x`: The number to round down.

#### fma

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Fused multiply-add: (x * y) + z, computed with a single rounding.

##### Parameters

- `x`: The first multiplicand.
- `y`: The second multiplicand.
- `z`: The addend.

#### fmod

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Floating-point remainder: x - n*y where n is the integer quotient x/y rounded toward zero.

##### Parameters

- `x`: The dividend.
- `y`: The divisor.

#### gamma

Type: `MPFR::MPFR -> MPFR::MPFR`

Gamma function.

##### Parameters

- `x`: The value.

#### get_f64

Type: `MPFR::MPFR -> Std::F64`

Convert an MPFR value to F64.

May lose precision if the MPFR value has more precision than F64.

##### Parameters

- `x`: The MPFR number to convert.

#### get_prec

Type: `MPFR::MPFR -> MPFR::Precision`

Get the precision of an MPFR number.

##### Parameters

- `x`: The number to get precision of.

#### get_si

Type: `MPFR::MPFR -> Std::Option Std::I64`

Convert an MPFR value to I64.

Rounds toward zero. Returns none if the value doesn't fit in I64.

##### Parameters

- `x`: The MPFR number to convert.

#### get_str

Type: `Std::I64 -> Std::I64 -> MPFR::RoundMode -> MPFR::MPFR -> (Std::String, Std::I64)`

Convert an MPFR value to a string in a given base with specified number of digits.

Returns a tuple of (mantissa_string, exponent) where the mantissa is a fraction
with an implicit radix point immediately to the left of the first digit.
For example, the number -3.1416 would be returned as ("-31416", 1).

If the number is NaN, returns ("@NaN@", 0).
If the number is +Inf, returns ("@Inf@", 0).
If the number is -Inf, returns ("-@Inf@", 0).

##### Parameters

- `base`: The base of the string representation (must be in the range [2, 62] or [-36, -2]).
- `n_digits`: Number of significant digits (0 means use get_str_ndigits with the number's precision).
- `rnd`: The rounding mode to use.
- `num`: The MPFR number to convert.

#### get_str_ndigits

Type: `Std::I64 -> MPFR::Precision -> Std::I64`

Get the number of digits required to represent an MPFR value in a given base.

This function returns the minimal integer m such that any number of p bits,
when output in base b with m digits, can be recovered exactly when read back in base b.

##### Parameters

- `base`: The base (must be in the range [2, 62]).
- `prec`: The precision in bits.

#### get_ui

Type: `MPFR::MPFR -> Std::Option Std::U64`

Convert an MPFR value to U64.

Rounds toward zero. Returns none if the value doesn't fit in U64.

##### Parameters

- `x`: The MPFR number to convert.

#### hypot

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Euclidean norm: sqrt(x^2 + y^2), computed without intermediate overflow or underflow.

##### Parameters

- `x`: The first component.
- `y`: The second component.

#### inf

Type: `MPFR::Precision -> MPFR::MPFR`

Create an MPFR value representing positive infinity.

##### Parameters

- `prec`: The precision in bits.

#### is_inf

Type: `MPFR::MPFR -> Std::Bool`

Check if the value is infinite.

##### Parameters

- `x`: The number to check.

#### is_nan

Type: `MPFR::MPFR -> Std::Bool`

Check if the value is NaN.

##### Parameters

- `x`: The number to check.

#### is_number

Type: `MPFR::MPFR -> Std::Bool`

Check if the value is a regular number (not NaN, not Inf).

##### Parameters

- `x`: The number to check.

#### is_zero

Type: `MPFR::MPFR -> Std::Bool`

Check if the value is zero.

##### Parameters

- `x`: The number to check.

#### j0

Type: `MPFR::MPFR -> MPFR::MPFR`

Bessel function of the first kind of order 0.

##### Parameters

- `x`: The value.

#### j1

Type: `MPFR::MPFR -> MPFR::MPFR`

Bessel function of the first kind of order 1.

##### Parameters

- `x`: The value.

#### jn

Type: `Std::I64 -> MPFR::MPFR -> MPFR::MPFR`

Bessel function of the first kind of order n.

##### Parameters

- `n`: The order.
- `x`: The value.

#### less

Type: `MPFR::MPFR -> MPFR::MPFR -> Std::Bool`

Check if lhs < rhs.

##### Parameters

- `lhs`: The left-hand side number.
- `rhs`: The right-hand side number.

#### lesseq

Type: `MPFR::MPFR -> MPFR::MPFR -> Std::Bool`

Check if lhs <= rhs.

##### Parameters

- `lhs`: The left-hand side number.
- `rhs`: The right-hand side number.

#### lngamma

Type: `MPFR::MPFR -> MPFR::MPFR`

Natural logarithm of the absolute value of the Gamma function.

##### Parameters

- `x`: The value.

#### log

Type: `MPFR::MPFR -> MPFR::MPFR`

Natural logarithm.

##### Parameters

- `x`: The number to take logarithm of.

#### log10

Type: `MPFR::MPFR -> MPFR::MPFR`

Base-10 logarithm.

##### Parameters

- `x`: The number to take logarithm of.

#### log1p

Type: `MPFR::MPFR -> MPFR::MPFR`

log(1 + x), computed accurately even for small x.

##### Parameters

- `x`: The number to add to 1 before taking logarithm.

#### log2

Type: `MPFR::MPFR -> MPFR::MPFR`

Base-2 logarithm.

##### Parameters

- `x`: The number to take logarithm of.

#### max

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Return the maximum of two MPFR numbers.

##### Parameters

- `x`: The first number.
- `y`: The second number.

#### min

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Return the minimum of two MPFR numbers.

##### Parameters

- `x`: The first number.
- `y`: The second number.

#### mpfr

Type: `MPFR::Precision -> Std::F64 -> MPFR::MPFR`

Create an MPFR value from an F64 with specified precision.

##### Parameters

- `prec`: The precision in bits.
- `val`: The F64 value to convert.

#### mpfr_i

Type: `MPFR::Precision -> Std::I64 -> MPFR::MPFR`

Create an MPFR value from an I64 with specified precision.

##### Parameters

- `prec`: The precision in bits.
- `val`: The I64 value to convert.

#### mpfr_str

Type: `MPFR::Precision -> Std::String -> Std::I64 -> Std::Option MPFR::MPFR`

Create an MPFR value from a string with specified precision and base.

##### Parameters

- `prec`: The precision in bits.
- `str`: The string representation of the number.
- `base`: The base of the string representation (2 to 62, or 0 for auto-detection).

#### mpfr_ui

Type: `MPFR::Precision -> Std::U64 -> MPFR::MPFR`

Create an MPFR value from a U64 with specified precision.

##### Parameters

- `prec`: The precision in bits.
- `val`: The U64 value to convert.

#### mul

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Multiply two MPFR numbers.
Uses RNDN rounding and precision is the maximum of the two operands.

##### Parameters

- `lhs`: The left-hand side operand.
- `rhs`: The right-hand side operand.

#### mul_2si

Type: `Std::I64 -> MPFR::MPFR -> MPFR::MPFR`

Multiply by 2^n where n can be negative (efficient bit shift).

##### Parameters

- `n`: The exponent (signed).
- `x`: The number to multiply.

#### mul_2ui

Type: `Std::U64 -> MPFR::MPFR -> MPFR::MPFR`

Multiply by 2^n (efficient bit shift).

##### Parameters

- `n`: The exponent (unsigned).
- `x`: The number to multiply.

#### nan

Type: `MPFR::Precision -> MPFR::MPFR`

Create an MPFR value representing NaN (Not a Number).

##### Parameters

- `prec`: The precision in bits.

#### neg

Type: `MPFR::MPFR -> MPFR::MPFR`

Negate an MPFR number (exact operation).

##### Parameters

- `x`: The number to negate.

#### neg_inf

Type: `MPFR::Precision -> MPFR::MPFR`

Create an MPFR value representing negative infinity.

##### Parameters

- `prec`: The precision in bits.

#### nextabove

Type: `MPFR::MPFR -> MPFR::MPFR`

Return the next floating-point number toward +infinity.

##### Parameters

- `x`: The starting number.

#### nextbelow

Type: `MPFR::MPFR -> MPFR::MPFR`

Return the next floating-point number toward -infinity.

##### Parameters

- `x`: The starting number.

#### nexttoward

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Return the next floating-point number in the direction of y.

##### Parameters

- `x`: The starting number.
- `direction`: The direction to move toward.

#### pow

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Power function: base^exponent.

##### Parameters

- `base`: The base.
- `exponent`: The exponent.

#### pow_si

Type: `Std::I64 -> MPFR::MPFR -> MPFR::MPFR`

Power function with signed integer exponent.

##### Parameters

- `exponent`: The signed integer exponent.
- `base`: The base.

#### pow_ui

Type: `Std::U64 -> MPFR::MPFR -> MPFR::MPFR`

Power function with unsigned integer exponent.

##### Parameters

- `exponent`: The unsigned integer exponent.
- `base`: The base.

#### rec_sqrt

Type: `MPFR::MPFR -> MPFR::MPFR`

Reciprocal square root of an MPFR number.

##### Parameters

- `x`: The number to take reciprocal square root of (1/sqrt(x)).

#### remainder

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

IEEE remainder: x - n*y where n is the integer quotient x/y rounded to nearest.

##### Parameters

- `x`: The dividend.
- `y`: The divisor.

#### rootn_ui

Type: `Std::U64 -> MPFR::MPFR -> MPFR::MPFR`

N-th root of an MPFR number.

##### Parameters

- `n`: The degree of the root (must be > 0).
- `x`: The number to take n-th root of.

#### round

Type: `MPFR::MPFR -> MPFR::MPFR`

Round to the nearest integer, rounding halfway cases away from zero.

##### Parameters

- `x`: The number to round.

#### sec

Type: `MPFR::MPFR -> MPFR::MPFR`

Secant function: sec(x) = 1/cos(x).

##### Parameters

- `x`: The angle in radians.

#### sech

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic secant function: sech(x) = 1/cosh(x).

##### Parameters

- `x`: The value.

#### setsign

Type: `Std::Bool -> MPFR::MPFR -> MPFR::MPFR`

Set the sign of x according to the boolean s (false = positive, true = negative).

##### Parameters

- `sign`: The sign to set (false for positive, true for negative).
- `x`: The number to set sign of.

#### sgn

Type: `MPFR::MPFR -> Std::I64`

Get the sign of a number.
Returns negative if num < 0, zero if num == 0, positive if num > 0.

##### Parameters

- `x`: The number to get sign of.

#### signbit

Type: `MPFR::MPFR -> Std::Bool`

Test if the sign bit is set (even for NaN and zero).

##### Parameters

- `x`: The number to check sign bit of.

#### sin

Type: `MPFR::MPFR -> MPFR::MPFR`

Sine function.

##### Parameters

- `x`: The angle in radians.

#### sinh

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic sine function.

##### Parameters

- `x`: The value.

#### sqr

Type: `MPFR::MPFR -> MPFR::MPFR`

Square an MPFR number.

##### Parameters

- `x`: The number to square.

#### sqrt

Type: `MPFR::MPFR -> MPFR::MPFR`

Square root of an MPFR number.

##### Parameters

- `x`: The number to take square root of.

#### sub

Type: `MPFR::MPFR -> MPFR::MPFR -> MPFR::MPFR`

Subtract two MPFR numbers.
Uses RNDN rounding and precision is the maximum of the two operands.

##### Parameters

- `lhs`: The left-hand side operand.
- `rhs`: The right-hand side operand.

#### tan

Type: `MPFR::MPFR -> MPFR::MPFR`

Tangent function.

##### Parameters

- `x`: The angle in radians.

#### tanh

Type: `MPFR::MPFR -> MPFR::MPFR`

Hyperbolic tangent function.

##### Parameters

- `x`: The value.

#### to_string_exp

Type: `MPFR::MPFR -> Std::String`

Convert an MPFR value to exponential form string.

The output format is "d.dddd...e±exp" (e.g., "3.14159e+0", "-1.23456e-10").
The number of significant digits is determined by the number's precision.

##### Parameters

- `num`: The MPFR number to convert.

#### to_string_exp_precision

Type: `Std::U8 -> MPFR::MPFR -> Std::String`

Convert an MPFR value to exponential form string with specified precision.

The output format is "d.{prec digits}e±exp" where the number of digits after
the decimal point is exactly `prec`.

##### Parameters

- `prec`: The number of digits after the decimal point.
- `num`: The MPFR number to convert.

#### to_string_precision

Type: `Std::U8 -> MPFR::MPFR -> Std::String`

Convert an MPFR value to string with specified precision (digits after decimal point).

The output format is standard decimal notation with exactly `prec` digits after
the decimal point (e.g., "3.14", "-123.456").

##### Parameters

- `prec`: The number of digits after the decimal point.
- `num`: The MPFR number to convert.

#### trunc

Type: `MPFR::MPFR -> MPFR::MPFR`

Round to the next integer toward zero.

##### Parameters

- `x`: The number to truncate.

#### y0

Type: `MPFR::MPFR -> MPFR::MPFR`

Bessel function of the second kind of order 0.

##### Parameters

- `x`: The value.

#### y1

Type: `MPFR::MPFR -> MPFR::MPFR`

Bessel function of the second kind of order 1.

##### Parameters

- `x`: The value.

#### yn

Type: `Std::I64 -> MPFR::MPFR -> MPFR::MPFR`

Bessel function of the second kind of order n.

##### Parameters

- `n`: The order.
- `x`: The value.

#### zero

Type: `MPFR::Precision -> MPFR::MPFR`

Create an MPFR value representing zero.

##### Parameters

- `prec`: The precision in bits.

#### zeta

Type: `MPFR::MPFR -> MPFR::MPFR`

Riemann zeta function.

##### Parameters

- `x`: The value.

#### zeta_ui

Type: `Std::U64 -> MPFR::Precision -> MPFR::MPFR`

Riemann zeta function for unsigned integer argument.

##### Parameters

- `n`: The unsigned integer argument.
- `prec`: The precision in bits.

### namespace MPFR::RoundMode

#### to_c_rnd

Type: `MPFR::RoundMode -> Std::FFI::CInt`

Convert RoundMode to C integer constant.

## Types and aliases

### namespace MPFR

#### MPFR

Defined as: `type MPFR = unbox struct { ...fields... }`

Arbitrary-precision floating-point number type.

##### field `_0`

Type: `Std::FFI::Destructor MPFR::MPFRHandle`

#### MPFRHandle

Defined as: `type MPFRHandle = Std::Ptr`

A pointer to struct `__mpfr_struct`.

#### Precision

Defined as: `type Precision = Std::I64`

Precision type for MPFR numbers (in bits).

#### RoundMode

Defined as: `type RoundMode = unbox union { ...variants... }`

Rounding mode for MPFR operations.

##### variant `rndn`

Type: `()`

##### variant `rndz`

Type: `()`

##### variant `rndu`

Type: `()`

##### variant `rndd`

Type: `()`

##### variant `rnda`

Type: `()`

## Traits and aliases

## Trait implementations

### impl `MPFR::MPFR : Std::Add`

### impl `MPFR::MPFR : Std::Div`

### impl `MPFR::MPFR : Std::Eq`

### impl `MPFR::MPFR : Std::LessThan`

### impl `MPFR::MPFR : Std::LessThanOrEq`

### impl `MPFR::MPFR : Std::Mul`

### impl `MPFR::MPFR : Std::Neg`

### impl `MPFR::MPFR : Std::Sub`

### impl `MPFR::MPFR : Std::ToString`

### impl `MPFR::MPFR : Std::Zero`