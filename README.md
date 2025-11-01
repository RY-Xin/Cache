# Cache System (C++17, CMake, Benchmark Project)

> This project is a **reproduction and extension** of the open-source *KamaCache*.  
> It adds an independent **CMake build system**, **benchmark analysis**, and **clean English documentation** for clarity and research purposes.

---

## Project Overview

This project implements a thread-safe cache system using multiple page replacement strategies, including:

- **LRU (Least Recently Used)** – removes the least recently accessed entries.  
- **LFU (Least Frequently Used)** – removes the least frequently accessed entries.  
- **ARC (Adaptive Replacement Cache)** – dynamically balances between recency and frequency.  

Additionally, several optimizations are applied to enhance performance and cache hit rate for LRU and LFU variants.

---

## Optimization Highlights

### LRU Optimizations
- **LRU Sharding** – improves performance in multi-threaded and high-concurrency scenarios.  
- **LRU-K** – prevents cache pollution by avoiding eviction of frequently accessed “hot” data due to recent “cold” data bursts.

### LFU Optimizations
- **LFU Sharding** – parallelized LFU segments to reduce contention under concurrent access.  
- **LFU-Aging** – introduces frequency decay over time to prevent stale hot data from occupying cache indefinitely.

---

## Benchmark Results

This project benchmarks all cache strategies under three simulated access patterns:  
**Hotspot**, **Cyclic Scan**, and **Dynamic Workload**.

| Test Scenario | LRU | LFU | ARC | LRU-K | LFU-Aging |
|----------------|------|------|------|--------|------------|
| **Hot Data Access** | 49.6% | 66.8% | 65.7% | 55.0% | 66.9% |
| **Cyclic Scan** | 4.6% | 8.9% | 9.7% | 4.8% | 8.9% |
| **Dynamic Workload** | 55.1% | 37.4% | 58.8% | 54.5% | 37.7% |

**Observations**
- **ARC** delivers the most balanced performance, adapting well to changing workloads.  
- **LFU** achieves the highest hit rate in stable hot data scenarios.  
- **LRU-K** provides more stable hit rates in fluctuating workloads.

---

## Build & Run

### Build the project
```bash
mkdir build && cd build
cmake ..
make
````

### Run benchmark tests

```bash
./testAllCachePolicy
```

### Clean build artifacts

```bash
make clean
```

---

## Project Structure

```
Cache/
├── KArcCache/              # ARC algorithm implementation
├── KICachePolicy.h         # Common cache interface
├── KLfuCache.h             # LFU and LFU-Aging implementations
├── KLruCache.h             # LRU and LRU-K implementations
├── testAllCachePolicy.cpp  # Benchmark test runner
├── CMakeLists.txt          # Build configuration
└── README.md               # Documentation (this file)
```

---

## Learning & Takeaways

Through this project, I:

* Implemented five cache replacement algorithms using **C++17 STL containers**
* Built a modular **CMake-based build system**
* Designed a benchmarking framework to test hit rates across workloads
* Compared algorithm performance and analyzed trade-offs between recency and frequency

---

## Future Improvements

* Add **thread-safe cache** with mutex locks or atomic operations
* Implement **TTL (Time-To-Live)** and expiration policies
* Visualize results using **Python/Matplotlib**
* Integrate **real-world access traces** for further analysis

---

## Author

**Remi (Xinhui Yu)**
Graduate Student @ Stevens Institute of Technology
[GitHub Profile](https://github.com/RemiYu)

---

## License

MIT License © 2025 Remi Yu
Based on the open-source *KamaCache* project for educational and benchmarking purposes.

````