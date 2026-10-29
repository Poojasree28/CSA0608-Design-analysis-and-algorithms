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
