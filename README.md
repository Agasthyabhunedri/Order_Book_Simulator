# Order Book Simulator (C++20) — Concurrency Ready

A fast, deterministic **order book + matching engine** simulator with **CSV/JSON** event parsing. Built in modern C++ with clean separation between:
- **Core engine** (single-threaded, deterministic)
- **Multi-threaded pipeline** (parser → sharder → N matchers → writer)
- **Multi-process pipeline** using shared memory rings

## Why this design?
- **Determinism first:** same input ⇒ same trades/snapshots across ST/MT/MP.
- **Scale when needed:** turn on MT or MP with flags, no core changes.
- **Performance:** lock-free rings, per-symbol FIFO, minimal allocations.

---

## Build (CMake)

### Prerequisites
- CMake ≥ 3.22
- C++20 compiler: Clang ≥ 15 / GCC ≥ 11 / MSVC 2022
- (Optional) Conan for dependencies (Catch2, Google Benchmark)

### Configure & build
```bash
# Debug
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j

