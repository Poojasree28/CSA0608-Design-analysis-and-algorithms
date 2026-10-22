

## Table 1: Performance Results

| Dataset Size | Algorithm | Average Time (ms) | Average Comparisons/Lookups |
|---|---|---:|---:|
| 1,000 | Linear Search | 0.058838 | 479.30 |
| 1,000 | Recursive Binary Search | 0.001911 | 9.00 |
| 1,000 | Hash Table Search | 0.000417 | 1.00 |
| 10,000 | Linear Search | 0.897288 | 4,896.93 |
| 10,000 | Recursive Binary Search | 0.071547 | 12.20 |
| 10,000 | Hash Table Search | 0.026078 | 1.00 |
| 100,000 | Linear Search | 12.441707 | 51,220.87 |
| 100,000 | Recursive Binary Search | 0.021422 | 15.33 |
| 100,000 | Hash Table Search | 0.001114 | 1.00 |
| 1,000,000 | Linear Search | 244.479962 | 521,474.03 |
| 1,000,000 | Recursive Binary Search | 0.009433 | 18.93 |
| 1,000,000 | Hash Table Search | 0.008276 | 1.00 |













## Table 2: Complexity Comparison

| Algorithm | Best Case | Average Case | Worst Case | Auxiliary Space |
|---|---|---|---|---|
| Linear Search | O(1) | O(n) | O(n) | O(1) |
| Recursive Binary Search | O(1) | O(log n) | O(log n) | O(log n) |
| Hash Table Search | O(1) | O(1) expected | O(n) | O(n) for hash table storage |












## Table 3: Algorithm Comparison

| Algorithm | Sorted Input Required | Preprocessing | Advantages | Limitations |
|---|---|---|---|---|
| Linear Search | No | None | Simple and works on unsorted data | Can require scanning the entire dataset |
| Recursive Binary Search | Yes | Sort data if initially unsorted | Efficient logarithmic search | Requires sorted data and recursive stack space |
| Hash Table Search | No | Build and maintain hash table | Expected constant-time lookup | Extra memory and possible collision overhead |
















# **GRAPHS**

 


<img width="1045" height="502" alt="image" src="https://github.com/user-attachments/assets/5da546d1-485d-465a-9b5c-7bb044040e3c" />

<img width="1021" height="589" alt="image" src="https://github.com/user-attachments/assets/5b7fa2c0-3a4a-4f6f-a739-6b19ade6aa0e" />


<img width="1034" height="548" alt="image" src="https://github.com/user-attachments/assets/66f616bb-f82a-440c-a3ab-e9bf901c518f" />



                                                    FIGURE 1: SEARCH ALGORITHM PERFORMANCE

# **FIGURE 3: AVERAGE PER-REQUEST SEARCH TIME VERSUS DATASET SIZE (LOG AXES)**

# **FIGURE 4: AVERAGE KEY COMPARISONS/LOOKUP OPERATIONS VERSUS DATASET SIZE**







<img width="1034" height="514" alt="image" src="https://github.com/user-attachments/assets/5e609e1f-c5ed-473d-acbb-e14b7fb5ecab" />





                                             

                                             FIGURE 2: AVERAGE PER-REQUEST SEARCH TIME VERSUS DATASET SIZE (LOG AXES)





<img width="1051" height="639" alt="image" src="https://github.com/user-attachments/assets/b75069ef-91c4-4205-bb5a-3a5d3408dae4" />



                                               
                                               FIGURE 3. AVERAGE KEY COMPARISONS/LOOKUP OPERATIONS VERSUS DATASET SIZE




                                               
