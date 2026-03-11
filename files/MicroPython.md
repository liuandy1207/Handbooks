# MicroPython

## Table of Contents

>

<hr>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

## `digitialio` Module

- Provides access to basic digital IO.

```python
import time
import digitalio
import board

# blinky example
# initialize a specific pin, in this case, the onboard LED
led = digitalio.DigitalInOut(board.LED)     # access through the board module
led.direction = digitalio.Direction.OUTPUT  # set pin direction
while True:
    led.value = True    # set to HIGH
    time.sleep(0.1)     # delay for 0.1 s
    led.value = False   # set to LOW
    time.sleep(0.1)     # delay for 0.1 s

# pull up/down an input pin
pin.Pull.UP
pin.Pull.DOWN
```
