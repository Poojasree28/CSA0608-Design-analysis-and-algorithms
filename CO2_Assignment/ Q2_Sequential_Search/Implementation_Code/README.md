## Source Code

```python
import turtle

def sequential_search(records, target):
    comparisons = 0

    for i, record in enumerate(records):
        comparisons += 1

        if record['tool_id'] == target:
            return record, comparisons

    return None, comparisons


if __name__ == '__main__':
    tools = [
        {
            'tool_id': f'T-{i:03}',
            'technician': f'TECH-{i % 4 + 1}',
            'issue_time': '10:00',
            'work_bay': f'BAY-{i % 3 + 1}'
        }
        for i in range(101, 111)
    ]

    targets = ['T-101', 'T-105', 'T-110', 'T-999']
    counts = []

    for target in targets:
        record, count = sequential_search(tools, target)
        print(
            target,
            'FOUND' if record else 'NOT_FOUND',
            'comparisons =', count
        )
        counts.append(count)

    # Create graph window
    screen = turtle.Screen()
    screen.title("Sequential Search Performance")
    screen.setup(900, 600)
    screen.bgcolor("white")

    pen = turtle.Turtle()
    pen.hideturtle()
    pen.speed(0)
    pen.width(3)

    # Graph dimensions
    left = -320
    bottom = -180
    width = 640
    height = 300
    max_count = 10

    # Draw axes
    pen.penup()
    pen.goto(left, bottom)
    pen.pendown()
    pen.goto(left, bottom + height)
    pen.goto(left, bottom)
    pen.goto(left + width, bottom)

    # Graph title
    pen.penup()
    pen.goto(0, 230)
    pen.write(
        "Sequential Search: Key Comparisons",
        align="center",
        font=("Arial", 16, "bold")
    )

    # Axis labels
    pen.goto(0, -240)
    pen.write(
        "Search Target",
        align="center",
        font=("Arial", 12, "normal")
    )

    pen.goto(-400, 150)
    pen.write(
        "Comparisons",
        align="center",
        font=("Arial", 11, "normal")
    )

    # Y-axis scale and grid
    for value in range(0, max_count + 1, 2):
        y = bottom + (value / max_count) * height

        pen
