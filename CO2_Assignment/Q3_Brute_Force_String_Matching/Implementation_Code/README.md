## Source Code

```python
import turtle

def brute_force_match(text, pattern):
    comparisons = 0

    for shift in range(len(text) - len(pattern) + 1):
        j = 0

        while j < len(pattern):
            comparisons += 1

            if text[shift + j] != pattern[j]:
                break

            j += 1

        if j == len(pattern):
            return shift, comparisons

    return -1, comparisons


# Test cases
tests = [
    ('security-alert', 'sec'),
    ('AAAAAAAAAAAB', 'AAAAB'),
    ('AAAAAAAAAA', 'AAAB')
]

counts = []

for text, pattern in tests:
    index, count = brute_force_match(text, pattern)
    print(repr(text), repr(pattern),
          'index =', index, 'comparisons =', count)
    counts.append(count)


# Draw graph using turtle
screen = turtle.Screen()
screen.title("Brute Force String Matching")
screen.setup(900, 600)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.hideturtle()
pen.speed(0)
pen.width(2)

left = -320
bottom = -180
graph_width = 640
graph_height = 300
max_count = max(counts) + 2


# Draw axes
pen.penup()
pen.goto(left, bottom)
pen.pendown()
pen.goto(left, bottom + graph_height)
pen.goto(left, bottom)
pen.goto(left + graph_width, bottom)


# Title
pen.penup()
pen.goto(0, 230)
pen.write("Brute Force String Matching",
          align="center", font=("Arial", 16, "bold"))


# Axis labels
pen.goto(0, -245)
pen.write("Test Cases", align="center",
          font=("Arial", 12, "normal"))

pen.goto(-400, 150)
pen.write("Comparisons", align="center",
          font=("Arial", 11, "normal"))


# Y-axis markings and grid
for value in range(0, max_count + 1, 2):
    y = bottom + value / max_count * graph_height

    pen.penup()
    pen.goto(left - 15, y - 5)
    pen.write(str(value), align="right",
              font=("Arial", 10, "normal"))

    pen.goto(left, y)
    pen.color("lightgray")
    pen.pendown()
    pen.goto(left + graph_width, y)
    pen.penup()
    pen.color("black")


# Draw bars
labels = ["Test 1", "Test 2", "Test 3"]
colors = ["blue", "orange", "green"]
bar_width = 100
gap = 105

for i, count in enumerate(counts):
    x = left + 35 + i * (bar_width + gap)
    bar_height = count / max_count * graph_height

    pen.penup()
    pen.goto(x, bottom)
    pen.color(colors[i])
    pen.pendown()
    pen.begin_fill()
    pen.goto(x + bar_width, bottom)
    pen.goto(x + bar_width, bottom + bar_height)
    pen.goto(x, bottom + bar_height)
    pen.goto(x, bottom)
    pen.end_fill()

    pen.penup()
    pen.color("black")
    pen.goto(x + bar_width / 2, bottom + bar_height + 8)
    pen.write(str(count), align="center",
              font=("Arial", 11, "bold"))

    pen.goto(x + bar_width / 2, bottom - 25)
    pen.write(labels[i], align="center",
              font=("Arial", 11, "normal"))


turtle.done()
```

