## Source Code

```python
import turtle


def cross(a, b, p):
    return ((b[0] - a[0]) * (p[1] - a[1])
            - (b[1] - a[1]) * (p[0] - a[0]))


def brute_force_hull_edges(points):
    edges = []
    n = len(points)

    for i in range(n):
        for j in range(i + 1, n):
            positive = negative = False

            for k in range(n):
                if k == i or k == j:
                    continue

                z = cross(points[i], points[j], points[k])

                if z > 0:
                    positive = True
                elif z < 0:
                    negative = True

                if positive and negative:
                    break

            if not (positive and negative):
                edges.append((points[i], points[j]))

    return edges


pts = [(0, 0), (4, 0), (4, 4),
       (0, 4), (2, 2), (1, 2)]

edges = brute_force_hull_edges(pts)

print("Supporting-line candidate edges:")
for edge in edges:
    print(edge)


# Draw graph using turtle
screen = turtle.Screen()
screen.title("Brute Force Convex Hull")
screen.setup(800, 650)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()
pen.width(3)


def convert(p):
    return (p[0] * 80 - 160, p[1] * 80 - 120)


# Draw coordinate axes
pen.penup()
pen.color("gray")
pen.goto(-200, -140)
pen.pendown()
pen.goto(240, -140)

pen.penup()
pen.goto(-200, -140)
pen.pendown()
pen.goto(-200, 240)


# Draw hull boundary edges
pen.color("red")
pen.width(4)

for a, b in edges:
    pen.penup()
    pen.goto(convert(a))
    pen.pendown()
    pen.goto(convert(b))


# Draw and label all points
for p in pts:
    x, y = convert(p)
    pen.penup()
    pen.goto(x, y)
    pen.dot(12, "blue")
    pen.goto(x + 10, y + 8)
    pen.color("black")
    pen.write(str(p), font=("Arial", 11, "normal"))


# Title and legend
pen.penup()
pen.goto(0, 260)
pen.write("Brute Force Convex Hull",
          align="center", font=("Arial", 17, "bold"))

pen.goto(-100, -210)
pen.color("red")
pen.write("Red: Hull edges",
          align="center", font=("Arial", 12, "normal"))

pen.goto(120, -210)
pen.color("blue")
pen.write("Blue: Points",
          align="center", font=("Arial", 12, "normal"))

turtle.done()
```

