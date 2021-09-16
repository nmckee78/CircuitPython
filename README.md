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
 ![This is the gif of it working](https://github.com/nmckee78/CircuitPython/blob/main/ezgif.com-gif-maker.gif)

### Wiring
There wasn't any wiring needed.

### Reflection
It took me a bit of time how circuitpython works but once I figured out how to import different things it was fairly easy.




## CircuitPython_Servo

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring
Make an account with your google ID at [tinkercad.com](https://www.tinkercad.com/learn/circuits), and use "TinkerCad Circuits to make a wiring diagram."  It's really easy!  
Then post an image here.   [here's a quick tutorial for all markdown code, like making links](https://guides.github.com/features/mastering-markdown/)
### Reflection




## CircuitPython_LCD

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection





## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection
