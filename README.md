# rap-manifesto

**Philosophy, guarantees, and benchmarks for Real Async Python.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## What is RAP?

RAP (Real Async Python) is an ecosystem of Python packages backed by native runtimes (primarily Rust) that provide **provably non-blocking, GIL-independent async I/O**. RAP exists to correct widespread misuse of the term "async" in Python by defining async behavior **by measurable outcomes**, not syntax.

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

| Package | Purpose | Status |
|---------|---------|--------|
| **[rapfiles](https://github.com/eddiethedean/rapfiles)** | True async filesystem I/O | ✅ Available |
| **[rapsqlite](https://github.com/eddiethedean/rapsqlite)** | True async SQLite | ✅ Available |
| **[rapcsv](https://github.com/eddiethedean/rapcsv)** | Streaming async CSV | ✅ Available |
| **[rap-bench](https://github.com/eddiethedean/rap-bench)** | Fake Async Detector CLI | ✅ Available |

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

## Contributing

Contributions to the RAP ecosystem are welcome! Each repository has its own contributing guidelines:

- [rapfiles](https://github.com/eddiethedean/rapfiles)
- [rapsqlite](https://github.com/eddiethedean/rapsqlite)
- [rapcsv](https://github.com/eddiethedean/rapcsv)
- [rap-bench](https://github.com/eddiethedean/rap-bench)

## License

MIT

---

**RAP**: Real Async Python. Not fake async. Not cooperative multitasking. **True async.**

