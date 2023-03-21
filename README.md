# CPyProjectTemplate
for this project we just needed to make a led blink using python
this project was very simple as it wwas the first project of the year so all we needed was the arduino and the computer
here is the code i used:
import board
import neopixel
import time

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.5 


while True:
    b=25
    g=0
    r=25
    dot.fill((b,g, r))
    time.sleep(1)
    dot.fill((0,0,0))
    time.sleep(1)
    print("Make it green")

I didnt have any real problems this project, just had to set up all the accounts and downloads.
