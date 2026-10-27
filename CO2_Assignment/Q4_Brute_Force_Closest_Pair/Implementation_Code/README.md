## Source Code

```python
from math import hypot, inf
import turtle


def closest_pair(points):
    best_distance = inf
    best_pair = None
    pair_count = 0

    for i in range(len(points) - 1):
        for j in range(i + 1, len(points)):
            pair_count += 1
            d = hypot(points[i][0] - points[j][0],
                      points[i][1] - points[j][1])

            if d < best_distance:
                best_distance = d
                best_pair = (points[i], points[j])

    return best_pair, best_distance, pair_count


points = [(0, 0), (5, 5), (2, 2), (9, 1), (2, 3)]

pair, distance, count = closest_pair(points)

print("Closest pair:", pair)
print("Minimum distance:", round(distance, 2))
print("Pairs checked:", count)


# Draw graph using turtle
screen = turtle.Screen()
screen.title("Closest Pair of Points")
screen.setup(800, 650)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()


# Coordinate mapping
def screen_point(p):
    return (p[0] * 45 - 200, p[1] * 45 - 150)


# Draw coordinate axes
pen.penup()
pen.goto(-250, -170)
pen.pendown()
pen.goto(250, -170)

pen.penup()
pen.goto(-250, -170)
pen.pendown()
pen.goto(-250, 230)


# Axis labels and title
pen.penup()
pen.goto(0, 250)
pen.write("Closest Pair of Points",
          align="center", font=("Arial", 16, "bold"))

pen.goto(0, -210)
pen.write("X-axis", align="center", font=("Arial", 11, "normal"))

pen.goto(-300, 220)
pen.write("Y-axis", align="center", font=("Arial", 11, "normal"))


# Draw all points
for p in points:
    x, y = screen_point(p)
    pen.penup()
    pen.goto(x, y)
    pen.dot(10, "blue")
    pen.goto(x + 8, y + 8)
    pen.write(str(p), font=("Arial", 10, "normal"))


# Highlight closest pair
pen.color("red")
pen.width(3)

p1, p2 = pair
pen.penup()
pen.goto(screen_point(p1))
pen.pendown()
pen.goto(screen_point(p2))


# Draw information
pen.penup()
pen.goto(0, -270)
pen.color("red")
pen.write("Minimum distance = " + str(round(distance, 2)),
          align="center", font=("Arial", 12, "bold"))

turtle.done()
```

