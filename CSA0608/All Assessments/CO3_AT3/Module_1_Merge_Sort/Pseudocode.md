# Module 1 – Stable Merge Sort

## Algorithm 1: MERGE_SORT

```text
MERGE_SORT(A, low, high)

1. If low < high, then
2.     mid = (low + high) / 2
3.     MERGE_SORT(A, low, mid)
4.     MERGE_SORT(A, mid + 1, high)
5.     MERGE(A, low, mid, high)
6. End If

7. Return

## ALGORITHM 2 - MERGE ##

MERGE(A, low, mid, high)

1. Create temporary arrays Left and Right
2. Copy A[low...mid] into Left
3. Copy A[mid+1...high] into Right
4. Set i = 0, j = 0, k = low

5. While i < size(Left) AND j < size(Right)
6.     If Left[i].timestamp <= Right[j].timestamp
7.         A[k] = Left[i]
8.         i = i + 1
9.     Else
10.        A[k] = Right[j]
11.        j = j + 1
12.    End If
13.    k = k + 1
14. End While

15. While i < size(Left)
16.     A[k] = Left[i]
17.     i = i + 1
18.     k = k + 1
19. End While

20. While j < size(Right)
21.     A[k] = Right[j]
22.     j = j + 1
23.     k = k + 1
24. End While

25. Return
