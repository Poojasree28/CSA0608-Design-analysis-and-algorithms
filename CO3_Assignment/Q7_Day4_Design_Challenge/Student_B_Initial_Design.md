# Student B – Initial Design Proposal

## Problem: Counting Inversions in an Array

### 1. Proposed Decomposition
- Split the input array into two halves.
- Find the number of inversions in each half separately.
- Identify inversions that involve elements from both halves.
- Combine all inversion counts to obtain the final result.

### 2. Base Case
- If the array contains one or no elements, return 0.
- No inversion is possible in such a small array.

### 3. Required Subproblem Information
Each subproblem should provide:
- The elements in sorted order.
- The inversion count of that subarray.
- Information required to identify inversions between the two halves.

### 4. Possible Combine Strategy
- Merge the two sorted subarrays.
- Compare elements from both halves.
- Whenever an element from the right half is smaller than an element from the left half, count the remaining elements in the left half.
- Add the cross-inversion count to the two subproblem counts.

### 5. Initial Conclusion
I propose using a recursive sorting-based approach. The merging process can be used not only to sort the elements but also to count inversions between the two halves.
