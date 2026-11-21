# OOP_PYTHON


```markdown
# 🐍 Python OOP Mastery — Encapsulation, Inheritance, Copy Semantics & Object Lifecycle

> A hands-on, production-grade reference repository that demonstrates Python's
> object-oriented programming concepts **with runnable code, verified output,
> and real-world design patterns** — no toy examples, no hand-waving.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Code Style: PEP8](https://img.shields.io/badge/code%20style-PEP8-brightgreen)](https://peps.python.org/pep-0008/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 📖 Table of Contents

- [Overview](#-overview)
- [What You'll Learn](#-what-youll-learn)
- [Repository Structure](#-repository-structure)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Modules Deep Dive](#-modules-deep-dive)
  - [1. Encapsulation — Bank Account System](#1-encapsulation--bank-account-system)
  - [2. Inheritance & MRO — Document Workflow Engine](#2-inheritance--mro--document-workflow-engine)
  - [3. Copy Semantics — Shallow vs Deep](#3-copy-semantics--shallow-vs-deep)
  - [4. Object Lifecycle — Constructors & Resource Management](#4-object-lifecycle--constructors--resource-management)
- [Design Patterns Demonstrated](#-design-patterns-demonstrated)
- [Running the Demos](#-running-the-demos)
- [Testing](#-testing)
- [Key Takeaways](#-key-takeaways)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## 🎯 Overview

This repository is a **curated collection of Python OOP demonstrations** built to
bridge the gap between *"I read the docs"* and *"I can design it in production."*
Every module is:

- ✅ **Runnable** — `python -m <module>` produces documented output
- ✅ **Verified** — expected outputs are included and tested
- ✅ **Idiomatic** — follows PEP 8 and Pythonic conventions
- ✅ **Real-world** — models actual domain problems (banking, document approval,
  config caching, session leases)

Whether you're preparing for interviews, teaching a workshop, or onboarding
junior engineers, this repo provides **worked examples with the "why" behind
every design decision.**

---

## 🧠 What You'll Learn

| Topic | Concepts Covered |
|-------|------------------|
| **Encapsulation** | `_protected`, `__private`, `@property`, read-only attributes, validation in setters, name mangling |
| **Inheritance** | `super()`, cooperative multiple inheritance, MRO, mixins, override vs. extend |
| **Copy Semantics** | Assignment vs. shallow vs. deep copy, `id()` proofs, cyclic references, `__copy__`/`__deepcopy__` |
| **Object Lifecycle** | `__new__` vs `__init__`, flyweight caching, `WeakValueDictionary`, context managers, `__del__` pitfalls |
| **Design Patterns** | Flyweight, Mixin, Factory Method, Context Manager, Registry |
| **Best Practices** | Immutability, idempotent cleanup, exception safety, defensive validation |

---

## 📁 Repository Structure

```
python-oop-mastery/
│
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── requirements.txt
├── pyproject.toml
│
├── src/
│   └── oop_mastery/
│       ├── __init__.py
│       ├── encapsulation/
│       │   ├── __init__.py
│       │   └── bank_account.py          # Session 1
│       ├── inheritance/
│       │   ├── __init__.py
│       │   └── document_workflow.py     # Session 2
│       ├── copy_semantics/
│       │   ├── __init__.py
│       │   └── copy_demos.py            # Session 3
│       └── lifecycle/
│           ├── __init__.py
│           └── resource_manager.py      # Session 4
│
├── examples/
│   ├── run_encapsulation.py
│   ├── run_inheritance.py
│   ├── run_copy_semantics.py
│   └── run_lifecycle.py
│
├── tests/
│   ├── test_encapsulation.py
│   ├── test_inheritance.py
│   ├── test_copy_semantics.py
│   └── test_lifecycle.py
│
└── docs/
    ├── encapsulation.md
    ├── inheritance_mro.md
    ├── copy_semantics.md
    └── object_lifecycle.md
```

---

## ⚙️ Installation

### Prerequisites

- **Python 3.10+** (uses `int | None` union syntax and `WeakValueDictionary` typing)
- No external dependencies required for core modules

### Clone & Set Up

```bash
# Clone the repository
git clone https://github.com/<your-username>/python-oop-mastery.git
cd python-oop-mastery

# Create a virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate      # Linux/macOS
# .venv\Scripts\activate       # Windows

# Install in editable mode (optional — for running tests)
pip install -e ".[dev]"
```

---

## 🚀 Quick Start

Run any module directly — each is self-contained with a `main()` demo:

```bash
# 1. Encapsulation: private attrs, properties, validation
python -m oop_mastery.encapsulation.bank_account

# 2. Inheritance: MRO, cooperative super(), mixins
python -m oop_mastery.inheritance.document_workflow

# 3. Copy semantics: shallow vs deep
python -m oop_mastery.copy_semantics.copy_demos

# 4. Object lifecycle: __new__, caching, context managers
python -m oop_mastery.lifecycle.resource_manager
```

Or via the `examples/` scripts:

```bash
python examples/run_lifecycle.py
```

---

## 🔬 Modules Deep Dive

### 1. Encapsulation — Bank Account System

**File:** `src/oop_mastery/encapsulation/bank_account.py`

Demonstrates the full encapsulation toolkit:

```python
class BankAccount:
    def __init__(self, owner: str, balance: float = 0):
        self.owner = owner
        self.__balance = balance          # private (name-mangled)

    @property
    def balance(self) -> float:           # read-only from outside
        return self.__balance

    @balance.setter
    def balance(self, value: float):      # validated setter
        if value < 0:
            raise ValueError("Balance cannot be negative")
        self.__balance = value

    def deposit(self, amount: float) -> None:
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self.__balance += amount
```

**Key ideas demonstrated:**

| Concept | Location |
|---------|----------|
| `_protected` convention | `_account_counter` |
| `__private` + name mangling | `__balance`, `__history` |
| `@property` getter / setter | `balance` |
| Read-only property | `transaction_count` |
| Immutable return (`tuple`) | `history` |
| Custom exceptions | `InsufficientFundsError` |
| Class-level state | `_account_counter` |

📄 Full walkthrough → [`docs/encapsulation.md`](docs/encapsulation.md)

---

### 2. Inheritance & MRO — Document Workflow Engine

**File:** `src/oop_mastery/inheritance/document_workflow.py`

A document-approval system that showcases **cooperative multiple inheritance**:

```python
class AuditableInvoice(AuditableMixin, TimestampMixin,
                       InvoiceDocument, Document):
    pass

# MRO:
# AuditableInvoice → AuditableMixin → TimestampMixin
#                  → InvoiceDocument → Document → object
```

**Key ideas demonstrated:**

| Concept | Location |
|---------|----------|
| Cooperative `__init__` (`**kwargs` relay) | Every class |
| Method Resolution Order | `AuditableInvoice.__mro__` |
| Override vs. extend with `super()` | `InvoiceDocument.submit` / `summary` |
| Mixins with cross-cutting concerns | `AuditableMixin`, `TimestampMixin` |
| Graceful degradation | `AuditableMixin.approve` (`getattr` fallback) |
| Domain-rule enforcement | `PolicyDocument.approve` |

**Why MRO order matters** — reorder the mixins and `super()` stops
chaining correctly, silently skipping audit hooks. The demo prints the MRO
and walks through valid + invalid transitions.

📄 Full walkthrough → [`docs/inheritance_mro.md`](docs/inheritance_mro.md)

---

### 3. Copy Semantics — Shallow vs Deep

**File:** `src/oop_mastery/copy_semantics/copy_demos.py`

A 17-question interactive exploration of `copy.copy` vs `copy.deepcopy`:

```python
import copy

original = [1, 2, [3, 4]]
assigned = original          # same object
shallow  = copy.copy(original)   # new outer, shared inner
deep     = copy.deepcopy(original)  # fully independent

original[2][0] = 999
print(assigned)   # [1, 2, [999, 4]]
print(shallow)    # [1, 2, [999, 4]]  ← leaked
print(deep)       # [1, 2, [3, 4]]    ← independent
```

**Key ideas demonstrated:**

| Concept | Location |
|---------|----------|
| Assignment vs. copy vs. deepcopy | `q1_warmup()` |
| `id()` proofs | `q2_identity()` |
| Nested-list aliasing trap (`[[0]*2]*2`) | `q3_nested_list_trap()` |
| Shallow-copy leaks in dicts/lists-of-dicts | `q4`, `q5` |
| Immutable tuples returned unchanged | `q6_tuple_semantics()` |
| Cyclic references + `memo` | `q9_cycles()` |
| Custom `__copy__` / `__deepcopy__` | `q12` |
| Performance comparison (`timeit`) | `q11_performance()` |

📄 Full walkthrough → [`docs/copy_semantics.md`](docs/copy_semantics.md)

---

### 4. Object Lifecycle — Constructors & Resource Management

**File:** `src/oop_mastery/lifecycle/resource_manager.py`

A controlled instance lifecycle manager covering `__new__` caching,
factory constructors, and deterministic cleanup:

```python
class ConfigProfile:
    _cache = weakref.WeakValueDictionary()

    def __new__(cls, environment: str, region: str, **kwargs):
        key = (environment, region)
        if (cached := cls._cache.get(key)) is not None:
            return cached                      # flyweight reuse
        instance = super().__new__(cls)
        cls._cache[key] = instance
        return instance

    def __init__(self, environment, region, timeout=30, retries=3):
        if getattr(self, "_initialized", False):
            return                             # guard against re-init
        ...
        self._initialized = True
```

```python
class SessionLease:
    @classmethod
    def from_env(cls, prefix: str, ttl_seconds: int = 60): ...
    @classmethod
    def ephemeral(cls, owner: str, ttl_seconds: int): ...

    def __enter__(self): return self.acquire()
    def __exit__(self, *exc): self.release(); return False
```

**Key ideas demonstrated:**

| Concept | Location |
|---------|----------|
| `__new__` vs `__init__` | `ConfigProfile` |
| Flyweight caching | `_cache` (WeakValueDictionary) |
| Re-init guard | `_initialized` flag |
| Factory constructors | `SessionLease.from_env` / `.ephemeral` |
| Exception-safe cleanup | `__exit__` returns `False` |
| `__del__` as last resort only | `SessionLease.__del__` (warning only) |
| Weak references prevent leaks | `weakref.WeakValueDictionary` |

📄 Full walkthrough → [`docs/object_lifecycle.md`](docs/object_lifecycle.md)

---

## 🎨 Design Patterns Demonstrated

| Pattern | Module | Purpose |
|---------|--------|---------|
| **Flyweight** | `lifecycle` | Cache `ConfigProfile` per `(env, region)` |
| **Mixin** | `inheritance` | Add `Timestamp`/`Audit` behaviour via multiple inheritance |
| **Factory Method** | `lifecycle` | `SessionLease.from_env`, `.ephemeral` |
| **Context Manager** | `lifecycle` | Deterministic `with`-block cleanup |
| **Registry** | `inheritance` | Implicit — MRO-based method dispatch |
| **Template Method** | `inheritance` | `Document.submit` overridden by subclasses |

---

## 🏃 Running the Demos

Each module prints a **structured, annotated walkthrough** of its concepts:

```bash
$ python -m oop_mastery.lifecycle.resource_manager

======================================================================
PART A: ConfigProfile flyweight cache
======================================================================
[__new__] ALLOCATING new ConfigProfile for ('prod', 'us-east')
[__init__] INITIALIZED (prod, us-east, timeout=45)
[__new__] REUSED cached ConfigProfile for ('prod', 'us-east')
[__init__] SKIPPED (already initialized) for (prod, us-east)
...
[__del__] WARNING: lease 'forgotten-7f3e...' was still active at GC
```

Every module's **expected output is documented inline** and validated by
the test suite.

---

## 🧪 Testing

Run the full test suite:

```bash
# Install dev dependencies first
pip install -e ".[dev]"

# Run all tests
pytest -v

# With coverage
pytest --cov=oop_mastery --cov-report=term-missing

# Single module
pytest tests/test_lifecycle.py -v
```

**Coverage targets:**

- ✅ Every public class has at least one happy-path test
- ✅ Every validation branch has a negative test
- ✅ MRO and `id()` assertions are explicit (not implicit)
- ✅ Context-manager cleanup verified under exceptions
- ✅ `WeakValueDictionary` eviction verified via `gc.collect()`

---

## 💡 Key Takeaways

After working through this repo, you should be able to:

1. **Encapsulate** state with `_`/`__` conventions, `@property`, and validation
   — and explain *why* Python doesn't enforce privacy at the compiler level.
2. **Design mixin hierarchies** where `super()` cooperates cleanly across
   `__init__`, `submit`, and `approve` — and predict MRO without running it.
3. **Choose between shallow and deep copy** — and prove the difference with
   `id()`, not by trial-and-error.
4. **Control instance creation** with `__new__` + flyweight caching, using
   `WeakValueDictionary` so the cache doesn't leak.
5. **Guarantee resource cleanup** with `with` — and explain why `__del__`
   is *not* a reliable substitute.

---

## 🗺️ Roadmap

- [x] Encapsulation (properties, validation, name mangling)
- [x] Inheritance & MRO (cooperative mixins, super())
- [x] Copy semantics (shallow vs deep, `__copy__`/`__deepcopy__`)
- [x] Object lifecycle (`__new__`, context managers, weakrefs)
- [ ] Polymorphism & Abstract Base Classes (`abc`, `Protocol`)
- [ ] Descriptors (data vs non-data, `__set_name__`)
- [ ] `__slots__` & memory footprint
- [ ] Metaclasses (`type`, `__init_subclass__`)
- [ ] Serialization (`pickle`, `__reduce__`)
- [ ] Thread-safe object pools (`threading.Lock`)

---

## 🤝 Contributing

Contributions are welcome! Please read [`CONTRIBUTING.md`](CONTRIBUTING.md)
first. In short:

1. Fork the repo and create a feature branch: `git checkout -b feat/abc-protocols`
2. Add the module **and** tests. Every demo must have documented expected output.
3. Run `pytest` and `ruff check .` before opening a PR.
4. Keep examples **self-contained** — no external services or network calls.

### Style Guide

- PEP 8, 88-char line limit (Black-compatible)
- Type hints required for all public functions
- Docstrings in Google style
- No bare `except:` — always catch specific exceptions

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.

```
MIT License

Copyright (c) 2026 <Your Name>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 🙏 Acknowledgments

- **Python Language Reference** — [Data Model](https://docs.python.org/3/reference/datamodel.html)
- **`copy` module docs** — [shallow vs deep copy](https://docs.python.org/3/library/copy.html)
- **`weakref` module docs** — [weak references](https://docs.python.org/3/library/weakref.html)
- **PEP 8** & **PEP 484** — style & typing
- The Python community's endless patience with `super()` questions 🙃

---

<p align="center">
  <b>⭐ If this repo helped you understand OOP better, star it!</b><br>
  <sub>Built with 🐍 and a healthy respect for MRO.</sub>
</p>
```

---


```
