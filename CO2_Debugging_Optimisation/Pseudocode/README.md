# Corrected Algorithms: Pseudocode

## 1. Corrected Stable Insertion Sort

```text
PROCEDURE CorrectedSortAlerts(alerts)

    FOR i FROM 1 TO length(alerts) - 1
        key ← alerts[i]
        j ← i - 1

        WHILE j >= 0 AND alerts[j].severity < key.severity
            alerts[j + 1] ← alerts[j]
            j ← j - 1
        END WHILE

        alerts[j + 1] ← key
    END FOR

    RETURN alerts

END PROCEDURE
```

## 2. Corrected Sequential Blocklist Search

```text
PROCEDURE CorrectedIsBlocked(blocklist, ip)

    FOR each address IN blocklist
        IF address = ip
            RETURN TRUE
        END IF
    END FOR

    RETURN FALSE

END PROCEDURE
```

## 3. Corrected Brute-Force Signature Matching

```text
PROCEDURE CorrectedFindSignature(log, pattern)

    IF pattern is empty
        RETURN every boundary position from 0 through length(log)
    END IF

    n ← length(log)
    m ← length(pattern)
    hits ← empty list

    FOR start FROM 0 TO n - m inclusive
        j ← 0

        WHILE j < m AND log[start + j] = pattern[j]
            j ← j + 1
        END WHILE

        IF j = m
            append start to hits
        END IF
    END FOR

    RETURN hits

END PROCEDURE
```

## 4. Corrected Brute-Force Closest Pair

```text
PROCEDURE CorrectedClosestLogins(events)

    IF length(events) < 2
        RETURN (None, infinity)
    END IF

    bestDistance ← infinity
    bestPair ← None

    FOR i FROM 0 TO length(events) - 1
        FOR j FROM i + 1 TO length(events) - 1
            distance ← EuclideanDistance(events[i], events[j])

            IF distance < bestDistance
                bestDistance ← distance
                bestPair ← (i, j)
            END IF
        END FOR
    END FOR

    RETURN (bestPair, bestDistance)

END PROCEDURE
```


# Optimized Pseudocode

The corrected versions first establish correctness with straightforward algorithms. The production-oriented versions then use data structures and pruning to reduce repeated work. The outputs and tie/stability rules remain consistent.



## 1. Optimised Sorting (Stable Adaptive Sort)

```text id="9x4k2p"
PROCEDURE OptimisedSortAlerts(alerts)

    IF alerts is empty
        RETURN empty list
    END IF

    Sort alerts by severity in descending order
    Preserve the original order of alerts with equal severity
    Use a stable adaptive sorting algorithm

    RETURN sorted alerts

END PROCEDURE
```


## 2. Optimised Blocklist Lookup

```text id="q7m2vd"
PROCEDURE PrepareBlocklist(blocklist)

    Create an empty set called blockedSet

    FOR each IP address in blocklist
        Add IP address to blockedSet
    END FOR

    RETURN blockedSet

END PROCEDURE


PROCEDURE OptimisedIsBlocked(blockedSet, ip)

    IF ip exists in blockedSet
        RETURN TRUE
    ELSE
        RETURN FALSE
    END IF

END PROCEDURE
```

## 3. Optimised Signature Matching (KMP)

```text
PROCEDURE OptimisedFindSignature(log, pattern)

    IF pattern is empty
        RETURN all boundary positions
    END IF

    Build LPS table for pattern

    i ← 0
    j ← 0
    hits ← empty list

    WHILE i < length(log)

        IF log[i] = pattern[j]

            i ← i + 1
            j ← j + 1

            IF j = length(pattern)

                append i - j to hits
                j ← LPS[j - 1]  // allows overlapping matches

            END IF

        ELSE IF j > 0

            j ← LPS[j - 1]  // do not move i backwards

        ELSE

            i ← i + 1

        END IF

    END WHILE

    RETURN hits

END PROCEDURE
```

## 4. Optimised Closest Pair (X-Sweep Pruning)

```text
PROCEDURE OptimisedClosestLogins(events)

    IF fewer than two events
        RETURN (None, infinity)
    END IF

    Sort (x, y, originalIndex) points by x

    bestSquared ← infinity
    bestPair ← None

    FOR each point p in sorted points

        FOR each later point q

            dx ← q.x - p.x

            IF dx * dx >= bestSquared
                BREAK  // later x values cannot improve result
            END IF

            dSquared ← dx * dx + (q.y - p.y) * (q.y - p.y)

            IF dSquared < bestSquared

                bestSquared ← dSquared
                bestPair ← (p.originalIndex, q.originalIndex)

            END IF

        END FOR

    END FOR

    RETURN (bestPair, sqrt(bestSquared))

END PROCEDURE
```

