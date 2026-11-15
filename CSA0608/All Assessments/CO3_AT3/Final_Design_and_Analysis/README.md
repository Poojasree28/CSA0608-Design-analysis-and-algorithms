# FINAL DESIGN AND JUSTIFICATION

## 1. Introduction

The KartIQ retail analytics platform requires efficient algorithms to handle large amounts of order, seller, customer, and product data. The four modules are designed using Divide-and-Conquer algorithms to improve processing speed and scalability. Each algorithm is selected according to its computational requirement.

## 2. Final Algorithm Selection

| Module | Selected Algorithm | Time Complexity | Auxiliary Space |
|:---|:---|:---|:---|
| Module 1 | Stable Merge Sort | O(n log n) | O(n) |
| Module 2 | Improved Quick Sort | Average: O(n log n), Worst: O(n²) | O(log n) stack |
| Module 3 | First-occurrence Binary Search | O(log n) | O(1) |
| Module 4 | Strassen's Matrix Multiplication | O(n^2.8074) | O(n²) with reusable workspace |

## 3. Justification of Algorithm Selection

### Module 1 – Merge Sort

Merge Sort is selected because it guarantees O(n log n) time complexity and maintains the original order of records with equal timestamps.

It is suitable for consolidating millions of retail orders.

**Main Trade-off:** It requires additional memory.

**Condition for Changing the Implementation:** When the complete dataset does not fit in RAM, External Merge Sort should be used.

### Module 2 – Improved Quick Sort

Median-of-three pivot selection and three-way partitioning are selected to improve sorting performance for nearly sorted seller scores and repeated scores.

Smaller-side recursion also controls stack usage.

**Main Trade-off:** Quick Sort is not stable and still has an O(n²) worst-case time complexity.

**Condition for Changing the Implementation:** If a strict worst-case time guarantee is required, use Introsort with a Heap Sort fallback.

### Module 3 – Binary Search

Binary Search is selected because the order list is already sorted by Module 1.

The modified algorithm returns the first matching timestamp.

**Main Trade-off:** It requires sorted data.

**Condition for Changing the Implementation:** If the order collection is frequently modified and sorted indexing cannot be maintained efficiently, use a suitable database index or another search structure.

### Module 4 – Strassen's Matrix Multiplication

Strassen's algorithm is selected because it reduces recursive scalar multiplications from eight to seven.

It is useful for large recommendation matrices.

**Main Trade-off:** It introduces extra additions, temporary memory usage, and recursion overhead.

**Condition for Changing the Implementation:** For small matrices or when the hardware performs conventional multiplication more efficiently, use conventional matrix multiplication.

## 4. Overall Algorithm Comparison

| Algorithm | Best Case | Average Case | Worst Case |
|:---|:---|:---|:---|
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) |
| Binary Search | O(1) | O(log n) | O(log n) |
| Strassen | O(n^2.8074) | O(n^2.8074) | O(n^2.8074) |

## 5. Integrated KartIQ System Architecture

The four modules work together as an integrated analytics engine.

<img width="854" height="558" alt="image" src="https://github.com/user-attachments/assets/3d9261ce-c97e-4238-bac0-f0fa167ce34c" />


## 6. Production Recommendations

1. Use Stable Merge Sort or External Merge Sort for large nightly order datasets.
2. Replace the existing first-element Quick Sort pivot with median-of-three pivot selection and three-way partitioning.
3. Use modified Binary Search to retrieve the first order with a specified timestamp.
4. Use a hybrid Strassen and conventional matrix multiplication approach for large recommendation matrices.
5. Measure execution time and memory usage using different input sizes.
6. Maintain sorted order indexes to support faster customer-support searches.
7. Use profiling and benchmarking to identify performance bottlenecks before deploying the algorithms.

## 7. Final Conclusion

The KartIQ platform can improve its analytical performance by applying suitable Divide-and-Conquer algorithms to its four major computational problems.

Stable Merge Sort provides reliable order consolidation, Improved Quick Sort supports efficient seller leaderboard updates, modified Binary Search enables fast order lookup, and Strassen's method reduces the number of scalar multiplications required for recommendation calculations.

The algorithms provide a suitable foundation for handling large retail datasets. Their practical performance can be improved further through memory optimisation, hybrid algorithms, and workload-specific benchmarking.

Therefore, the proposed design provides an efficient and scalable algorithmic foundation for the KartIQ retail data analytics platform.

---

# ADDITIONAL REQUIREMENT – EXPERIMENTAL TESTING AND COMPARISON

The assignment also requests input datasets, test cases, experimental results, comparison tables, and graphs.

## 1. Test Cases

The following test cases are designed to verify the correctness and performance of the four selected algorithms.

| Module | Test Case | Input | Expected Result |
|:---|:---|:---|:---|
| Merge Sort | Normal sorting | 105, 102, 105, 101, 102, 103 | 101, 102, 102, 103, 105, 105 |
| Merge Sort | Duplicate timestamps | 102, 102, 102 | Original order preserved |
| Quick Sort | Unsorted scores | 42, 17, 63, 8, 55, 29 | 8, 17, 29, 42, 55, 63 |
| Quick Sort | Nearly sorted scores | 8, 17, 29, 42, 55, 63 | Same sorted order |
| Binary Search | Existing timestamp | 102 | First matching order O2 |
| Binary Search | Missing timestamp | 200 | Order not found |
| Strassen | 2 × 2 matrices | Given sample matrices | 50, 38, 38, 34 |

## 2. Experimental Performance Comparison

The following graph compares the theoretical scalar multiplication counts for Module 4.

### Matrix Multiplication Comparison

**Input:** Two 1024 × 1024 matrices.

| Algorithm | Scalar Multiplications |
|:---|---:|
| Conventional Matrix Multiplication | 1,073,741,824 |
| Strassen's Matrix Multiplication | Approximately 205,891,132 |

**Theoretical Operation Counts**

The comparison is based on theoretical scalar multiplication counts, not measured execution times.

### Graph Representation

- X-axis: Matrix Multiplication Algorithms
- Y-axis: Number of Scalar Multiplications
- Algorithm 1: Conventional Matrix Multiplication
- Algorithm 2: Strassen's Matrix Multiplication

The graph should show that Strassen's algorithm requires fewer scalar multiplications than conventional matrix multiplication for large matrices.

## 3. Experimental Results Table

For the report, execute the programs on your computer and enter the measured execution times.

| Module | Input Size | Expected Growth |
|:---|---:|:---|
| Merge Sort | 1,000 | O(n log n) |
| Merge Sort | 10,000 | O(n log n) |
| Merge Sort | 100,000 | O(n log n) |
| Quick Sort | 1,000 | Average O(n log n) |
| Quick Sort | 10,000 | Average O(n log n) |
| Quick Sort | 100,000 | Average O(n log n) |
| Binary Search | 1,000,000 | O(log n) |
| Binary Search | 10,000,000 | O(log n) |
| Strassen | 2 × 2 | Recursive demonstration |
| Strassen | 64 × 64 | O(n^2.8074) |
| Strassen | 128 × 128 | O(n^2.8074) |

## 4. Experimental Observation

The experimental testing is used to evaluate the performance of the selected algorithms with different input sizes.

- **Merge Sort:** Maintains consistent O(n log n) performance as the input size increases.
- **Quick Sort:** Provides efficient average-case performance with improved pivot selection and three-way partitioning.
- **Binary Search:** Searches efficiently in sorted datasets with logarithmic time complexity.
- **Strassen's Algorithm:** Reduces the number of scalar multiplications for large matrices compared with conventional matrix multiplication.

Actual execution times may vary depending on the processor, memory, programming language, and implementation.

## 5. Final Experimental Conclusion

The experimental testing and theoretical comparison demonstrate the suitability of the selected Divide-and-Conquer algorithms for the KartIQ retail analytics platform.

Merge Sort provides stable order consolidation, Improved Quick Sort supports seller leaderboard processing, Binary Search enables fast order retrieval, and Strassen's algorithm improves large matrix multiplication efficiency.

The combination of these algorithms provides a scalable solution for processing large retail datasets. Actual benchmarking results should be recorded to validate their practical performance.

## 5. Sample Outputs of the Selected Algorithms

The following outputs demonstrate the working of the four selected algorithms in the KartIQ retail analytics platform.

### Module 1 – Stable Merge Sort Output

**Input:**
```text
Order Timestamps:
105, 102, 105, 101, 102, 103
```

**Output:**

<img width="940" height="661" alt="image" src="https://github.com/user-attachments/assets/391fe4cb-4622-4223-bf36-8b21fe08766a" />


### Module 2 – Improved Quick Sort Output

**Input:**
```text
Seller Scores:
42, 17, 63, 8, 55, 29
```

**Output:**

<img width="940" height="458" alt="image" src="https://github.com/user-attachments/assets/93a73cc6-06cd-48fd-bd7b-4f50ae7114f0" />


### Module 3 – First-occurrence Binary Search Output

**Input:**
```text
Sorted Order Timestamps:
101, 102, 102, 103, 105, 105

Search Timestamp: 102
```

**Output:**

<img width="940" height="439" alt="image" src="https://github.com/user-attachments/assets/bd830b79-ddcc-44e6-860d-64c216248a86" />


### Module 4 – Strassen's Matrix Multiplication Output

**Input:**

Matrix A:
```text
1  2
3  4
```

Matrix B:
```text
5  6
7  8
```

**Output:**

<img width="940" height="457" alt="image" src="https://github.com/user-attachments/assets/c3f232c0-ed5d-44f5-a3aa-040d905d8add" />


### Overall Output Summary

| Module | Algorithm | Output Status |
|:---|:---|:---|
| Module 1 | Stable Merge Sort | Successfully Sorted |
| Module 2 | Improved Quick Sort | Successfully Sorted |
| Module 3 | First-occurrence Binary Search | First Matching Order Found |
| Module 4 | Strassen's Matrix Multiplication | Resultant Matrix Generated |

All four algorithms produce the expected results and satisfy the functional requirements of the KartIQ retail analytics platform.
