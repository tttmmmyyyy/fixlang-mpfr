# MPFR Wrapper for Fix

This is a wrapper for the GNU MPFR (Multiple Precision Floating-Point Reliable) Library written in the Fix language.

It's currently verified to work with MPFR 4.1.0.

To use this library, you must have MPFR and GMP installed and be able to dynamically link to them using the `-lmpfr -lgmp` flags.

## Overview

MPFR provides arbitrary-precision floating-point arithmetic with well-defined rounding modes and precise semantics. This wrapper makes MPFR functionality available in Fix with a functional programming style.

## Naming Conventions

Most Fix functions are named by dropping the MPFR prefix (e.g., `mpfr_`) and are placed within the `MPFR::` namespace.

Due to Fix's allowed naming conventions, some functions deviate from this rule.

## Key Design Decisions

### Precision Management

Unlike MPFR's C API which has a global default precision, this wrapper **requires explicit precision specification** for all constructors. This makes the code more functional and explicit.

```fix
let x = MPFR::mpfr(113, 42);  // Create MPFR with 113-bit precision, value 42
```

### Rounding Modes

All arithmetic operations use explicit rounding modes. The default rounding mode is RNDN (round to nearest, ties to even). For trait implementations (Add, Sub, Mul, Div), RNDN is used with precision set to the maximum of the two operands.

```fix
let z = x + y;  // Uses RNDN rounding, precision is max(x.prec, y.prec)
```

For explicit control over rounding:

```fix
let z = MPFR::add_with_rnd(x, y, RoundMode::rndu());  // Round toward +∞
```

## Features

- **Arbitrary precision floating-point arithmetic**: Set precision to any valid bit count
- **Multiple rounding modes**: RNDN (nearest), RNDZ (toward zero), RNDU (toward +∞), RNDD (toward -∞), RNDA (away from zero)
- **Rich mathematical functions**: Trigonometric, exponential, logarithmic, special functions, and more
- **Type conversions**: Convert to/from I64, F64, String, MPZ, MPQ
- **Functional style**: Immutable data structures with automatic memory management
- **Trait implementations**: Zero, Add, Sub, Mul, Div, Neg, Eq, LessThan, ToString

## Installation

1. Install MPFR and GMP:
   ```bash
   # On Debian/Ubuntu:
   sudo apt-get install libmpfr-dev libgmp-dev
   
   # On macOS:
   brew install mpfr gmp
   ```

2. Clone this repository and use it as a Fix dependency.

## Usage Example

```fix
module Main;

import MPFR;

main : IO ();
main = (
    // Create MPFR numbers with 113-bit precision
    let x = MPFR::mpfr(113, 2);
    let y = MPFR::mpfr(113, 3);
    
    // Arithmetic operations
    let sum = x + y;
    let product = x * y;
    let quotient = x / y;
    
    // Mathematical functions
    let sqrt_2 = MPFR::sqrt(x);
    let pi = MPFR::const_pi(113);
    let sin_pi = MPFR::sin(pi);
    
    // String conversion
    println(sum.to_string);;
    println(pi.to_string)
);
```

## Testing

Run tests with:

```bash
fix test
```

Tests use valgrind for memory leak detection.

## Documentation

Generate documentation with:

```bash
fix docs
```

Documentation will be generated in the `docs/` directory.

## License

MIT License - see LICENSE file for details.

## References

- [MPFR Homepage](https://www.mpfr.org/)
- [MPFR Documentation](https://www.mpfr.org/mpfr-current/mpfr.html)
- [Fix Language](https://github.com/tttmmmyyyy/fixlang)
