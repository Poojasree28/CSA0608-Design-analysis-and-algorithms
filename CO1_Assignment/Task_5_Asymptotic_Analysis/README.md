# TASK 5 – PERFORM ASYMPTOTIC ANALYSIS 
## 5.1 Introduction

Asymptotic analysis describes how an algorithm's running time grows as the input size \(n\) becomes very large. Big-O notation represents an asymptotic upper bound, Omega notation represents a lower bound, and Theta notation represents a tight asymptotic bound.

## 5.2 Asymptotic Analysis of the Algorithms

### 1. Linear Search

Linear Search examines registration numbers sequentially until the required number is found or the list ends.

- **Best case:** \(\Omega(1)\), when the key is the first element.
- **Worst case:** \(O(n)\), when the key is last or absent.
- **Average case:** \(\Theta(n)\), assuming successful searches are equally likely to target any position.

Therefore, the worst-case running time is \(\Theta(n)\).

As the database grows, the number of comparisons increases proportionally to the number of records. A database with 1,000,000 records may require up to 1,000,000 element checks.

### 2. Iterative Binary Search

Iterative Binary Search repeatedly halves the search interval in a sorted array.

- **Best case:** \(\Theta(1)\), when the key matches the middle element immediately.
- **Worst case:** \(\Theta(\log n)\).
- **Average case:** \(\Theta(\log n)\), for a uniformly distributed successful search over sorted positions.

Therefore, the worst-case running time is \(\Theta(\log n)\).

As the database grows, the number of comparisons increases very slowly because each comparison eliminates approximately half of the remaining records.

### 3. Recursive Binary Search

Recursive Binary Search uses recursive function calls to search progressively smaller halves of a sorted array.

- **Best case:** \(\Theta(1)\), when the key matches the middle element in the first call.
- **Worst case:** \(\Theta(\log n)\).
- **Average case:** \(\Theta(\log n)\), under the same successful-search assumption.

The recursive and iterative versions have the same asymptotic search-time growth. However, Recursive Binary Search requires additional stack space for its recursive calls.

## 5.3 Comparison of Growth Rates

| Algorithm | Best-case time | Average-case time | Worst-case time |
|---|---|---|---|
| Linear Search | \(\Theta(1)\) | \(\Theta(n)\) | \(\Theta(n)\) |
| Iterative Binary Search | \(\Theta(1)\) | \(\Theta(\log n)\) | \(\Theta(\log n)\) |
| Recursive Binary Search | \(\Theta(1)\) | \(\Theta(\log n)\) | \(\Theta(\log n)\) |

## 5.4 Growth When the Dataset Increases

For Binary Search, the approximate worst-case number of iterations is \(\lfloor\log_2 n\rfloor+1\).

| Dataset size (\(n\)) | Linear Search: worst-case checks | Binary Search: maximum iterations |
|---:|---:|---:|
| 1,000 | 1,000 | 10 |
| 10,000 | 10,000 | 14 |
| 100,000 | 100,000 | 17 |
| 1,000,000 | 1,000,000 | 20 |

The table shows that increasing the dataset from 1,000 to 1,000,000 records multiplies the worst-case Linear Search comparisons by 1,000. In contrast, Binary Search increases from approximately 10 to 20 iterations.

## 5.5 Interpretation in the University Database Context

The university database receives 50,000 search requests per hour and contains approximately 1,000,000 student records. Linear Search may perform an extremely large number of comparisons when many requests target records near the end or search for absent registration numbers.

Iterative and Recursive Binary Search are more scalable because their search time grows logarithmically rather than linearly. If the database is maintained in sorted order, both approaches can locate records with approximately 20 iterations in the worst case for one million records.

Since new records are added once per day, maintaining sorted order or periodically sorting the records can support efficient searches. The sorting and update costs must also be considered when evaluating the complete system.

## 5.6 Conclusion

Asymptotic analysis shows that Linear Search has linear growth, \(\Theta(n)\), in its average and worst cases, whereas both Binary Search algorithms have logarithmic growth, \(\Theta(\log n)\). For a large university database with frequent search requests, Binary Search provides better scalability when the records are sorted. Iterative and Recursive Binary Search have similar search-time complexity, although the recursive version uses additional call-stack space.
