# Student A – Initial Design Proposal

## Problem: Counting Inversions in an Array

### 1. Proposed Decomposition
- Divide the given array into two approximately equal halves.
- Count the inversions present in the left half.
- Count the inversions present in the right half.
- Count the inversions formed between the left and right halves.

### 2. Base Case
- If the array contains zero or one element, return 0.
- A single element cannot form an inversion.

### 3. Required Subproblem Information
Each recursive call should return:
- The sorted version of its subarray.
- The number of inversions found in that subarray.

### 4. Possible Combine Strategy
- Combine the two sorted halves using a merge operation.
- During merging, count cross-inversions.
- If an element from the right half is smaller than the current element in the left half, count all remaining elements in the left half as inversions.
- Add left, right and cross-inversion counts.

### 5. Initial Conclusion
I propose using a Merge Sort-based Divide and Conquer approach because it divides the array into smaller subproblems and counts inversions efficiently while merging the sorted halves.
