
# SentinelOps SOC Alert-Triage Module

## Python Source Code

The following Python program implements stable alert sorting, blocklist IP checking, KMP signature matching, closest-pair login detection, algorithm comparison, and graph generation.

```python
import math
import random
import os
import matplotlib.pyplot as plt


# 1. STABLE ALERT SORTING
def sort_alerts(alerts):
    return sorted(alerts, key=lambda alert: alert[1], reverse=True)


# 2. BLOCKLIST IP CHECK
def is_blocked(blocklist, ip):
    return ip in blocklist


# 3. KMP STRING MATCHING
def find_signature(log, pattern):
    if pattern == "":
        return list(range(len(log) + 1))

    n = len(log)
    m = len(pattern)
    lps = [0] * m
    length = 0
    i = 1

    while i < m:
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        elif length > 0:
            length = lps[length - 1]
        else:
            lps[i] = 0
            i += 1

    result = []
    i = 0
    j = 0

    while i < n:
        if log[i] == pattern[j]:
            i += 1
            j += 1

            if j == m:
                result.append(i - j)
                j = lps[j - 1]
        elif j > 0:
            j = lps[j - 1]
        else:
            i += 1

    return result


# 4. CLOSEST LOGIN LOCATIONS
def closest_logins(events):
    if len(events) < 2:
        return None, math.inf

    points = sorted(
        (x, y, index)
        for index, (x, y) in enumerate(events)
    )

    best_squared = math.inf
    best_pair = None

    for i in range(len(points)):
        x1, y1, index1 = points[i]
        j = i + 1

        while j < len(points):
            x2, y2, index2 = points[j]
            dx = x2 - x1

            if dx * dx >= best_squared:
                break

            dy = y2 - y1
            distance_squared = dx * dx + dy * dy

            if distance_squared < best_squared:
                best_squared = distance_squared
                best_pair = (index1, index2)

            j += 1

    return best_pair, math.sqrt(best_squared)


# 5. BRUTE-FORCE CLOSEST-PAIR EXPERIMENT
def brute_force_distance_count(events):
    n = len(events)

    if n < 2:
        return None, math.inf, 0

    best_squared = math.inf
    best_pair = None
    count = 0

    for i in range(n):
        for j in range(i + 1, n):
            dx = events[i][0] - events[j][0]
            dy = events[i][1] - events[j][1]

            distance_squared = dx * dx + dy * dy
            count += 1

            if distance_squared < best_squared:
                best_squared = distance_squared
                best_pair = (i, j)

    return best_pair, math.sqrt(best_squared), count


# 6. OPTIMIZED DISTANCE-COMPUTATION COUNT
def optimized_distance_count(events):
    if len(events) < 2:
        return 0

    points = sorted(
        (x, y, index)
        for index, (x, y) in enumerate(events)
    )

    best_squared = math.inf
    count = 0

    for i in range(len(points)):
        x1, y1, index1 = points[i]
        j = i + 1

        while j < len(points):
            x2, y2, index2 = points[j]
            dx = x2 - x1

            if dx * dx >= best_squared:
                break

            dy = y2 - y1
            distance_squared = dx * dx + dy * dy
            count += 1

            if distance_squared < best_squared:
                best_squared = distance_squared

            j += 1

    return count


# 7. INSERTION-SORT COMPARISON COUNT
def insertion_sort_comparisons(alerts):
    alerts = list(alerts)
    comparisons = 0

    for i in range(1, len(alerts)):
        key = alerts[i]
        j = i - 1

        while j >= 0:
            comparisons += 1

            if alerts[j][1] < key[1]:
                alerts[j + 1] = alerts[j]
                j -= 1
            else:
                break

        alerts[j + 1] = key

    return comparisons


# 8. GENERATE GRAPH 1
def generate_closest_pair_graph():
    sizes = [100, 300, 600, 1000]
    brute_counts = []
    optimized_counts = []
    rng = random.Random(42)

    print("\nCLOSEST-PAIR EXPERIMENT")
    print("-" * 55)

    for n in sizes:
        events = [
            (rng.uniform(0, 10000), rng.uniform(0, 10000))
            for _ in range(n)
        ]

        brute_count = n * (n - 1) // 2
        optimized_count = optimized_distance_count(events)

        brute_counts.append(brute_count)
        optimized_counts.append(optimized_count)

        print(
            "Events:", n,
            "| Brute Force:", brute_count,
            "| X-Sweep:", optimized_count
        )

    plt.figure(figsize=(9, 5))
    plt.plot(
        sizes, brute_counts,
        marker="o", label="Brute Force"
    )
    plt.plot(
        sizes, optimized_counts,
        marker="o", label="Optimized X-Sweep"
    )

    plt.xlabel("Number of Login Events")
    plt.ylabel("Distance Calculations")
    plt.title("Closest-Pair Algorithm Comparison")
    plt.legend()
    plt.grid(True)
    plt.tight_layout()

    filename = os.path.join(
        os.getcwd(), "closest_pair_comparison.png"
    )
    plt.savefig(filename, dpi=150)

    print("\nGraph 1 saved at:")
    print(filename)

    plt.show(block=True)
    plt.close()


# 9. GENERATE GRAPH 2
def generate_insertion_sort_graph():
    rng = random.Random(7)

    random_alerts = [
        ("ALERT-" + str(i), rng.randint(1, 100))
        for i in range(300)
    ]

    nearly_sorted = sorted(
        random_alerts,
        key=lambda alert: alert[1],
        reverse=True
    )

    # Introduce six swaps.
    for _ in range(6):
        i, j = rng.sample(range(300), 2)
        nearly_sorted[i], nearly_sorted[j] = (
            nearly_sorted[j], nearly_sorted[i]
        )

    nearly_count = insertion_sort_comparisons(nearly_sorted)
    random_count = insertion_sort_comparisons(random_alerts)

    print("\nINSERTION-SORT EXPERIMENT")
    print("-" * 55)
    print("Nearly sorted comparisons:", nearly_count)
    print("Random comparisons:", random_count)

    plt.figure(figsize=(8, 5))
    plt.bar(
        ["Nearly Sorted", "Random"],
        [nearly_count, random_count]
    )

    plt.xlabel("Input Type")
    plt.ylabel("Key Comparisons")
    plt.title("Insertion Sort Comparison")
    plt.grid(axis="y")
    plt.tight_layout()

    filename = os.path.join(
        os.getcwd(), "insertion_sort_comparisons.png"
    )
    plt.savefig(filename, dpi=150)

    print("\nGraph 2 saved at:")
    print(filename)

    plt.show(block=True)
    plt.close()


# 10. MAIN PROGRAM
def main():
    print("=" * 55)
    print("SENTINELOPS SOC ALERT-TRIAGE MODULE")
    print("=" * 55)

    # Test 1: Sorting
    alerts = [
        ("ALERT-1", 3),
        ("ALERT-2", 5),
        ("ALERT-3", 2),
        ("ALERT-4", 5),
        ("ALERT-5", 4)
    ]

    print("\n1. ALERT SORTING")
    for alert_id, severity in sort_alerts(alerts):
        print(alert_id, "Severity:", severity)

    # Test 2: Blocklist
    blocklist = {
        "192.168.1.10",
        "10.0.0.5",
        "172.16.0.8"
    }

    print("\n2. BLOCKLIST CHECK")
    print(
        "Is 10.0.0.5 blocked?",
        is_blocked(blocklist, "10.0.0.5")
    )

    # Test 3: KMP
    log = "login failed; attack detected; login failed"
    pattern = "login failed"

    print("\n3. KMP SIGNATURE MATCHING")
    print("Log:", log)
    print("Pattern:", pattern)
    print("Match positions:", find_signature(log, pattern))

    # Test 4: Closest login locations
    events = [
        (1, 2),
        (8, 9),
        (2, 3),
        (10, 10),
        (1.5, 2.2)
    ]

    pair, distance = closest_logins(events)

    print("\n4. CLOSEST LOGIN LOCATIONS")
    print("Closest pair indices:", pair)
    print("Minimum distance:", round(distance, 4))

    if pair is not None:
        print("First location:", events[pair[0]])
        print("Second location:", events[pair[1]])

    # Test 5: Brute-force comparison
    _, brute_distance, brute_count = (
        brute_force_distance_count(events)
    )
    optimized_count = optimized_distance_count(events)

    print("\n5. ALGORITHM COMPARISON")
    print("Brute-force calculations:", brute_count)
    print("X-sweep calculations:", optimized_count)
    print(
        "Brute-force minimum distance:",
        round(brute_distance, 4)
    )

    # Test 6: Insertion sort
    print("\n6. INSERTION SORT")
    print(
        "Number of key comparisons:",
        insertion_sort_comparisons(alerts)
    )

    # Test 7: Graph generation
    print("\n7. GENERATING GRAPHS")
    generate_closest_pair_graph()
    generate_insertion_sort_graph()

    print("\nBOTH GRAPHS GENERATED SUCCESSFULLY.")
    print("PROGRAM COMPLETED SUCCESSFULLY.")


if __name__ == "__main__":
    main()
```
