# CircuitPython
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [NextAssignmentGoesHere](#NextAssignment)
---

## Hello_CircuitPython

### Description & Code
This was the first thing I did with circuitpython and I got the light to blink and change between bright pink and blue

This is my code:

```python
import board
import neopixel
import time

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)

print("Make it red!")

dot.brightness = 0.3
while True:
    dot.fill((255, 0, 191))
    time.sleep(0.5)
    dot.fill((100,0,255))
    time.sleep(0.5)

```


### Evidence
 ![This is the gif of it working](https://github.com/nmckee78/CircuitPython/blob/main/Gif%20folder/ezgif.com-gif-maker.gif)

### Wiring
There wasn't any wiring needed.

### Reflection
It took me a bit of time how circuitpython works but once I figured out how to import different things it was fairly easy.




## CircuitPython_Servo

### Description & Code
 The Servo assignment was basically to get a servo working with circuit python and also to add a capacitive touch aswell.
```python
import time
import board
import pwmio
import touchio

from adafruit_motor import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)


touch_pad = board.A0  # Will not work for Circuit Playground Express!
touch_pad = board.A5
touch_A0 = touchio.TouchIn(board.A0)
touch_A5 = touchio.TouchIn(board.A5)

while True:
    if touch_A0.value:
        print("Touched 1!")
        for angle in range(180, 0, -5): # 180 - 0 degrees, 5 degrees at a time.
                my_servo.angle = angle
                time.sleep(0.05)# Write your code here :-)
    if touch_A5.value:
        print("Touched 2!")
        for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
                my_servo.angle = angle
                time.sleep(0.05)


```

### Evidence
 ![This is the gif of it working](https://github.com/nmckee78/CircuitPython/blob/main/Gif%20folder/ezgif.com-gif-maker%20(1).gif)

    
### Wiring
![Picture of the wiring](https://github.com/nmckee78/CircuitPython/blob/main/Pictures/Brilliant%20Vihelmo-Bigery.png)
### Reflection
I had some trouble getting the code and wiring to work as the insturctions on the code website was a bit confusing but with a bit of help I managed to figure it out



## CircuitPython_DistanceSensor

### Description & Code
 The distance sensor is used to change the color from red then fades to blue then fades to green
```python
import time
import board
import adafruit_hcsr04
import neopixel
import simpleio

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
dot = neopixel.NeoPixel(board.NEOPIXEL, 10, brightness=0.5)

r = 0
g = 0
b = 0


while True:

    try:
        distance = sonar.distance
        print((distance,))

        if distance < 5:
            r = 255
            g = 0
            b = 0
        elif distance > 5 and distance < 20:
            r = simpleio.map_range(distance, 5, 20, 255, 0)
            b = simpleio.map_range(distance, 5, 20, 0, 255)
            g = 0
            r = int(r)
            g = int(g)
            b = int(b)
        elif distance > 20 and distance < 35:
            r = 0
            b = simpleio.map_range(distance, 20, 35, 255, 0)
            g = simpleio.map_range(distance, 20, 35, 0, 255)
            r = int(r)
            g = int(g)
            b = int(b)
        elif distance > 35:
            r = 0
            b = 0
            g = 255
            r = int(r)
            g = int(g)
            b = int(b)
        print(r, g, b)
        time.sleep(0.05)

    except RuntimeError:
        print("Retrying!")
        r = 0
        g = 0
        b = 255
        time.sleep(0.1)

    print(r, g, b)
    dot.fill((r, g, b))
    time.sleep(0.05)


```

### Evidence
![This is the gif of it working](https://github.com/nmckee78/CircuitPython/blob/main/Gif%20folder/ezgif.com-gif-maker%20(2).gif)

### Wiring
![Picture of the wiring](https://github.com/nmckee78/CircuitPython/blob/main/Pictures/Smashing%20Esboo-Snicket.png)
### Reflection
This one was very hard to figure out because first I had to figure out how to wire the distance sensor correctly. Then I had to figure out the rgb values and figure out the correct ranges and formulas to work. This was also with Mu and circuitPython being very wierd the whole time. Then I messed up the error message for it not working at the end which took another think to figure out.





## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection
