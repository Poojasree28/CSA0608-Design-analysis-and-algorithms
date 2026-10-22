<div align="justify">



# Aim

To analyse the time and space efficiency of the ShopSphere e-commerce platform’s back-end modules using exact operation counts, asymptotic notation, backward substitution, the Master Theorem, best/average/worst-case analysis, and a scalability audit for a catalogue of one million products.




# Problem Statement

ShopSphere currently maintains 100,000 products and expects the catalogue to grow to 1,000,000 products. The platform must assess five modules: duplicate-listing detection (M1), API rate limiting (M2), product search (S1 and S2), recommendation generation (M4), and sales analytics (M5). The report generator has cost f(n) = 3n² + 10n log₂ n + 50. The assigned question assumes that the server performs 10 basic operations per second and asks whether the modules can meet a nightly processing window of 10 minutes.




# Tools and Requirements

- Language: Python 3
- External packages: None required; the program uses the Python standard library.
- Execution command: `python scalability_audit.py`
- Input sizes: n = 100,000 and n = 1,000,000 for scalability comparison; M2 is also verified for n = 1,024.
- Assumption for theoretical runtime estimates: 10 basic operations per second, as stated in the question.




# Methodology

- Identify the basic operation for each module and derive its count or recurrence.
- Use exact summations for M1 and M2 and backward substitution for S2.
- Apply the Master Theorem to both M4 designs and use a recursion-tree/extended Master Theorem argument for M5.
- Compare best, average and worst cases for S1 and S2.
- Prove the report generator’s Θ(n²) bound using constants and disprove O(n) using the formal definition.
- Evaluate operation counts at n = 1,000,000 and convert them to time using 10 operations per second.
- Execute the accompanying Python program to verify arithmetic and print a machine-readable summary.




# Part (a) – Understand the Problem

| Module | Input size | Dominant basic operation | Expected growth | Reason |
|---|---|---|---|---|
| M1 – Duplicate detector | n products | Compare the title and seller of a pair of products | Θ(n²) | Every product is compared with every later product. |
| M2 – API rate limiter | n requests | Audit(Request[j]) | Θ(n) | The inner-loop counts form a geometric series: 1+2+4+…. |
| M3 – Product search S1 | n products | Compare target with the current product ID | Best Θ(1); average/worst Θ(n) | An unsorted list may require scanning many entries. |
| M3 – Product search S2 | n sorted index entries | Compare target with the middle key | Θ(log n) | Each comparison discards half the remaining index. |
| M4 – Recommendation engine | n customer-product records | Process recursive subproblems and merge | Current Θ(n²); redesign Θ(n log n) | The current recurrence has four half-size calls; redesign has two. |
| M5 – Sales analytics | n sales records | Process/sort records at each recursive level | Θ(n log² n) | There are Θ(log n) levels, each contributing Θ(n log n). |




# Part (b) – Analyse the Iterative Modules

## M1: Exact number of comparisons

For each i from 0 to n − 2, j runs from i + 1 to n − 1. Therefore, the number of comparisons for a fixed i is n − i − 1.

C₁(n) = Σᵢ₌₀ⁿ⁻² (n − i − 1) = (n − 1) + (n − 2) + … + 2 + 1.

Using the sum of the first n − 1 positive integers:

C₁(n) = n(n − 1)/2 = (n² − n)/2.

Thus, time complexity is Θ(n²). The algorithm uses Θ(1) auxiliary space if the input catalogue is already stored and marking does not create a new data structure. If the list of duplicate indices is accumulated separately, that output storage depends on the number of duplicates.

## M2: Exact number of audit operations

The values of i are 1, 2, 4, 8, …, 2ᵏ, where 2ᵏ < n and 2ᵏ is the largest power of two below n. The inner loop performs i audits during an iteration.

Let k = ⌈log₂ n⌉ for n > 1. The loop values are 1, 2, …, 2ᵏ⁻¹, so

A(n) = Σᵣ₌₀ᵏ⁻¹ 2ʳ = 2ᵏ − 1 = 2^⌈log₂ n⌉ − 1.

Since n ≤ 2^⌈log₂ n⌉ < 2n, the count is Θ(n), not Θ(n log n). The team member’s claim is incorrect because the inner-loop lengths do not each equal n; they form a geometric series.

For n = 1,024 = 2¹⁰, the values are 1 + 2 + 4 + … + 512 = 2¹⁰ − 1 = 1,023 audit operations.

Space complexity is Θ(1) auxiliary space, since only the loop variables and current request are needed.




# Part (c) – Solve S2 by Backward Substitution

The question gives T(n) = T(n/2) + 1 and T(1) = 1. Assume n is a power of two.

- T(n) = T(n/2) + 1
- T(n/2) = T(n/4) + 1, therefore T(n) = T(n/4) + 2
- T(n) = T(n/8) + 3
- After k substitutions: T(n) = T(n/2ᵏ) + k
- Stop when n/2ᵏ = 1, so 2ᵏ = n and k = log₂ n
- Using T(1) = 1: T(n) = 1 + log₂ n

For n = 2ᵏ, the exact recurrence solution is T(n) = log₂ n + 1 comparisons. For arbitrary n, the comparison count is Θ(log n), with the precise count depending on the tree shape and stopping condition.

| Implementation | Time complexity | Auxiliary space |
|---|---|---|
| Iterative binary search | Θ(log n) | Θ(1) |
| Recursive binary search | Θ(log n) | Θ(log n) call stack |




# Part (d) – Apply the Master Theorem

## M4 current design: T(n) = 4T(n/2) + n

| Parameter | Value |
|---|---|
| a | 4 |
| b | 2 |
| f(n) | n = Θ(n) |
| n^(log_b a) | n^(log₂ 4) = n² |
| Comparison | f(n) = O(n^(2−1)) = O(n) |
| Master Theorem case | Case 1 |
| Result | T(n) = Θ(n²) |

The current design has quadratic growth because replicated partitions cause four recursive calls on half-sized inputs. Doubling n approximately quadruples the dominant work.

## M4 proposed redesign: T(n) = 2T(n/2) + n

| Parameter | Value |
|---|---|
| a | 2 |
| b | 2 |
| f(n) | n = Θ(n) |
| n^(log_b a) | n^(log₂ 2) = n |
| Comparison | f(n) = Θ(n^(log_b a)) |
| Master Theorem case | Case 2 |
| Result | T(n) = Θ(n log n) |

After redesign, doubling n increases the dominant work by approximately a factor of 2 × log₂(2n)/log₂(n), which approaches 2 for large n. Removing replication improves the asymptotic growth from quadratic to n log n.

## M5: T(n) = 2T(n/2) + n log n

Here a = 2, b = 2 and n^(log_b a) = n. The non-recursive work is f(n) = n log n, which is Θ(n log n), larger than n by a logarithmic factor. The three basic Master Theorem cases in their simplest form do not directly describe this logarithmic-factor extension; use the extended case or a recursion tree.

At each recursion-tree level, the subproblem sizes sum to n. At a level with subproblem size n/2ʳ, the combined non-recursive work is n(log₂ n − r). Summing for r = 0 through log₂ n − 1 gives n Σₛ₌₁ˡᵒᵍ²ⁿ s = Θ(n(log n)²).

Therefore, T(n) = Θ(n log² n).




# Part (e) – Best, Average and Worst Cases

| Algorithm | Case | Input condition | Comparisons |
|---|---|---|---|
| S1 linear search | Best | Target is first item | 1 |
| S1 linear search | Average (successful, uniformly located) | Target position equally likely from 1 to n | (n + 1)/2 |
| S1 linear search | Worst successful | Target is last item | n |
| S1 linear search | Unsuccessful | Target is absent | n |
| S2 binary search | Best | Target equals the first middle key | 1 |
| S2 binary search | Average | Depends on target distribution and tree shape | Θ(log n) |
| S2 binary search | Worst | Target is deepest leaf or absent after the last interval | Θ(log n) |

## S1 expected comparisons when existence probability is p

Assume a successful target is equally likely to occur at any of the n positions, and an unsuccessful search checks all n items. Conditional expected comparisons are (n + 1)/2 when present and n when absent.

E[C] = p(n + 1)/2 + (1 − p)n = n − p(n − 1)/2.

For n = 1,000,000 and p = 0.5:

E[C] = 1,000,000 − 0.5 × 999,999 / 2 = 750,000.25 comparisons.

This result assumes uniform position for successful searches. If the question uses a different distribution, the expected count would need to be adjusted.




# Part (f) – Prove the Asymptotic Bound

Given f(n) = 3n² + 10n log₂ n + 50, show f(n) = Θ(n²).

For n ≥ 1, log₂ n ≤ n, so n log₂ n ≤ n². Also, 50 ≤ 50n². Thus f(n) ≤ 3n² + 10n² + 50n² = 63n².

For the lower bound, f(n) ≥ 3n² for all n ≥ 1. Choose c₁ = 3, c₂ = 63 and n₀ = 1. Then 3n² ≤ f(n) ≤ 63n² for all n ≥ n₀. Therefore f(n) = Θ(n²).

## Show f(n) is not O(n)

If f(n) were O(n), there would be constants c > 0 and n₀ such that f(n) ≤ cn for every n ≥ n₀. But f(n) ≥ 3n², so this would require 3n² ≤ cn, or 3n ≤ c, for arbitrarily large n. This is impossible for any fixed c.

Therefore f(n) ∉ O(n).




# Part (g) – Scalability Decision

The assignment states that the server performs 10 basic operations per second and the processing window is 10 minutes = 600 seconds. Therefore, the nominal capacity is 6,000 basic operations during the window. The estimates below count the dominant operations; actual wall-clock time can be greater because of constants and system overhead.

| Module/design | Operation count at n = 1,000,000 | Estimated time at 10 ops/s | Within 10 minutes? |
|---|---|---|---|
| M1 | n(n − 1)/2 = 499,999,500,000 comparisons | 49,999,950,000 seconds ≈ 1,584.4 years | No |
| M2 | 2^⌈log₂ n⌉ − 1 = 1,048,575 audits | 104,857.5 seconds ≈ 29.1 hours | No |
| S2 | log₂ n + 1 ≈ 20.93; use about 20–21 comparisons | About 2.0–2.1 seconds | Yes |
| M4 current | Θ(n²); leading-scale estimate n² = 10¹² | About 100,000,000,000 seconds | No |
| M4 redesign | Θ(n log₂ n); leading-scale estimate n log₂ n ≈ 19,931,569 | About 1,993,157 seconds ≈ 23.1 days | No under this stated rate |
| M5 | Θ(n log₂² n); leading-scale estimate n(log₂ n)² ≈ 398,631,371 | About 39,863,137 seconds ≈ 461.4 days | No |

Important interpretation: the question provides recurrences and asymptotic forms but not all recurrence base-case costs or exact operation constants. For M4 and M5, these are leading-scale estimates rather than exact instruction counts. The 10-operations-per-second assumption is very restrictive; apply it consistently when answering the question.




# Redesign Recommendations

- M1: Replace pairwise comparison with a hash-based grouping by (seller, normalized title), expected Θ(n), or sort by the key and scan adjacent records in Θ(n log n).
- M2: The given doubling-window algorithm is Θ(n), but its exact count exceeds the stated 10-minute capacity at one million requests under the supplied rate. Consider batching, incremental counters, and suitable rate-limiting data structures.
- S2: Keep binary search on a sorted index, or use an appropriate database index for production-scale queries.
- M4: Remove replicated recursive work as proposed; this changes Θ(n²) to Θ(n log n), although the stated throughput assumption still predicts more than 10 minutes.
- M5: Review the repeated sorting/processing at each level. Seek a design with linear or n log n total work where the business requirements permit it, and profile actual implementation costs.
- Validate theoretical estimates with repeated execution on realistic data; distinguish asymptotic operation counts from measured wall-clock time.




# Python Implementation and Verification

The accompanying source file scalability_audit.py calculates the principal operation-count estimates and checks the M2 count at n = 1,024. Execute it using Python and capture the terminal output for the final report. This report document is a prepared solution draft; add your own actual source-code and execution screenshots before submission.






## SOURCE CODE:



<img width="1031" height="1062" alt="image" src="https://github.com/user-attachments/assets/e80ab113-fc7c-4331-8b67-1a7c5251d976" />



<img width="1027" height="1005" alt="image" src="https://github.com/user-attachments/assets/57b1bb04-119c-4ca4-a56d-adfd64acfb1c" />



<img width="1028" height="926" alt="image" src="https://github.com/user-attachments/assets/5f21aeac-4c6f-489c-b3ea-054aabf1c3ce" />



<img width="1025" height="1264" alt="image" src="https://github.com/user-attachments/assets/9dcdac71-a709-4ff9-b1c4-60a5217a2c5a" />



<img width="1030" height="1043" alt="image" src="https://github.com/user-attachments/assets/f6ddfabb-5654-4b50-ade4-325a4ce34aba" />



<img width="1027" height="1230" alt="image" src="https://github.com/user-attachments/assets/201c5979-28d2-4750-a811-86d6f3c4c9b2" />




<img width="981" height="1306" alt="image" src="https://github.com/user-attachments/assets/68db1c51-c908-4110-a7d5-855bad56edea" />



<img width="1023" height="1254" alt="image" src="https://github.com/user-attachments/assets/24bbc43b-bc49-4fd4-8409-303954c75a44" />








## OUTPUT SCREENSHOT:




<img width="1024" height="1295" alt="image" src="https://github.com/user-attachments/assets/1c6279c9-cea1-4d5f-ae4d-2746dcc8895a" />






<img width="1033" height="835" alt="image" src="https://github.com/user-attachments/assets/752d73d7-4754-483b-a2c0-3155122285b5" />




# Analysis

The ShopSphere Scalability Audit analyses the time and space complexity of five modules as the product catalogue grows from 100,000 to 1,000,000 products.

- M1 – Duplicate-Listing Detector: Performs (n(n-1)/2) comparisons, giving (Θ(n²)) time complexity.

- M2 – API Rate Limiter: Performs (2^{⌈log₂ n⌉}-1) audits, giving (Θ(n)) time complexity.

- M3 – Product Search: Linear Search has (Θ(n)) average and worst-case complexity, while Binary Search has (Θ(log n)) time complexity.

- M4 – Recommendation Engine: The current design has (Θ(n²)) complexity. The proposed redesign improves it to (Θ(n log n)).

- M5 – Sales Analytics Engine: The recurrence (T(n)=2T(n/2)+n log n) gives (Θ(n log² n)) complexity.

- Asymptotic Proof: The report generator function (f(n)=3n²+10n log n+50) is (Θ(n²)) and is not (O(n)).

- The scalability estimates identify which modules exceed the 10-minute processing limit under the assignment's assumption of 10 basic operations per second. The results help identify inefficient algorithms and recommend improvements for handling a growing product catalogue.

# Conclusion

The audit shows that algorithm design determines whether ShopSphere can scale. M1 is quadratic and should be redesigned. M2 has a geometric-series operation count and is Θ(n), not Θ(n log n), but its count still exceeds the stated capacity at n = 1,000,000. S2 is logarithmic and scales well. M4 improves from Θ(n²) to Θ(n log n) by removing replicated recursion. M5 is Θ(n log² n). The report generator is Θ(n²), and its cost is not O(n). Theoretical results should be complemented by execution evidence and realistic profiling.
</div>
