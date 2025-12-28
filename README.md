# Project Shokunin: Reliable Systems Journey

> **Mission:** To engineer a mathematically verified Instant Payment System (SPI) from first principles.
> **Philosophy:** Moving beyond "it works" to "it cannot fail".

## 📜 The Manifesto
This is not a tutorial on distributed systems. This is a rigorous engineering log documenting the construction of critical financial infrastructure over the course of 12+ months.
Each module includes modeling notes documenting non-obvious insights uncovered through formal specification and verification.

Unlike standard roadmaps, this project prioritizes **correctness over velocity**. Every line of code is grounded in:
1.  **Academic Whitepapers:** Implementing algorithms from primary sources (Paxos, Raft, LMAX).
2.  **Formal Verification:** Using TLA+ to co-evolve specifications and code, treating correctness as a property to be proven.
3.  **Business Logic Integrity:** Treating financial rules as invariant laws, not just requirements.

## 🗺️ The Roadmap (From Zero to Criticality)

### Phase 1: The Mathematical Foundation & Internals
*Goal: To deconstruct Go's concurrency primitives, prove key correctness properties with TLA+, and rebuild them from scratch to master the memory model.*

#### Module 1.1: Data Structures (State Management)
*Focus: Pointer manipulation and circular buffers.*
- [ ] **Circular Buffer (Ring):**
    - *Go Implementation:* Recreate `container/ring` focusing on memory efficiency.
    - *Formal Verification:* Prove in TLA+ that the buffer never overwrites unread data without permission.
- [ ] **Doubly Linked List:**
    - *Go Implementation:* Recreate `container/list`.
    - *Formal Verification:* Prove invariant consistency (next.prev must always equal current).

#### Module 1.2: Synchronization Primitives (The "Sync" Package)
*Focus: Managing shared memory access safely.*
- [ ] **The Mutex:**
    - *Go Implementation:* Build a Mutual Exclusion lock using only `atomic` flags (CAS).
    - *Formal Verification:* Prove **Safety** (only one process enters critical section) and **Liveness** (no deadlocks).
- [ ] **Weighted Semaphore:**
    - *Go Implementation:* Build a semaphore to limit concurrent access (Rate Limiting base).
    - *Formal Verification:* Prove resource bound invariants.

#### Module 1.3: Concurrency Patterns (Communication)
*Focus: "Do not communicate by sharing memory; share memory by communicating."*
- [ ] **Channels from Scratch:**
    - *Go Implementation:* Rebuild Go's `chan` using a Ring Buffer + Mutex + CondVars.
    - *Formal Verification:* Model the Blocking/Unblocking behavior of senders and receivers (Producer-Consumer problem).

---
*Tech Stack: Go, TLA+, Linux Internals.*
*Status: Initialization*
