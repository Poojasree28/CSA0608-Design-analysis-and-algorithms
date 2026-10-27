## Source Code

```python
import random
import turtle

def selection_sort(a):
    c = 0
    for i in range(len(a) - 1):
        m = i
        for j in range(i + 1, len(a)):
            c += 1
            if a[j] < a[m]:
                m = j
        a[i], a[m] = a[m], a[i]
    return c

def bubble_sort(a):
    c = 0
    for end in range(len(a) - 1, 0, -1):
        changed = False
        for j in range(end):
            c += 1
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                changed = True
        if not changed:
            break
    return c

def insertion_sort(a):
    c = 0
    for i in range(1, len(a)):
        key = a[i]
        j = i - 1
        while j >= 0:
            c += 1
            if a[j] > key:
                a[j + 1] = a[j]
                j -= 1
            else:
                break
        a[j + 1] = key
    return c

sizes = [10, 50, 100, 200]
sel, bub, ins = [], [], []

random.seed(42)

for n in sizes:
    data = [random.randint(1, 10000) for _ in range(n)]
    sel.append(selection_sort(data.copy()))
    bub.append(bubble_sort(data.copy()))
    ins.append(insertion_sort(data.copy()))

print("Input sizes:", sizes)
print("Selection:", sel)
print("Bubble:", bub)
print("Insertion:", ins)

# Draw graph using turtle
screen = turtle.Screen()
screen.title("Sorting Algorithm Comparisons")
screen.setup(1000, 650)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()
pen.width(3)

left, bottom = -400, -230
graph_width, graph_height = 800, 430
max_value = max(sel + bub + ins) * 1.1

# Draw axes
pen.penup()
pen.goto(left, bottom)
pen.pendown()
pen.goto(left, bottom + graph_height)
pen.goto(left, bottom)
pen.goto(left + graph_width, bottom)

# Axis labels
pen.penup()
pen.goto(0, -290)
pen.write("Input size n", align="center",
          font=("Arial", 14, "normal"))

pen.goto(-450, 230)
pen.write("Comparisons", align="center",
          font=("Arial", 12, "normal"))

# X-axis labels
for n in sizes:
    x = left + (n / 200) * graph_width
    pen.penup()
    pen.goto(x, bottom - 25)
    pen.write(str(n), align="center",
              font=("Arial", 10, "normal"))

# Y-axis labels and grid
for k in range(5):
    value = max_value * k / 4
    y = bottom + graph_height * k / 4
    pen.penup()
    pen.goto(left - 12, y - 5)
    pen.write(str(int(value)), align="right",
              font=("Arial", 9, "normal"))
    pen.goto(left, y)
    pen.pendown()
    pen.goto(left + graph_width, y)
    pen.penup()

def draw_line(values, color, name):
    pen.color(color)
    pen.width(3)
    for i, n in enumerate(sizes):
        x = left + (n / 200) * graph_width
        y = bottom + (values[i] / max_value) * graph_height
        if i == 0:
            pen.penup()
            pen.goto(x, y)
            pen.pendown()
        else:
            pen.goto(x, y)
        pen.dot(9)

# Draw three sorting lines
draw_line(sel, "blue", "Selection")
draw_line(bub, "orange", "Bubble")
draw_line(ins, "green", "Insertion")

# Graph title
pen.penup()
pen.goto(0, 270)
pen.color("black")
pen.write("Q1: Comparisons on random data",
          align="center",
          font=("Arial", 18, "normal"))

# Legend
for i, (color, name) in enumerate([
    ("blue", "Selection"),
    ("orange", "Bubble"),
    ("green", "Insertion")
]):
    pen.goto(260, 240 - i * 25)
    pen.color(color)
    pen.pendown()
    pen.forward(25)
    pen.penup()
    pen.forward(8)
    pen.color("black")
    pen.write(name, font=("Arial", 11, "normal"))

turtle.done()
```
