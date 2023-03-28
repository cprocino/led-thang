# rotary encoder

For this assignment, we had to make a “traffic light”NeoPixel controlled by a rotary put it on a LCD. The rotary encoder picks the color.

Code

    import rotaryio
    import board
    import digitalio
    import neopixel
    from lcd.lcd import LCD
    from lcd.i2c_pcf8574_interface import I2CPCF8574Interface

    # get and i2c object
    i2c = board.I2C()

      # some LCDs are 0x3f... some are 0x27.
    lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)

    led: neopixel.Neopixel = neopixel.NeoPixel(board.NEOPIXEL, 1) # initialization of hardware
    print("neopixel")

    led.brightness = 0.1

    button = digitalio.DigitalInOut(board.D12)
    button.direction = digitalio.Direction.INPUT
    button.pull = digitalio.Pull.UP

    colors = [("stop", (255, 0, 0)), ("caution", (128, 128, 0)), ("go", (0, 255, 0))]

    encoder = rotaryio.IncrementalEncoder(board.D10, board.D9, 2)
    last_position = None
    while True:
        position = encoder.position
        if last_position is None or position != last_position:
            lcd.clear()
            lcd.print(colors[position % len(colors)][0])
        if(not button.value):
            led[0] = colors[position % len(colors)][1]
       last_position = position



wiring  


![images](https://user-images.githubusercontent.com/71406784/228336909-24ebc7de-6144-4aee-914e-3090d875208f.jpg)
i got this wiring diagram from osoyoo.com and made a few slight changes to make it work.

Reflection
this one was difficult for me as i had no idea what i was doing until it worked. I got most of the project from rivers github and want to give him a huge thanks. this took a while to figure out but git hub is a great resource.

