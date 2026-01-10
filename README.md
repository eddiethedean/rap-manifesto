# rap-manifesto

**Philosophy, guarantees, and benchmarks for Real Async Python.**

---

## What is RAP?

RAP (Real Async Python) is an ecosystem of Python packages backed by native runtimes (primarily Rust) that provide **provably non-blocking, GIL-independent async I/O**. RAP exists to correct widespread misuse of the term "async" in Python by defining async behavior **by measurable outcomes**, not syntax.

---

## Core Principles

### 1. Behavioral Async
- Async is defined by concurrency under contention.
- Passing the Fake Async Detector is mandatory.
- Syntax alone is insufficient.

### 2. GIL Independence
- All heavy I/O executes outside the Python GIL.
- No reliance on Python thread pools.
- True parallelism, not cooperative multitasking.

### 3. Native First
- Rust is the default implementation language.
- Python is a thin orchestration layer.
- Direct syscalls where possible.

### 4. Falsifiable Claims
- Every performance claim must be benchmarked.
- Benchmarks are public, reproducible, and documented.
- Benchmarks decide disputes.

---

## The RAP Prefix

Packages prefixed with **`rap`** stand for **Real Async Python**. This is a contract, not marketing:

- **`rapfiles`** — True async filesystem I/O
- **`rapsqlite`** — True async SQLite
- **`rapcsv`** — Streaming async CSV
- **`rap-bench`** — Fake Async Detector CLI

If a package bears the `rap` prefix, it guarantees:
- Measurable concurrency under load
- Real parallelism (GIL-independent)
- Verifiable async behavior via benchmarks

---

## What RAP Is Not

- ❌ Not "async syntax with threads"
- ❌ Not compatibility-first
- ❌ Not magic performance dust
- ❌ Not cooperative yielding masquerading as async

---

## Benchmarks

Benchmarks are available in the `rap-bench` repository. All RAP packages must pass the Fake Async Detector, which:

1. Launches 1 blocking or slow task
2. Launches 100–1000 concurrent I/O tasks
3. Measures throughput, p50/p95 latency, and event loop stall gaps

**Pass Criteria:**
- No collapse in unrelated task progress
- Stable latency under contention
- Zero event loop stalls

---

## Repositories

| Repo | Purpose |
|------|---------|
| [rap-manifesto](https://github.com/rap-project/rap-manifesto) | Philosophy, guarantees, benchmarks |
| [rap-bench](https://github.com/rap-project/rap-bench) | Fake Async Detector CLI |
| [rapfiles](https://github.com/rap-project/rapfiles) | True async filesystem I/O |
| [rapsqlite](https://github.com/rap-project/rapsqlite) | True async SQLite |
| [rapcsv](https://github.com/rap-project/rapcsv) | Streaming async CSV |

---

## License

MIT

