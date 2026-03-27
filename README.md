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

This fork tracks `ucb-bar/berkeley-softfloat-3` directly and cherry-picks
smart-contract-specific additions from the earlier EOSIO and AntelopeIO forks
with original authorship preserved.

## Additions Over Upstream

The following changes have been applied on top of the upstream Berkeley
SoftFloat (including post-3e upstream commits for BF16 support, RISC-V
fixes, and build improvements):

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
