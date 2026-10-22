# TASK 10 – COMPARE THEORY WITH EXPERIMENTAL BEHAVIOUR 

## 10.1 Introduction

Theoretical analysis predicts the time complexity of an algorithm, whereas experimental analysis measures its actual execution time and number of comparisons. Comparing both analyses helps determine whether the observed performance agrees with the theoretical predictions.

The three algorithms considered are Linear Search, Iterative Binary Search, and Recursive Binary Search.

## 10.2 Comparison of Theoretical and Experimental Behaviour

### 1. Linear Search

**Theoretical Behaviour:**

Linear Search has a best-case time complexity of O(1) and an average- and worst-case time complexity of O(n). In the worst case, it examines every registration number until the key is found or the list ends.

**Experimental Behaviour:**

The experimental results show that the number of comparisons increases with the dataset size. For an absent key, Linear Search performs n comparisons. Therefore, increasing the dataset from 1,000 to 1,000,000 records increases the comparisons from 1,000 to 1,000,000.

**Comparison:**

The experimental comparison counts agree with the theoretical prediction of linear growth. Execution time also generally increases with input size, although actual measurements may fluctuate.

### 2. Iterative Binary Search

**Theoretical Behaviour:**

Iterative Binary Search has a best-case time complexity of O(1) and an average- and worst-case time complexity of O(log n). It repeatedly divides the sorted search interval into two halves.

**Experimental Behaviour:**

The measured comparison counts increase slowly as the dataset size grows. For a dataset containing 1,000,000 records, the algorithm needs approximately 20 iterations in the worst case under balanced-halving analysis.

**Comparison:**

The experimental results support the theoretical prediction of logarithmic growth. Iterative Binary Search is more scalable than Linear Search when the registration numbers are sorted.

### 3. Recursive Binary Search

**Theoretical Behaviour:**

Recursive Binary Search has a best-case time complexity of O(1) and an average- and worst-case time complexity of O(log n). Each recursive call searches only one half of the remaining interval.

**Experimental Behaviour:**

The experimental comparison counts are similar to those of Iterative Binary Search because both algorithms follow the same search strategy. However, execution times may differ due to the overhead of recursive function calls.

**Comparison:**

The observed comparison counts agree with the theoretical logarithmic growth. Recursive Binary Search is efficient for large, sorted datasets, but it requires additional call-stack space.

## 10.3 Comparison Table

| Factor | Linear Search | Iterative Binary Search | Recursive Binary Search |
|---|---|---|---|
| Worst-case time complexity | O(n) | O(log n) | O(log n) |
| Growth in comparisons | Linear | Logarithmic | Logarithmic |
| Sorting required | No | Yes | Yes |
| Additional call-stack space | O(1) | O(1) | O(log n) |
| Scalability for large sorted datasets | Low | High | High |

## 10.4 Agreement Between Theory and Experiment

The theoretical analysis predicts that Linear Search requires a number of comparisons proportional to the input size, whereas both Binary Search algorithms require a logarithmic number of comparisons.

The experimental comparison counts should reflect these growth patterns. Small differences in measured execution time do not necessarily indicate a disagreement with theoretical complexity because Big-O notation describes the growth rate rather than exact running time.

## 10.5 Reasons for Differences Between Theory and Experiment

Theoretical complexity analysis counts operations and ignores many practical details. Actual execution time can differ because of:

1. **Hardware performance:** Processor speed and available memory affect execution time.
2. **Programming language overhead:** Python interpreter operations contribute to the measured time.
3. **Recursive function calls:** Recursive Binary Search incurs additional function-call and stack-management overhead.
4. **System activity:** Other running programs may affect timing measurements.
5. **Measurement overhead:** Very short searches may be affected by the precision of the timer and measurement procedure.

Therefore, repeated measurements and average execution times provide a more reliable comparison.

## 10.6 Scalability in the University Database

The university database contains approximately 1,000,000 student records and receives 50,000 search requests per hour.

Linear Search may perform up to 1,000,000 comparisons for one unsuccessful search. Binary Search requires approximately 20 iterations under balanced-halving analysis for the same dataset.

Consequently, Iterative and Recursive Binary Search are more suitable for frequent searches when the registration numbers are maintained in sorted order. Since new records are added once per day, the cost of maintaining the sorted data must also be considered.

## 10.7 Conclusion

The theoretical and experimental analyses demonstrate that Linear Search has linear worst-case growth, whereas Iterative and Recursive Binary Search have logarithmic worst-case growth. Binary Search approaches are more scalable for large, sorted university databases. Although their comparison counts are similar, their actual execution times may differ because of implementation overhead and system conditions. Therefore, theoretical analysis and experimental measurements together provide a more complete evaluation of algorithm performance.

