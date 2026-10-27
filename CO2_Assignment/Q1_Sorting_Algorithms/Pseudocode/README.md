## Pseudocode

### SELECTION-SORT(A)
    for i = 0 to n-2
        minIndex = i
        for j = i+1 to n-1
            comparisons += 1
            if A[j] < A[minIndex]
                minIndex = j
        if minIndex != i
            swap A[i], A[minIndex]
            swaps += 1

### BUBBLE-SORT(A)
    for end = n-1 down to 1
        swapped = false
        for j = 0 to end-1
            comparisons += 1
            if A[j] > A[j+1]
                swap A[j], A[j+1]
                swaps += 1
                swapped = true
        if swapped == false
            break

### INSERTION-SORT(A)
    for i = 1 to n-1
        key = A[i]
        j = i-1
        while j >= 0
            comparisons += 1
            if A[j] > key
                A[j+1] = A[j]
                moves += 1
                j -= 1
            else
                break
        A[j+1] = key
        moves += 1
