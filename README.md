# CherSoft lander challenge
## v1.0

Your mission is to land a rocket back on Earth.
You will write a program to control the throttle using just your instruments.![An artist's impression of your rocket in flight.](https://i.snag.gy/zCVnMt.jpg)
*An artist's impression of your rocket in flight.*

|Performance data|  |
|--|--|
|Maximum thrust|1200 kN
|Maximum throttle change per second|10%
|Empty mass|5000 kg
|Fuel flow (at full throttle)|50 kg / s

There are 3 scenarios to play. The judge immediately starts the next scenario when the last one ends (be it through landing or crashing)

|Level|Altitude (m)|Initial speed (m/s)|Fuel available|
|--|--|--|--|
|1|500|0|20 sec (1000 kg)|
|2|30000|500|30 sec (1500 kg)|
|3|35867000|0|550 sec (27500 kg)|

## Getting started
The judge application, Lander.exe, is a console app. You issue commands to it on stdin and receive instrument data on stdout. 
Every tick you'll receive an update (on stdout) with the current situation of the rocket, that looks like this:

````
0 | Lander ID : 1
1 | Status : Flying
2 | g (m/s/s) : 9.8
3 | Time (s) : 0.0625
4 | Altitude (m) : 499.980859375
5 | Vertical speed (m/s) : -0.6125
6 | Mass (kg) : 6000
7 | Fuel remaining (kg) : 1000
8 | Engine thrust (kN) : 0
9 | Commanded throttle (%) : 0
?
````

The ? prompt is asking you to enter a value on stdin.

Typing a blank line will continue the simulation. Typing a number between 0 and 1 sets the throttle demand to that value (0 = off, 1 = full throttle).

Lines that start with "#" are log messages. You'll receive your victory code this way (if you get one!)

You can actually try this out without writing a program. Run the judge application and hit enter until your altitude is about 390 m. Then type ```1``` followed by return. After stepping the simulation a few more times you should see your thrust increasing and your vertical speed begin to decrease. Now you just need to turn it off at the right time :)
## Connecting your program to the judge
There are 2 options:
1. Spawn the judge process from your program.
2. Start the judge process, passing the path to your program as an argument.

Either should work.

## Important points
- There is no drag simulation (just thrust and gravity).
- Standard gravity at 0 m is 9.8 m/s^2.
- The simulation runs at a variable time step (up to 16 Hz depending on altitude).
- Note that throttle changes aren't instantaneous, it takes some time for your engine to reach full throttle.

## How to win
Any landing at less than 5 m/s impact speed will be considered good.

If you land at least one rocket, you'll receive a victory hash when the program finishes.
```
# Level 1: Landed, 2.1 m/s touchdown after 18.69 s with 95.44% fuel remaining
# Level 2: Landed, 3.14 m/s touchdown after 58.44 s with 81.06% fuel remaining
# Level 3: Landed, 1.16 m/s touchdown after 3010.31 s with 16.39% fuel remaining
# You landed 3 out of 3 rockets
# Victory! Here is your hash: ThisIsN0trEalx4eHgsMC451x/3YxLjAsMSwwLjEseHh4LDMsLDAuMTYseHMC45NSMTguNjksMiwwLjEBnX4CkB56vF0LDU4Lj1mDpZuODEsQ0LDA4xNiwzMDEwLjMxh4
```
Hold on to that for now, I'll probably make a leaderboard at some point.

Tie breakers are
- Softest touchdown
- Shortest time to land
- Fuel remaining

The overall winner is the person who wins the most levels.

**Good luck!**
