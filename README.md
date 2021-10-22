# CircuitPython
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython Distance Sensor](#CircuitPython_DistanceSensor)
* [CircuitPython_Photointerrupters](#CircuitPython_Photointerrupters)
* [CircuitPython Lcd](#CircuitPython_Lcd)
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





## CircuitPython_Photointerrupters

### Description & Code
The photointerrupter is a device that uses an led and a sensor to tell when something interupts the light in a small passage and then prints the number or times it is interrupted
```python
from digitalio import DigitalInOut, Direction, Pull
import time
import board

interrupter = DigitalInOut(board.D7)
interrupter.direction = Direction.INPUT
interrupter.pull = Pull.UP
initial = time.monotonic()  # Time in seconds since power on

counter = 0

photo = False
state = False

max = 4
start = time.monotonic()

while True:
    photo = interrupter.value
    if photo and not state:
        counter += 1
    state = photo

    remaining = max + start - time.monotonic()

    if remaining <= 0:
        print("The number of interrupts is:", str(counter))
        max = time.monotonic() + 4
        counter = 0

```

### Evidence
![Picture of the code working](https://github.com/nmckee78/CircuitPython/blob/main/Pictures/Photointerrupter%20Screenshot.PNG)
### Wiring
![This is obviously not the actual photointerrupter but as there is no photointerrupter on tinkercad this is the best equivalent,it uses the same ports as the photointerrupter aswell](https://github.com/nmckee78/CircuitPython/blob/main/Pictures/Ingenious%20Wluff-Jaiks.png)
### Reflection
The photointerrupter was not incredibly complicated however there were a few important things, including making sure the two wires going to 5 volt are duct taped together and not touching the other wires. Also this was the final straw of my use of the MU software as it was causing me serious issues and I switched over to VS code which got it working.





## CircuitPython_Lcd

### Description & Code
The lcd was supposed to be able to print when the capacitive touch was triggered printing the number of times it was touched and then the other capacitive touch wire telling it to swich from counting up to counting down into the negatives
```python
import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import time
import touchio

i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)

touch_a5 = board.A5
touch_A5 = touchio.TouchIn(touch_a5)
touch_a0 = board.A0
touch_A0 = touchio.TouchIn(touch_a0)

count = 0
updown = 1

while True:
    if touch_A5.value:
        count += updown
        lcd.clear()
        if updown == 1:
            lcd.print("Up: ")
        else:
            lcd.print("Down: ")
        lcd.print(str(count))
        while touch_A5.value:
            time.sleep(0.01)
    if touch_A0.value:
        updown = -updown
        while touch_A0.value:
            time.sleep(0.1)
        lcd.clear()
        if updown == 1:
            lcd.print("Up: ")
        else:
            lcd.print("Down: ")
        lcd.print(str(count))


```

### Evidence
![Picture of the code working](https://github.com/nmckee78/CircuitPython/blob/main/Gif%20folder/ezgif.com-gif-maker%20(3).gif)
### Wiring
![This is simply a represantition of the code as there is no Lcd backapack in tinkercad](https://github.com/nmckee78/CircuitPython/blob/main/Pictures/Fantabulous%20Waasa.png)
### Reflection
This one was fairly easy as most of the code is the same concept as the capacitive touch code and just replacing print with printing it on the lcd and a little bit of math it is fairly straightforward.

