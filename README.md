# berkeley-softfloat-3 — SoftFloat for WASM Smart Contracts

[![Build & Test](https://github.com/AnvoIO/berkeley-softfloat-3/actions/workflows/build.yaml/badge.svg)](https://github.com/AnvoIO/berkeley-softfloat-3/actions/workflows/build.yaml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![License: BSD-3-Clause](https://img.shields.io/badge/License-BSD--3--Clause-orange.svg)](COPYING.txt)

A fork of [Berkeley SoftFloat Release 3e](http://www.jhauser.us/arithmetic/SoftFloat.html)
for the Anvo Network Contract Development Toolkit (CDT).

## Upstream

**[ucb-bar/berkeley-softfloat-3](https://github.com/ucb-bar/berkeley-softfloat-3)** —
the canonical GitHub mirror of John R. Hauser's Berkeley SoftFloat library,
maintained by the UC Berkeley Architecture Research group.

This fork is based on the current upstream `master` (post-Release 3e) and
cherry-picks smart-contract-specific additions from the earlier EOSIO and
AntelopeIO forks with original authorship preserved. The previous
AntelopeIO-based fork was pinned to Release 3e (January 2018) and had
fallen years behind upstream.

## Upstream Improvements Over Release 3e

By forking from the current upstream rather than the stale AntelopeIO fork,
this repository includes 19 upstream commits that were never picked up by
the EOSIO or AntelopeIO forks:

- **BF16 (bfloat16) support** — new `bfloat16_t` type and conversion functions
- **RISC-V build support** — `Linux-RISCV64-GCC` build target and specialization fixes
- **ARM bug fix** — corrected `softfloat_propagateNaNF128M` for ARM-VFPv2-defaultNaN
- **`exceptionflags` enumeration** — added typedef for exception flags
- **CC override** — allows compiler override for RISC-V builds

## CDT-Specific Additions

The following changes have been applied on top of the upstream Berkeley
SoftFloat:

| Change | Author | Origin |
|--------|--------|--------|
| CMake build system + C++ header (`softfloat.hpp`) | Bucky Kittinger | EOSIO |
| `f128` to `extFloat80` conversion | Bucky Kittinger | EOSIO |
| `isNaN` for `float128_t` | Bucky Kittinger | EOSIO |
| `float64_t` / `float128_t` comparison operators | arhag | EOSIO |
| Helper functions (sign bit, NaN checks, infinity constants) | arhag | EOSIO |
| Correct `+/-` infinity representations for `float64_t` | arhag | EOSIO |
| Strict-aliasing cleanup (type punning warnings) | Matt Witherspoon | EOSIO |
| CMake install component support | Matt Witherspoon | AntelopeIO |
| Unused-label warning fix | Lin Huang | AntelopeIO |
| `__builtin_memcpy` for WASM build compatibility | Robert Capps | Anvo Network |

## Usage

This library is used as a git submodule by [CDT](https://github.com/AnvoIO/cdt).
It is not intended for standalone use.

```bash
# As part of CDT build:
git submodule update --init libraries/native/softfloat
```

## Documentation

The original SoftFloat package documentation is in the `doc/` subdirectory:

* [SoftFloat.html](http://www.jhauser.us/arithmetic/SoftFloat-3/doc/SoftFloat.html) — Using the SoftFloat functions
* [SoftFloat-source.html](http://www.jhauser.us/arithmetic/SoftFloat-3/doc/SoftFloat-source.html) — Building SoftFloat
* [SoftFloat-history.html](http://www.jhauser.us/arithmetic/SoftFloat-3/doc/SoftFloat-history.html) — History of major changes

## License

The original Berkeley SoftFloat library is licensed under the BSD-3-Clause
license. See [COPYING.txt](COPYING.txt).

Additions by EOSIO, AntelopeIO, and Anvo Network contributors are licensed
under the MIT license. See [LICENSE](LICENSE).
