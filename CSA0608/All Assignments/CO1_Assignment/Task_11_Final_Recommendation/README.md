# TASK 11 – RECOMMEND AND DEFEND THE FINAL DESIGN 
## 11.1 Introduction

The university student-record system contains approximately 1,000,000 student records and receives 50,000 search requests per hour. Therefore, an efficient searching algorithm is required to provide fast record retrieval and support future database growth.

Based on the theoretical complexity analysis and experimental comparison, Iterative Binary Search is recommended for the university student-record system, provided that the registration numbers are maintained in sorted order.

## 11.2 Recommended Algorithm

**Recommended Approach: Iterative Binary Search**

Iterative Binary Search searches a sorted array by comparing the required registration number with the middle element. If the key is not found, it eliminates half of the remaining search interval and continues until the key is found or the interval becomes empty.

This approach is recommended because it provides efficient searching with logarithmic time complexity and does not require recursive function calls.

## 11.3 Reasons for Selecting Iterative Binary Search

**1. Theoretical Efficiency**

The worst-case time complexity of Iterative Binary Search is:

\[
T(n)=O(\log n)
\]

For one million student records:

\[
\log_2(1,000,000)\approx 19.93
\]

Therefore, approximately 20 iterations are sufficient under the usual balanced-halving analysis. Linear Search, in contrast, may examine all one million records.

**2. Experimental Performance**

The comparison-count results from Task 9 can be used to evaluate the performance of the three algorithms. Linear Search performs up to \(n\) comparisons for an absent key, while Iterative Binary Search requires logarithmically many comparisons.

Iterative Binary Search also avoids the function-call overhead associated with Recursive Binary Search. The actual execution-time measurements from Task 9 should be used to confirm the observed performance on the test computer.

**3. Preprocessing Cost**

Binary Search requires the registration numbers to be sorted in ascending order. If the database is initially unsorted, sorting is necessary and introduces an additional cost. For example, comparison-based Merge Sort requires \(O(n\log n)\) time.

However, the university adds new records only once per day. The records can be maintained in sorted order or updated in batches, allowing the sorting or maintenance cost to be shared across many search requests.

**4. Scalability**

The system receives 50,000 search requests per hour. Since Binary Search has logarithmic search complexity, it remains efficient as the number of student records grows from thousands to millions.

**5. Simplicity and Memory Usage**

Iterative Binary Search uses a loop rather than recursive function calls. Its auxiliary space complexity is \(O(1)\), making it simple to implement and efficient in memory usage.

## 11.4 Comparison with Alternative Algorithms

| Factor | Linear Search | Iterative Binary Search | Recursive Binary Search |
|---|---|---|---|
| Worst-case time complexity | \(O(n)\) | \(O(\log n)\) | \(O(\log n)\) |
| Sorted data required | No | Yes | Yes |
| Auxiliary space | \(O(1)\) | \(O(1)\) | \(O(\log n)\) |
| Function-call overhead | No recursion | No recursion | Recursive calls |
| Suitability for large, sorted data | Less suitable | Highly suitable | Highly suitable |

Linear Search is useful when data is unsorted or the dataset is small. Recursive Binary Search is also efficient, but Iterative Binary Search is preferred because it avoids recursion overhead and uses constant auxiliary space.

## 11.5 Limitations and Trade-Offs

Although Iterative Binary Search is efficient, it requires sorted data and is most straightforward to implement on an array or another structure that supports efficient middle-element access.

Maintaining sorted records when new students are added may introduce update costs. For a database with frequent insertions, deletions, or updates, a database index or balanced search tree may be more practical than repeatedly sorting an entire array.

The final system design should therefore consider both search efficiency and the cost of maintaining the data structure.

## 11.6 Final Recommendation

Iterative Binary Search is recommended for the university student-record system when the registration numbers are stored in sorted order or an appropriate indexed structure is maintained. Its logarithmic search complexity, constant auxiliary space, and lack of recursive function-call overhead make it a practical choice for frequent searches.

This recommendation is supported by the theoretical analysis in Tasks 3–7 and should be validated using the comparison counts and execution times collected in Tasks 8–10. As the database grows beyond one million records, the same approach remains efficient, provided that the cost of maintaining sorted data is properly managed.

## 11.7 Conclusion

The analysis shows that Iterative Binary Search offers an effective balance of search speed, memory usage, and implementation simplicity. It is more suitable than Linear Search for frequent searches in a large, sorted student database and avoids the additional stack space required by Recursive Binary Search. Therefore, it is the preferred algorithm for the proposed university student-record system under the stated conditions.
