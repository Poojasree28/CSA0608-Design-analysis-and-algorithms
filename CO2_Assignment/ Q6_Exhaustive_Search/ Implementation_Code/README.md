## Source Code

```python
import turtle

def exhaustive_packing(packages, capacity):
    n = len(packages)
    best_value = -1
    best_weight = 0
    best_mask = 0

    for mask in range(1 << n):
        weight = value = 0

        for i, (w, v) in enumerate(packages):
            if mask & (1 << i):
                weight += w
                value += v

        if weight <= capacity and value > best_value:
            best_value = value
            best_weight = weight
            best_mask = mask

    chosen = [i for i in range(n)
              if best_mask & (1 << i)]

    return chosen, best_weight, best_value


packages = [(2, 6), (3, 8), (4, 9), (5, 10)]
capacity = 7

chosen, weight, value = exhaustive_packing(packages, capacity)

print("Chosen package indices:", chosen)
print("Total weight:", weight)
print("Total value:", value)
print("Capacity:", capacity)


# Draw graph using turtle
screen = turtle.Screen()
screen.title("Exhaustive Packing - Knapsack")
screen.setup(850, 600)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()

# Graph settings
left = -300
bottom = -170
bar_width = 100
gap = 65
scale = 25

# Title
pen.penup()
pen.goto(0, 230)
pen.write("0/1 Knapsack: Package Values",
          align="center", font=("Arial", 17, "bold"))

# Axes
pen.goto(left, bottom)
pen.pendown()
pen.goto(left, bottom + 300)
pen.goto(left, bottom)
pen.goto(300, bottom)
pen.penup()

# Axis labels
pen.goto(0, -220)
pen.write("Packages", align="center",
          font=("Arial", 12, "normal"))

pen.goto(-370, 170)
pen.write("Value", align="center",
          font=("Arial", 12, "normal"))

# Draw bars for each package
for i, (w, v) in enumerate(packages):
    x = left + 35 + i * (bar_width + gap)
    bar_height = v * scale
    color = "green" if i in chosen else "lightblue"

    pen.goto(x, bottom)
    pen.color(color)
    pen.pendown()
    pen.begin_fill()
    pen.goto(x + bar_width, bottom)
    pen.goto(x + bar_width, bottom + bar_height)
    pen.goto(x, bottom + bar_height)
    pen.goto(x, bottom)
    pen.end_fill()

    # Package value label
    pen.penup()
    pen.goto(x + bar_width / 2, bottom + bar_height + 8)
    pen.color("black")
    pen.write(str(v), align="center",
              font=("Arial", 12, "bold"))

    # Package name and weight
    pen.goto(x + bar_width / 2, bottom - 25)
    pen.write("P" + str(i + 1),
              align="center", font=("Arial", 11, "normal"))

    pen.goto(x + bar_width / 2, bottom - 43)
    pen.write("W=" + str(w),
              align="center", font=("Arial", 10, "normal"))

pen.goto(0, -260)
pen.color("green")
pen.write("Green = Selected | Blue = Not selected",
          align="center", font=("Arial", 11, "normal"))

turtle.done()
```

