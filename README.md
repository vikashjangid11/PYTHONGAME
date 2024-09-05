import pgzrun
import random

WIDTH = 800
HEIGHT = 500

# Snake settings
snake = [(40, 10)]
direction = "RIGHT"
score = 0

# Food settings
food = (random.randint(0, WIDTH // 20) * 20, random.randint(0, HEIGHT // 20) * 20)

def draw():
    screen.clear()
    screen.fill("light blue")
    for segment in snake:
        screen.draw.filled_rect(Rect(segment, (20, 20)), "gray")
    screen.draw.filled_circle(food, 10, "red")
    screen.draw.text(f"Score: {score}", (10, 10), fontsize=30, color="black")

def update():
    global food, score
    move_snake()
    if snake[0] == food:
        score += 1
        snake.append(snake[-1])
        food = (random.randint(0, WIDTH // 20) * 20, random.randint(0, HEIGHT // 20) * 20)

def move_snake():
    global direction
    x, y = snake[0]
    if direction == "UP":
        y -= 20
    elif direction == "DOWN":
        y += 20
    elif direction == "LEFT":
        x -= 20
    elif direction == "RIGHT":
        x += 20
    snake.insert(0, (x, y))
    snake.pop()

def on_key_down(key):
    global direction
    if key == keys.W and direction != "DOWN":
        direction = "UP"
    elif key == keys.S and direction != "UP":
        direction = "DOWN"
    elif key == keys.A and direction != "RIGHT":
        direction = "LEFT"
    elif key == keys.D and direction != "LEFT":
        direction = "RIGHT"

pgzrun.go()
