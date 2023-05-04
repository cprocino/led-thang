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

# Temp sensor
for this project we just needed to tempiture sensor work 
this project was very simple as it was the first project of this unt so all we needed was thethe basic nessecities of the project. Bread board, arduino the sensor and a LCD screen 

here is the code i used:

        import board   #[Lines 1-8] Importing all Neccessary libraries to communicate with LCD
        import time
        from lcd.lcd import LCD
        from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
        from digitalio import DigitalInOut, Direction, Pull
        import board
        import analogio


        # get and i2c object
        i2c = board.I2C()
        tmp36 = analogio.AnalogIn(board.A0)
        # some LCDs are 0x3f... some are 0x27.
        lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)
        def tmp36_temperature_C(analogin):              #Convert millivolts to temperature
            millivolts = analogin.value * (analogin.reference_voltage * 1000 / 65535)
            return (millivolts - 500) / 10


        while True:
         # Read the temperature in Celsius.
          temp_C = tmp36_temperature_C(tmp36)  
          # Convert to Fahrenheit.
          temp_F = (temp_C * 9/5) + 32
           # Print out the value and delay a second before looping again.
               lcd.set_cursor_pos(0, 0)           #[Lines 26-36] Print different messages based on the temperature
         if temp_F > 75:
             lcd.print("it's too hot!")
         elif temp_F < 70:
             lcd.print("it's too cold")
         else:
                lcd.print("It's just right")
         lcd.set_cursor_pos(1, 0)
         lcd.print("Temp: {}F".format(temp_F))
          time.sleep(.5) 

here is the wiring diagram:

![Screenshot 2023-03-20 151632](https://user-images.githubusercontent.com/71406784/226443222-5c6ae118-0ef2-4f15-843e-01d13204ca6a.png)



This was a pretty easy project it just needed some help from nixon and ChatGPT to finnish.


