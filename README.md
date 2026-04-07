# BEM Frequency-Domain Solver

Linear wave-body interaction solver using the Boundary Element Method (BEM)
in the frequency domain, with Quadratic Transfer Function (QTF) computation.

## Features

- First-order hydrodynamic coefficients (added mass, damping, wave excitation)
- Second-order Quadratic Transfer Functions (QTF)
- FMM-accelerated BIE solver
- Multi-body support
- JSON-based input files

## Build

Requires: C++23 compiler (GCC 12+ or Clang 16+), CMake 3.16+, LAPACK/BLAS.

```bash
mkdir build && cd build
cmake ..
make -j$(sysctl -n hw.logicalcpu)    # macOS
make -j$(nproc)                       # Linux
```

### CMake Options

| Option | Default | Description |
|--------|---------|-------------|
| `BEM_COMPILER` | `gcc` | `gcc` or `clang` |
| `USE_TETGEN` | `ON` | TetGen tetrahedralization (AGPL-3.0) |
| `FMM_M2L_METHOD` | `SimpleM2L` | FMM M2L translation method |
| `BEM_ENABLE_OPENMP` | `ON` | OpenMP parallelization |

## Usage

```bash
./main_freq_domain path/to/settings.json
```

## Directory Structure

```
├── lib/                  # Shared library (mesh, FMM, geometry)
│   ├── include/          # Header files
│   └── src/              # Source files
├── bem/
│   ├── core/             # BEM common (BVP solver, boundary conditions)
│   └── frequency_domain/ # Frequency-domain solver and QTF
└── third_party/tetgen/   # TetGen (optional, AGPL-3.0)
```

## Related Packages

- [BEM_TimeDomain](https://github.com/tomoakihirakawa/BEM_TimeDomain) — Time-domain nonlinear BEM
- [CableDynamics](https://github.com/tomoakihirakawa/CableDynamics) — Mooring line dynamics
- [BEM_for_Nonlinear_Waves](https://github.com/tomoakihirakawa/BEM_for_Nonlinear_Waves) — Integrated repository

## License

LGPL-3.0-or-later. See [LICENSE](LICENSE).

TetGen (optional) is licensed under AGPL-3.0. See `third_party/tetgen/LICENSE`.
