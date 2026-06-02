# thermodynamics

Thermodynamics in Rust. Carnot cycles to entropy.

A crate implementing classical and statistical thermodynamics from first principles. Covers the four laws, ideal and van der Waals gases, Carnot cycles, entropy (Clausius, Boltzmann, Gibbs), Maxwell relations, phase transitions, partition functions, and heat transfer.

## Install

```toml
[dependencies]
thermodynamics = "0.1"
```

Requires Rust **2021 edition**. Depends on `serde` and `nalgebra`.

## Quick Start

```rust
use thermodynamics::*;

// The four laws
assert!(zeroth_law_equilibrium(&[300.0, 300.0, 300.0], 0.1));
let delta_u = first_law(1000.0, 400.0); // ΔU = Q − W
assert!(is_spontaneous(5.0));
assert_eq!(third_law_entropy(0.0, true), 0.0);

// Ideal gas: PV = nRT
let p = ideal_gas_pressure(1.0, 300.0, 0.0249);
let v = ideal_gas_volume(1.0, 300.0, 101325.0);

// Carnot cycle
let cycle = CarnotCycle::new(600.0, 300.0, 1000.0);
assert_eq!(cycle.efficiency, 0.5);

// Entropy
let ds = clausius_entropy_change(1000.0, 300.0);
let s_boltz = boltzmann_entropy(1e10);
let s_gibbs = gibbs_entropy(&[0.25, 0.25, 0.25, 0.25]);

// Statistical mechanics
let z = canonical_partition_function(&[0.0, 1e-21, 2e-21], 300.0);
let u = partition_function_energy(&[0.0, 1e-21, 2e-21], 300.0);
let a = helmholtz_from_partition(z, 300.0);
```

## Modules

| Module | What It Gives You |
|---|---|
| `constants` | R, k_B, N_A, σ, atm, temperature conversions |
| `laws` | All four laws, heat capacities for monatomic & diatomic ideal gases |
| `gas` | Ideal gas law, van der Waals equation, compressibility factor |
| `carnot` | Carnot efficiency, work, COP for refrigerators & heat pumps |
| `entropy` | Clausius, Boltzmann, Gibbs entropy, mixing, phase transitions |
| `maxwell` | All four Maxwell relations, thermodynamic potential derivatives |
| `phase` | Clausius–Clapeyron, boiling point vs pressure, phase rule |
| `statistical` | Partition functions, Fermi–Dirac & Bose–Einstein distributions |
| `heat_transfer` | Conduction, convection, radiation, Biot & Fourier numbers |
| `agent_budget` | Compute energy budgets with Landauer's principle |

76 tests covering every formula against known values.

```bash
cargo test
```

## License

MIT OR Apache-2.0
