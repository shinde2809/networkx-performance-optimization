# Performance Optimization of NetworkX Betweenness Centrality

## Repository
networkx/networkx

## Baseline Commit
510674456f7ac4016051bc3a34c99e319d242cea
---

## 🔍 Problem

Betweenness centrality computation in NetworkX is slow for large graphs due to its pure Python implementation of Brandes' algorithm.

We identified this as a hot path by observing long execution times for graphs with ~2000 nodes.

---

## ⚡ Optimization

Replaced the Python implementation with:

- CSR (Compressed Sparse Row) graph representation
- Numba-accelerated implementation of Brandes algorithm

This reduces Python overhead and leverages compiled execution.

---

## 🚀 Results

| Version     | Median Time |
|------------|------------|
| Baseline   | 28.418717861175537 sec      |
| Candidate  | 0.8331713676452637 sec      |

**Speedup: ~34x**

---

## ✅ Correctness

- Outputs match baseline using `np.allclose`
- Tolerance: `1e-6` (floating point differences)
- Existing tests: preserved

---

## ⚖️ Trade-offs

- Increased code complexity
- Requires Numba dependency
- Less flexible than pure Python version

---

## 🔮 Future Work

- Parallelization across sources
- GPU acceleration
- Sparse optimizations for very large graphs

---

## 🧪 Notes

- All results reproducible via Colab notebooks
- Same graph + same environment used for fair comparison
