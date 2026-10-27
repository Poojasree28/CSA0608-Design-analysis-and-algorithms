## Source Code

```python
from math import hypot, inf
import turtle

def divide_closest(points):
    points = sorted(points, key=lambda p: (p[0], p[1]))

    if len(points) <= 3:
        best = inf
        pair = None
        count = 0

        for i in range(len(points)):
            for j in range(i + 1, len(points)):
                count += 1
                d = hypot(points[i][0] - points[j][0],
                          points[i][1] - points[j][1])
                if d < best:
                    best, pair = d, (points[i], points[j])

        return pair, best, count

    mid = len(points) // 2
    mid_x = points[mid][0]

    lp, ld, lc = divide_closest(points[:mid])
    rp, rd, rc = divide_closest(points[mid:])

    if ld <= rd:
        best, pair = ld, lp
    else:
        best, pair = rd, rp

    count = lc + rc

    strip = sorted(
        [p for p in points if abs(p[0] - mid_x) < best],
        key=lambda p: p[1]
    )

    for i in range(len(strip)):
        j = i + 1
        while j < len(strip) and strip[j][1] - strip[i][1] < best:
            count += 1
            d = hypot(strip[i][0] - strip[j][0],
                      strip[i][1] - strip[j][1])
            if d < best:
                best, pair = d, (strip[i], strip[j])
            j += 1

    return pair, best, count


# Input points
points = [(0, 0), (5, 5), (2, 2), (9, 1), (2, 3)]

pair, distance, comparisons = divide_closest(points)

print("Points:", points)
print("Closest pair:", pair)
print("Minimum distance:", round(distance, 2))
print("Distance comparisons:", comparisons)


# Draw graph using turtle
screen = turtle.Screen()
screen.title("Divide and Conquer - Closest Pair")
screen.setup(800, 650)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()
pen.width(3)


def convert(p):
    return (p[0] * 45 - 200, p[1] * 45 - 150)


# Draw axes
pen.color("gray")
pen.penup()
pen.goto(-220, -170)
pen.pendown()
pen.goto(250, -170)

pen.penup()
pen.goto(-220, -170)
pen.pendown()
pen.goto(-220, 240)


# Draw points
for p in points:
    x, y = convert(p)
    pen.penup()
    pen.goto(x, y)
    pen.dot(12, "blue")
    pen.goto(x + 8, y + 8)
    pen.color("black")
    pen.write(str(p), font=("Arial", 10, "normal"))


# Highlight closest pair
pen.color("red")
pen.width(4)
pen.penup()
pen.goto(convert(pair[0]))
pen.pendown()
pen.goto(convert(pair[1]))


# Title and result
pen.penup()
pen.goto(0, 270)
pen.color("black")
pen.write(
    "Divide and Conquer: Closest Pair",
    align="center",
    font=("Arial", 16, "bold")
)

pen.goto(0, -220)
pen.color("red")
pen.write(
    "Red line = Closest pair; Distance = " + str(round(distance, 2)),
    align="center",
    font=("Arial", 11, "normal")
)

turtle.done()
```

