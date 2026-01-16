# rap-manifesto

**Philosophy, guarantees, and benchmarks for Real Async Python.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## What is RAP?

RAP (Real Async Python) is an ecosystem of Python packages backed by native runtimes (primarily Rust) that provide **provably non-blocking, GIL-independent async I/O**. RAP exists to correct widespread misuse of the term "async" in Python by defining async behavior **by measurable outcomes**, not syntax.

## The Problem: Fake Async

Many popular Python "async" libraries like `aiofiles`, `aiocsv`, and `aiosqlite` use `async`/`await` syntax but aren't truly async. They wrap blocking I/O operations in thread pools, which means:

- Your event loop can still stall under load
- I/O operations still block threads, just in a pool
- It's async syntax, not async behavior
- Performance degrades under contention

RAP provides true async alternatives that execute I/O operations **outside the Python GIL** using native async runtimes (Rust + Tokio), ensuring your event loop never stalls, even under heavy load.

## Core Principles

### 1. Behavioral Async
- Async is defined by **concurrency under contention**.
- Passing the **Fake Async Detector** is mandatory.
- Syntax alone is insufficient.

### 2. GIL Independence
- All heavy I/O executes **outside the Python GIL**.
- No reliance on Python thread pools.
- **True parallelism**, not cooperative multitasking.

### 3. Native First
- **Rust** is the default implementation language.
- **Python** is a thin orchestration layer.
- **Direct syscalls** where possible.

### 4. Falsifiable Claims
- Every performance claim must be **benchmarked**.
- Benchmarks are **public, reproducible, and documented**.
- Benchmarks **decide disputes**.

## The RAP Prefix

Packages prefixed with **`rap`** stand for **Real Async Python**. This is a **contract**, not marketing:

| Package | Purpose | Status | Goal |
|---------|---------|--------|------|
| **[rapfiles](https://github.com/eddiethedean/rapfiles)** | True async filesystem I/O | ✅ Phase 1 Complete (v0.1.1) | Drop-in replacement for `aiofiles` |
| **[rapsqlite](https://github.com/eddiethedean/rapsqlite)** | True async SQLite | ✅ Phase 1 Complete (v0.1.1) | Drop-in replacement for `aiosqlite` |
| **[rapcsv](https://github.com/eddiethedean/rapcsv)** | Streaming async CSV | ✅ Phase 1 Complete (v0.1.1) | Drop-in replacement for `aiocsv` |
| **[rap-bench](https://github.com/eddiethedean/rap-bench)** | Fake Async Detector CLI | ✅ Available | Benchmarking tool |

**Current Status**: All RAP packages have completed Phase 1 (v0.1.1) with core functionality stable and production-ready. All packages support Python 3.8 through 3.13 and are verified to pass the Fake Async Detector. We're actively working toward full drop-in compatibility with their `aio*` equivalents. See each package's README for current status, limitations, and ROADMAP for planned improvements.

If a package bears the `rap` prefix, it guarantees:
- ✅ **Measurable concurrency** under load
- ✅ **Real parallelism** (GIL-independent)
- ✅ **Verifiable async behavior** via benchmarks

## What RAP Is Not

- ❌ **Not** "async syntax with threads"
- ❌ **Not** compatibility-first
- ❌ **Not** magic performance dust
- ❌ **Not** cooperative yielding masquerading as async

## Benchmarks

Benchmarks are available in the [rap-bench](https://github.com/eddiethedean/rap-bench) repository. All RAP packages must pass the **Fake Async Detector**, which:

1. Launches **1 blocking or slow task**
2. Launches **100–1000 concurrent I/O tasks**
3. Measures **throughput, p50/p95 latency, and event loop stall gaps**

**Pass Criteria:**
- ✅ No collapse in unrelated task progress
- ✅ Stable latency under contention
- ✅ Zero event loop stalls

### Running the Detector

```bash
pip install rap-bench
rap-bench detect rapfiles
rap-bench detect rapsqlite
rap-bench detect rapcsv
```

## Repository Structure

| Repository | Purpose | PyPI Package |
|------------|---------|--------------|
| [rap-manifesto](https://github.com/eddiethedean/rap-manifesto) | Philosophy, guarantees, benchmarks | N/A |
| [rap-bench](https://github.com/eddiethedean/rap-bench) | Fake Async Detector CLI | [`rap-bench`](https://pypi.org/project/rap-bench/) |
| [rapfiles](https://github.com/eddiethedean/rapfiles) | True async filesystem I/O | [`rapfiles`](https://pypi.org/project/rapfiles/) |
| [rapsqlite](https://github.com/eddiethedean/rapsqlite) | True async SQLite | [`rapsqlite`](https://pypi.org/project/rapsqlite/) |
| [rapcsv](https://github.com/eddiethedean/rapcsv) | Streaming async CSV | [`rapcsv`](https://pypi.org/project/rapcsv/) |

## Quick Start

Install any RAP package:

```bash
pip install rapfiles rapsqlite rapcsv
```

Run the Fake Async Detector:

```bash
pip install rap-bench
rap-bench list
rap-bench detect rapfiles
```

## Vision & Roadmap

Our goal is to provide true async alternatives to popular Python async libraries, starting with:

- **rapfiles** → `aiofiles` alternative
- **rapsqlite** → `aiosqlite` alternative  
- **rapcsv** → `aiocsv` alternative

Each package follows a phased development approach, with the ultimate goal of achieving drop-in replacement compatibility while providing provably superior async performance. We're building this ecosystem with a focus on:

1. **Credibility** - Proving true async behavior through benchmarks
2. **Compatibility** - Enabling seamless migration from existing libraries
3. **Performance** - Delivering measurable improvements under load

See each package's ROADMAP for detailed development plans.

## Contributing

Contributions to the RAP ecosystem are welcome! This is a young project with big ambitions, and we'd love to have you join us on this journey. Each repository has its own contributing guidelines:

- [rapfiles](https://github.com/eddiethedean/rapfiles)
- [rapsqlite](https://github.com/eddiethedean/rapsqlite)
- [rapcsv](https://github.com/eddiethedean/rapcsv)
- [rap-bench](https://github.com/eddiethedean/rap-bench)

## License

MIT

---

**RAP**: Real Async Python. Not fake async. Not cooperative multitasking. **True async.**

