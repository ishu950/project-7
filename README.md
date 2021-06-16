# project-7
pon game

## mainpy

from turtle import Turtle,Screen
from paddle import Paddle
from ball import Ball
from score import Scoreboard
import time
screen = Screen()
screen.setup(width=800,height=600)
screen.bgcolor("black")
screen.title("PONG")
screen.tracer(0)

ball = Ball()
scoreboard=Scoreboard()

r_paddle = Paddle((350, 0))
l_paddle = Paddle((-350, 0))

screen.listen()
screen.onkey(r_paddle.go_up, "u")
screen.onkey(r_paddle.go_down, "d")
screen.onkey(l_paddle.go_up, "r")
screen.onkey(l_paddle.go_down, "l")



game_is_on = True
while game_is_on:
    time.sleep(ball.move_speed)
    screen.update()
    ball.move()

    if ball.ycor() > 280 or ball.ycor() < -280:
        ball.y_bounce()


    if ball.distance(r_paddle) < 50 and ball.xcor() >320 or ball.distance(l_paddle) < 50 and ball.xcor() < -320 :
        ball.x_bounce()

    if ball.xcor()  > 380 :
        ball.refresh()
        scoreboard.l_point()
    if ball.xcor() < -380:
        ball.refresh()
        scoreboard.r_point()



screen.exitonclick()














## paddle

from turtle import Turtle

class Paddle(Turtle):

    def __init__(self, position):
        super().__init__()
        self.shape("square")
        self.color("white")
        self.shapesize(stretch_wid=5, stretch_len=1)
        self.penup()
        self.goto(position)

    def go_up(self):
        new_y = self.ycor() + 20
        self.goto(self.xcor(), new_y)


    def go_down(self):
        new_y = self.ycor() - 20
        self.goto(self.xcor(), new_y)
        
        
        
        
        
 ### ball
 from turtle import Turtle

class Ball(Turtle):

    def __init__(self):
        super().__init__()
        self.shape("circle")
        self.color("White")
        self.penup()
        self.goto(0, 0)
        self.y_move = 10
        self.x_move = 10
        self.move_speed = 0.1

    def move(self):
        new_x = self.xcor() + self.x_move
        new_y = self.ycor() + self.y_move
        self.goto(new_x, new_y)

    def y_bounce(self):
        self.y_move *= -1


    def x_bounce(self):
        self.x_move *= -1
        self.move_speed *= 0.9

    def refresh(self):
        self.goto(0,0)

        self.move_speed=0.1
        self.x_bounce()
        
        
        
        ### score
        
        from turtle import Turtle


class Scoreboard(Turtle):


    def __init__(self):
        super().__init__()
        self.color("white")
        self.penup()
        self.hideturtle()
        self.l_score = 0
        self.r_score = 0
        self.update_scoreboard()


    def update_scoreboard(self):
        self.clear()
        self.goto(-100, 200)
        self.write(self.l_score, align="center", font=("Courier",30,"normal") )
        self.goto(100,200)
        self.write(self.r_score, align="center", font=("Courier", 30, "normal"))

    def l_point(self):
        self.l_score += 1
        self.update_scoreboard()
    def r_point(self):
        self.r_score += 1
        self.update_scoreboard()
        
        
        
        
        
 
