# Grok Notes

## General Python

### Variables
Variables are used to store a value throughout a piece of code. For example, look at the below example:
```python
print('Hello James!')
print('I know that you are called James.')
print('I am reading your mind James.')
```
But what if you want to change James to someone else's name? You'll have to go through and hcange it 3 times.
A variable, solves this issue, look at the below example:
```python
name = "James"
print('Hello ' + name + '!')
print('I know that you are called ' + name + '.')
print('I am reading your mind ' + name + '.')
```

#### Types of Variables
In Python there are a few different types of data. Here are some of the basic ones:
 * String - `str` - `""` / `''` - Defined by single or double quotes.
 * Integer - `int` - `3` - Defined by just a whole number
 * Float - `float` - `3.14` - Defined by just the decimal
 * List - `list` - `[]` - Defined by square brackets - an order list than you can change after you set it
 * Tuple - `tuple` - `()` - Defined by brackets - an ordered list that you cannot change after you first set it
 * Dictionary - `dict` - `{}` Defined by curly brackets - a collection of key - value pairs

### Functions
"A function is a block of code which only runs when it is called. You can pass data, known as parameters, into a function. A function can return data as a result." - W3Schools
I had written an explanation, but it was much worse than the quote above.

```python
def sum(a, b): # A function can have inputs
  return a + b # The return statement gives back a value when you run it

print('What is the sum of 3 and 4? I will tell you below...')
value = sum(3, 4) # Here we are setting a variable to the returned value of a function.
                  # In this case it returns an integer
print(str(value)) # Because the function returns an integer, we should convert it to a
                  # string first. In this specific case, it is not necessary but beware
                  # of errrors when not converting to a string.
```
Note that this is an oversimplified example, but it shows you the basics of a function.

A function always needs to be called with `()`.
For example, if you run this:
```python
from microbit import *

while True:
  if button_a.was_pressed():
    display.show(Image.HEART)
  else:
    display.clear()
```
It will work perfectly, but if you run the below:

```python
from microbit import *

while True:
  if buton_a.was_pressed:
    display.show(Image.HEART)
  else:
    display.clear()
```
It will always show a heart, even if you aren't pressing the button. This is because Python, when given a function to RUN, will check if the RETURNED VALUE is `True`, but if you don't run the function (by forgetting the `()`), then it will return `True`, because THERE IS A FUNCTION WITH THAT NAME, even if the value of the button was `False`.

### While True Loops
To make a program loop forever, use a `while: True` loop.
```python
from microbit import *

while True:
  sleep(2000)
  print('Hello World')
```

### For Loops
For loops are used when you don't want something to repeat forever, but only for a set number of iterations.
```python
from microbit import *

for i in range(5): # Repeat five times
  print('Hello World')
 
images = [Image.CLOCK12, Image.CLOCK3, Image.CLOCK6, Image.CLOCK9]

for image in images:
  display.show(image)
  sleep(1000)
```

### If / Elif / Else
If elif else is used to determine if a statement is `True`.
If a statement is not `True`, then something else will happen. See below:

```python
from microbit import *

while True:
  if button_a.was_pressed():
    print('Button A was pressed')
  elif button_b.was_pressed():
    print('Button B was pressed.')
  else:
    print('No button is being pressed.') # You will almost certainly want to remove this, because it will spam the terminal.
```

### Sleep
This makes the program wait for a specified amount of time.
```python
sleep(2000) # In milliseconds
```

## Buttons
### is_pressed()
The buttons on the microbit can be used in if statements, to return `True` or `False` values.
There are two functions that return a button's value on the microbit. The first is `is_pressed`. This will keep on returning `True` until you let go of the button.
```python
from microbit import *

while True:
  if button_a.is_pressed():
    print('Button A is being pressed.')
  elif button_b.is_pressed():
    print('Button B is being pressed.')
```
This code will keep on spamming hte terminal for as long as you press either of the buttons.

### was_pressed()
`was_pressed` is different, it will only return `True` the FIRST time it detects the button was presed, after that, it will return `False`, even if it is still being held.

```python
from microbit import *

while True:
  if button_a.was_pressed():
    print('Button A was pressed.')
  elif button_b.was_pressed():
    print('Button B was pressed.')
```
This code will not spam the terminal, only printing once the first time you press the button.

## External IO
IO stands for in/out, of which, the microbit has many. But the easiest ones to access are pins 0, 1, and 2, which you can attach crocodile wires to, and connect to buttons, for example.
### Reading IO
Pin 1 and pin 2 are exposed in microbit as `pin1` and `pin2` respectively. You can use the `read_digital()` function that they both have, which is their equivalent of `button_a.is_pressed()`.
```python
from microbit import *

while True:
  if pin1.read_digital():
    display.show(Image.DUCK)
  elif pin2.read_digital():
    display.show(Image.GIRAFFE)
```

## Display
### Images
```python
from microbit import *
display.show(Image.HEART)
```
### Scroll
```python
from microbit import *
display.scroll('Hello')
```

### Set Certain Pixels
The microbit display has 5x5 grid of pixels that you have illuminated before, but now you have to set each pixel yourself.
The X axis, of dots is the rows (left to right), and the Y axis is the columns (top to bottom).
The X axis starts at zero on the far left of the display, and the Y axis starts at 0 on the top of the display.
You can also set the brightness individually for each pixel, from 0-9, 0 being off, and 9 being on at full brightness.

```python
from microbit import *

display.set_pixel(0, 0, 9) # The first number is the X axis, the second is the Y axis, and the last number is the brightness (0-9).
```

### Setting the Entire Display by Pixels
Although you can use the `set_pixel` function, it'd be pretty slow to write every line of code like that, so you can use strings inside the `Image()` function instead! 

```python
from microbit import *

SMILE = Image('00000:'
              '09090:'
              '00000:'
              '90009:'
              '09990:')

display.show(SMILE)
```
Each line here (seperated by a colon) is a line of the display. Because there are 5 pixels X and Y, there are 5 rows and columns of 0-9s. As you can imagine, 0-9 is hte brightness of each pixel.

You can make it more compact by not having each line with it's own row, but it may get confusing.

```python
from microbit import *

SMILE = Image('00000:09090:00000:90009:09990:')
display.show(SMILE)
```

### Inverting an `Image`
To invert an image, you call the `invert()` function on an `Image`. Here's an example:

```python
from microbit import *

display.show(Image.HEART)
sleep(1000)
display.show(Image.HEART.invert())
```

### Shifting an `Image`
Say you have a really big image you want to display, well, there's a way you can do that.

In the example below, it makes it look as if you are going down a rabbit hole on the microbit display.

```python
from microbit import *

HOLE = Image('90009:'
             '90009:'
             '90009:'
             '90009:'
             '90099:'
             '90099:'
             '90009:'
             '90009:'
             '99009:'
             '99009:'
             '99009:'
             '90009:'
             '90099:'
             '90099:'
             '90099:'
             '90099:'
             '90009:'
             '99009:'
             '99009:'
             '99099:'
             '99999')
HEIGHT = 17
display.show(HOLE)
for line in range(1, HEIGHT + 1):
  sleep(200)
  display.show(HOLE.shift_up(line))
display.show(HOLE.shift_up(HEIGHT))

display.show(Image.RABBIT)
```

### Don't Wait for Animations
We can also animate a list of different images, for example, `Image.ALL_CLOCKS`, has all of the clock images in it, and we can step through them like so:
```python
from microbit import *

display.show(Image.ALL_CLOCKS, loop=True)
```
We can loop scrolling text as well:
```python
from microbit import *

display.scroll('You can\'t stop me!', loop=True)
```

But this takes time to do, so we can't do other things while scrolling this text, or animating.
To fix this we can add the `wait=False` keyword, so that we can do other things while this is animating.

```python
from microbit import *

# Uncomment one of the following lines to test each one!

display.show(Image.ALL_CLOCKS, wait=False, loop=True)
#display.scroll('Hello!', wait=False, loop=True)
```

### Delaying and Clearing Animations
You can change the delay between chaning images in an animation using the `delay` keyword. You can choose to clear the display after the last image, or keep the last image onscreen using the `clear` keyword.

```python
from microbit import *

display.show(Image.ALL_CLOCKS, delay=50, clear=True)
```

### Clear
```python
from microbit import *

display.show(Image.HEART) # Show an image first
sleep(2000)
display.clear() # Clear the display
```

## Music
### Playing a Song
```python
from microbit import *
import music # Music isn't a part of the microbit library, so you have to import it seperately

music.play(music.ODE) # This plays the song 'ODE', there are many other songs you can play too.
```

### Playing a Note
```python
from microbit import *
import music

music.play('C') # This plays middle C for 4 beats.
music.play('C4:2') # This plays middle C for 2 beats.
                   # [NOTE][octave]:[duration]
```

### Don't Wait for the Music
Sometimes musicians are incredibly boring, and have long songs, but it's okay, WE CAN MULTITASK!!

```python
from microbit import *
import music

music.play(music.ODE, wait=False)

while True:
  if button_a.was_pressed():
    print('Musicians are SLOW!!!')
```

### Playing Music FOREVER
If you want a soundtrack for your life to play forever around you, then just add the keyword `loop=True`, and the music will play for the foreseeable future.
```python
from microbit import *
import music

music.play(music.ODE, loop=True)
```

You can use both `wait=False` and `loop=True` at the same time, to play music forever, and multitask.
```python
from microbit import *
import music

music.play(music.ODE, wait=False, loop=True)

while True:
  if button_a.was_pressed():
    print('Musicians are SLOW!!!')
```

### Stopping Music
If for some reason, the soundtrack to your life got boring after a couple of hours, then you can use `music.stop()` to stop the music.

```python
from microbit import *
import music

music.play(music.ODE, wait=False, loop=True)

while True:
  if button_a.was_pressed():
    music.stop()
```

## Temperature
You can check the current temperature by calling the `temperature()` function.
```python
from microbit import *

print(temperature())
```
## Compass
To use the compass no the microbit you can use the `compass.heading()` function to get the current direction the microbit is pointing. from 0°-359°.

```python
from microbit import *

while True:
  display.scroll(str(compass.heading()))
```

## Accelerometer
The accelerometer on the microbit provides lots of interesting functionality that Grok does not document, so there's more documentation on it [here](https://microbit-micropython.readthedocs.io/en/v1.1.1/accelerometer.html).

Here's an example of how to use the accelerometer.
```python
from microbit import *

while True:
  if accelerometer.was_gesture("shake"):
    display.show(Image.HEART)
    sleep(1000)
    display.clear()
```

## Radio
### Turning the Radio On
To use the radio function you first have to turn on the radio. This is because using it requires more power and memory than normal useage. The microbit has a range of around 10m.
```python
import radio

radio.on()
```

### Sending Messages
You can send messages using your microbit ot other microbits around it.
```python
import radio

radio.on()
radio.send("Hello World!")
```

### Receiving Messages
To receive messages from other microbits you can use hte `radio.receive()` function, as shown below.
```python
from microbit import *
import radio

radio.on()

while True:
  message = radio.receive()
  if message: # If no message has been sent, it returns None, therefore, we only print if
              # there is a message received 
    print(message)
```

### Radio Channels
You can choose which channel to send messages on (from 0-100) and only other people on that channel will be able to hear your messages. To change channel, set it when you call `radio.config())`.
```python
import radio

radio.on()
radio.config(channel=20)
```

### Clearing the Queue
To clear the queue, you can use `radio.on()` even if the radio is already on.
```python
import radio

radio.on()

# Some other code here that spams messages

radio.on() # Clears the queue
```
