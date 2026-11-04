# Joint Final Design

## Problem: Counting Inversions in an Array

### 1. Comparison of Student A and Student B Designs

| Design Aspect | Student A | Student B |
|---|---|---|
| Decomposition | Divide array into two halves | Divide array into two halves |
| Base Case | Zero or one element | Zero or one element |
| Subproblem Information | Sorted subarray and inversion count | Sorted subarray and inversion count |
| Combine Strategy | Merge and count cross-inversions | Merge and count cross-inversions |
| Main Approach | Merge Sort-based approach | Recursive sorting-based approach |

### 2. Agreement Between the Designs
- Both students proposed dividing the array into two halves.
- Both selected zero or one element as the base case.
- Both identified the need to count inversions within each half and across the halves.
- Both proposed using merging to count cross-inversions.

### 3. Strengths and Weaknesses

**Strengths**
- The problem can be divided into smaller subproblems.
- Each subproblem can be solved recursively.
- The merge operation helps count cross-inversions efficiently.
- The approach avoids checking every possible pair individually.

**Weaknesses**
- Additional memory is required during merging.
- Recursive calls introduce some overhead.
- Correct counting requires maintaining sorted subarrays.

### 4. Final Decomposition
- Divide the array into left and right halves.
- Recursively count inversions in the left half.
- Recursively count inversions in the right half.
- Count cross-inversions while merging the sorted halves.
- Add all three counts.

### 5. Base Case
If the array contains zero or one element, return 0 because no inversion can exist.

### 6. Information Returned
Each recursive call returns:
- A sorted subarray.
- The total number of inversions in that subarray.

### 7. Combine Operation
- Merge the two sorted subarrays.
- If the current right element is smaller than the current left element, add the number of remaining elements in the left subarray to the cross-inversion count.
- Complete the merge.
- Add the left, right and cross-inversion counts.

### 8. Final Algorithm

```text
COUNT-INVERSIONS(A):

    if length(A) <= 1:
        return A, 0

    divide A into left and right halves

    left_sorted, left_count = COUNT-INVERSIONS(left)

    right_sorted, right_count = COUNT-INVERSIONS(right)

    merged, cross_count = MERGE-AND-COUNT(left_sorted, right_sorted)

    total_count = left_count + right_count + cross_count

    return merged, total_count
```

### 9. Recurrence Relation

T(n) = 2T(n/2) + O(n)

Where:
- 2T(n/2) represents the two recursive calls.
- O(n) represents the merging and cross-inversion counting process.

Using the Master Theorem:

**Time Complexity: O(n log n)**

### 10. Final Conclusion
Both initial designs used a similar Divide and Conquer strategy. After comparing the proposals, the group selected the Merge Sort-based approach because it efficiently counts inversions while sorting the array. The final design uses recursive division and an efficient merging process to achieve O(n log n) time complexity.
