# TASK 12 – RE-EVALUATE AND ADAPT THE DESIGN 
## A. Impact Analysis 
### 12.1 Changes in Requirements

The university student-record system must now process 50,000 search requests per hour using a database containing 1,000,000 student records. However, new student records are added only once per day.

These requirements highlight the need for fast searching while keeping the cost of maintaining the database manageable.

### 12.2 Impact on Original Assumptions

The original design recommended Iterative Binary Search because it provides logarithmic search complexity. The changed requirements emphasize the following factors:

1. **High search frequency:** The system must handle 50,000 searches per hour, equivalent to approximately 13.89 searches per second on average.
2. **Large dataset:** Searching must remain efficient for 1,000,000 student records.
3. **Low update frequency:** New records are added only once per day, so the database does not need to be reorganized after every search.
4. **Preprocessing cost:** Sorting or maintaining an index may require additional processing, but this cost can be spread across many searches.
5. **Scalability:** The chosen approach must remain efficient as the database grows.

The main change is that search performance becomes especially important compared with record-update frequency. Therefore, a design that maintains searchable data in sorted order is appropriate.

## B. Evaluation of the Original Design 
### 12.3 Suitability of Iterative Binary Search

The original recommendation of Iterative Binary Search remains appropriate because it has a worst-case time complexity of \(O(\log n)\).

For a database containing 1,000,000 records:

\[
\log_2(1,000,000)\approx19.93
\]

Therefore, approximately 20 iterations are sufficient under the usual balanced-halving analysis.

In contrast, Linear Search may examine all 1,000,000 records when the required registration number is absent or located at the end of the list.

### 12.4 Preprocessing Cost

If the database is initially unsorted, sorting it using Merge Sort requires:

\[
P(n)=O(n\log n)
\]

After sorting, each Binary Search requires only:

\[
S(n)=O(\log n)
\]

Since new records are added once per day, the university can maintain the sorted data or update it in batches. The preprocessing cost can therefore be shared across many search requests instead of repeating a full sort for every search.

### 12.5 Alternative Approach

A database index, such as a balanced B-tree index on the registration-number column, could provide better overall system performance. It supports efficient searches and allows new records to be inserted without repeatedly sorting the entire database.

However, for the current algorithm comparison, Iterative Binary Search remains an appropriate choice when the data is already stored in a sorted array.

## C. Adaptation or Redesign 
### 12.6 Design Decision: Modify the Original Solution

The original solution will be modified rather than completely replaced. Iterative Binary Search will remain the basic searching algorithm, while the data-maintenance strategy will be improved.

The revised strategy is:

1. Store student records ordered by registration number, or maintain a suitable database index.
2. Use Iterative Binary Search on the sorted array when implementing the assignment algorithms.
3. Add new student records through a daily update process that maintains the sorted order.
4. Avoid sorting the entire dataset before every search request.
5. Validate the revised implementation using the same datasets and test cases used in the earlier tasks.

### 12.7 Effect on Computational Complexity

For a sorted array, Iterative Binary Search has:

\[
T_{\text{search}}(n)=O(\log n)
\]

Its auxiliary space complexity is:

\[
S(n)=O(1)
\]

If the database is initially unsorted and requires Merge Sort:

\[
T_{\text{sort}}(n)=O(n\log n)
\]

However, sorting is not repeated for every search. For a database index, search and insertion costs depend on the chosen index structure; a balanced B-tree typically supports search and insertion in \(O(\log n)\) time under standard assumptions.

This modified design preserves efficient searching while reducing unnecessary preprocessing.

## D. Evidence-Based Defence (2 Marks)

### 12.8 Mathematical Evidence

The theoretical worst-case complexities of the three proposed algorithms are:

| Algorithm | Worst-case search time | Suitability for 1,000,000 records |
|---|---|---|
| Linear Search | \(O(n)\) | Less suitable for frequent searches |
| Iterative Binary Search | \(O(\log n)\) | Highly suitable for sorted data |
| Recursive Binary Search | \(O(\log n)\) | Suitable, but uses additional stack space |

For one million records, Linear Search may require up to one million element comparisons, whereas Binary Search requires approximately 20 iterations under balanced-halving analysis.

### 12.9 Evidence from Search Frequency

The system receives 50,000 searches per hour.

\[
\frac{50,000}{3,600}\approx13.89
\]

Therefore, the system processes approximately 13.89 search requests per second on average.

Because searches are frequent and updates are infrequent, investing in maintaining sorted data or an index is justified. This reduces the cost of repeated searches.

### 12.10 Experimental Evidence

The comparison counts and execution times collected in Task 9 should be used to validate the theoretical analysis.

The expected observation is that Linear Search comparison counts increase proportionally to dataset size, whereas the comparison counts of Iterative and Recursive Binary Search increase logarithmically.

Actual execution-time measurements should be taken from the program output. They should not be assumed from theoretical complexity alone.

### 12.11 Computational Trade-Offs

The revised design offers the following advantages:

- Fast searches for a large student database.
- Constant auxiliary space for Iterative Binary Search on an array.
- Lower repeated preprocessing costs when sorted data is maintained.
- Better scalability as the number of student records increases.

The main limitation is that maintaining a sorted array can make insertions expensive because elements may need to be shifted. If the database is implemented as a real production system, a database index is generally more practical than repeatedly sorting a large array.

## 12.12 Final Conclusion

After evaluating the changed requirements, the original recommendation is retained with a modification to the data-maintenance strategy. Iterative Binary Search remains efficient for sorted student registration numbers because it has \(O(\log n)\) worst-case search complexity and \(O(1)\) auxiliary space.

The high search frequency of 50,000 requests per hour and the low update frequency of once per day justify maintaining searchable data in sorted order or using a database index. The final design balances search efficiency, preprocessing cost, memory usage, and future scalability. Experimental measurements from Task 9 should be used to confirm the expected performance on the test system.
