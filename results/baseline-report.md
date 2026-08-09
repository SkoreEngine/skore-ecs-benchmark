# skore-ecs-benchmark baseline (APX-63)

Baseline reproduction of the published Skore-vs-Flecs comparison on this
machine. No engine or benchmark code changes were made; this is a measurement
snapshot to anchor later optimization work.

## Commands

```sh
git submodule update --init thirdparty/skore
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build -j4
./build/bin/skore_ecs_benchmark --out results/comparison.md
```

CMake defaults already force `CMAKE_BUILD_TYPE=Release` when unset; it is set
explicitly here. Release flags as configured: `-O3 -DNDEBUG`. No sanitizers.

## Versions

| Component | Version / commit |
| --- | --- |
| skore-ecs-benchmark | `fab3352` (HEAD of default branch) |
| Skore (submodule `thirdparty/skore`) | `abe525aa6f3bc96c4e02523c67b4630698ad23f3` (tag `0.0.1-alpha-77-gabe525a`, branch v2) |
| Flecs | 4.1.6 (vendored single-file amalgamation) |
| Compiler | g++ (Ubuntu 13.3.0-6ubuntu2~24.04.1) 13.3.0 |
| CMake | 3.30.5 |
| Ninja | 1.11.1 |
| Build type | Release (`-O3 -DNDEBUG`) |

## Hardware notes

- CPU: AMD EPYC Processor (with IBPB), 1 socket x 4 cores, 1 thread/core (4 vCPU)
- RAM: 7.8 GiB total, ~5.4 GiB available
- OS: Linux 6.8.0-137-generic (Ubuntu 24.04.1, x86_64)

Single-socket EPYC with only 4 cores; absolute times are not comparable to a
beefy desktop, but the Skore/flecs ratio per scenario is the signal we care
about.

## Run configuration

- entities per scenario: 100000
- warm-up runs: 2
- timed runs: 5
- query/system iterations per timed run: 100
- result file: `results/comparison.md` (regenerated each run)
- sanity checksum (all suites): 47369306390000 (stable across runs 2-4)

## Raw results (final run)

| scenario | skore_avg(s) | flecs_avg(s) | skore/flecs | skore_ops/s | flecs_ops/s |
| --- | ---: | ---: | ---: | ---: | ---: |
| create_entities | 0.164452 | 0.0078132 | 21.048x | 608079 | 1.27988e+07 |
| destroy_entities | 0.0173988 | 0.00181049 | 9.60996x | 5.74754e+06 | 5.52336e+07 |
| add_component | 0.167365 | 0.00671589 | 24.9208x | 597495 | 1.489e+07 |
| remove_component | 0.112912 | 0.00593189 | 19.0347x | 885646 | 1.6858e+07 |
| iterate_position | 0.00689724 | 0.00608349 | 1.13376x | 1.44986e+09 | 1.64379e+09 |
| iterate_position_velocity | 0.00960977 | 0.00679602 | 1.41403x | 1.04061e+09 | 1.47145e+09 |
| system_update | 0.00737107 | 0.00670893 | 1.09869x | 1.35666e+09 | 1.49055e+09 |
| deferred_spawn | 0.174152 | 0.0125477 | 13.8792x | 574212 | 7.96961e+06 |

## Ratio across 4 full runs (variance check)

| scenario | run1 | run2 | run3 | run4 (final) |
| --- | ---: | ---: | ---: | ---: |
| create_entities | 18.59x | 15.51x | 17.97x | 21.05x |
| destroy_entities | 6.07x | 6.34x | 9.24x | 9.61x |
| add_component | 23.32x | 22.65x | 31.77x | 24.92x |
| remove_component | 16.38x | 18.45x | 18.06x | 19.03x |
| iterate_position | 1.00x | 1.16x | 1.18x | 1.13x |
| iterate_position_velocity | 1.13x | 1.31x | 1.16x | 1.41x |
| system_update | 1.12x | 1.28x | 0.93x | 1.10x |
| deferred_spawn | 13.53x | 14.84x | 13.77x | 13.88x |

## Interpretation

- The reported ~10x gap is **confirmed for structural scenarios**: Skore is
  ~6-32x slower on create/destroy/add/remove/deferred-spawn. Add/remove
  component and create are the worst (~15-32x).
- **Iteration scenarios are already comparable** (~1.0-1.4x), so the gap is not
  in query/iteration hotspots; it lives in entity/component structural
  operations (spawn, add/remove component, deferred command apply).
- Structural runs are noisy (best/worst spread large, driven by allocator /
  first-touch page faults); ratios are stable enough to rank scenarios.

Next step (APX-64): profile Skore ECS spawn / add / remove / command-apply
paths to locate the structural-operation hotspots.
