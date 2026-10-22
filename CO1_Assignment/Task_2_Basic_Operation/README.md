# TASK 2 – IDENTIFY THE BASIC OPERATION 
## 2.1 Linear Search

**Basic Operation:** Comparison between the array element and the search key (`A[i] == key`).

**Where it occurs:** Inside the `for` loop, where each registration number is compared with the required registration number.

**Justification:** This comparison is the basic operation because it determines whether the required registration number has been found. Linear Search checks elements one by one until the key is found or the list ends.

**Effect of Input Size (n):** As the number of student records increases, the number of comparisons may also increase. In the worst case, Linear Search performs `n` comparisons when the key is the last element or is absent. Therefore, its worst-case time complexity is **O(n)**.

## 2.2 Iterative Binary Search

**Basic Operation:** Comparison between the middle element and the search key (`A[mid] == key` and `key < A[mid]`).

**Where it occurs:** Inside the `while` loop, where the middle registration number is checked against the required registration number.

**Justification:** These comparisons determine whether the key is found or whether the search should continue in the left or right half of the sorted array. They are appropriate for efficiency analysis because they control how quickly the search space decreases.

**Effect of Input Size (n):** Each iteration reduces the remaining search space by approximately half. Therefore, the number of comparisons increases logarithmically as the number of records increases. The worst-case time complexity is **O(log n)**.

## 2.3 Recursive Binary Search

**Basic Operation:** Comparison between the middle element and the search key (`A[mid] == key` and `key < A[mid]`).

**Where it occurs:** In each recursive call, after calculating the middle index, the algorithm compares the middle registration number with the key.

**Justification:** These comparisons determine whether the search is complete or another recursive call is required. They are the dominant operation because each call reduces the search interval by approximately half.

**Effect of Input Size (n):** As the input size increases, the number of recursive calls and associated key comparisons increases logarithmically. Therefore, its worst-case time complexity is **O(log n)**. Unlike Iterative Binary Search, it also uses additional call-stack space for recursion.

## 2.4 Conclusion

The dominant basic operation in all three algorithms is the comparison of a registration number with the search key. Linear Search may examine every record, resulting in **O(n)** worst-case time complexity. Iterative and Recursive Binary Search repeatedly halve the search interval, resulting in **O(log n)** worst-case time complexity. Counting these comparisons helps evaluate and compare the efficiency of the algorithms.
