# Lab 5 - Controlling Arduino from the Raspberry pi using Python PyFirmata


## Pre requirements

### Setting up your Arduino for Firmata

* On **File** menu:
  - Select **Examples** -> **Firmata** -> **StandardFirmata**
  - **Verify** and **Upload** Standard Firmata code to the Arduino board

### Installing pyfirmata

* Connect via ssh to rapsberry pi
* Set up your Raspberry Pi with the python firmata libraries.
  Run the following commands:
```
> pi@raspberrypi~$ sudo apt-get install python-serial
> pi@raspberrypi~$ sudo pip install pyfirmata
```

### Find arduino port

* Find out the port name for the USB interface used:
  - Run this command in terminal without Arduino plugged in:
```
> ls /dev/tty*
```

  - Plug in the Arduino to the Raspberry Pi with USB cable
  - Run the command again. If a new name appears, then this is the name of your port.
  Register it to be further used.

## Goal 1 - Connecting to an Arduino

* Create a file 'ex1.py' in ‘/home/pi/lab5’ directory (or open an ipython console)
* Import the Arduino and util classes from the pyfirmata module and create an object using the USB address you found in the previous step:
```
>>> from pyfirmata import Arduino, util
>>> board = Arduino('/dev/ttyUSB0') # example
```


## Goal 2 -  Blink a LED

* Use digital pin 13, which is connected to an internal LED.
* LED on pin 13 should blink for 10 times (time ON = 1s and time OFF = 1s)
* Close pyFirmata after it is done

Learn the following functions:
```
    >>> board.digital[pin_nr].write(pin_value) # set the pin values high or low (1 and 0, respectively)
    >>> board.pass_time(t) # Non-blocking time-out for t seconds
    >>> board.exit()
```

### Goal 3 - Controlling analog ports

* To use analog ports, it is handy to start an iterator thread:
```
    >>> it = util.Iterator(board)
    >>> it.start()
    >>> board.analog[0].enable_reporting()
```

* Reads an analog input on pin A0, and prints the result, repeatedly for 2 minutes (sampling_rate = 10 Hz).

Learn the following functions:
```
    >>> time.time()
    >>> board.analog[0].read()
```

* Save the data received from pin A0 in a file 'data_analog.txt'.
* The file should have 2 columns:
 - Column 1 - current time (s)
 - Column 2 - pin A0 data (V)

Learn the following functions:
```
    >>> file = open('data_analog.txt', 'w')
    >>> file.write()
    >>> file.close()
 ```

* Question: What is the maximum sampling rate you can use to acquire the signal?

## Goal 4 - Dimming a LED

* Adapt the code from link 4 about dimming a LED
* Define a digital pin as PWM
* The time to reach the max/min of brightness should be 5 s
* Number of steps to get to the max/min -> use STEPS = 10
* The LED should be brightening and dimming repeatedly for 2 minutes

Learn the following functions:
```
    >>> digital_a0 = board.get_pin()
    >>> digital_a0.write()
```


## Links
* http://raspberrypi-aa.github.io/session3/firmata.html
* https://github.com/tino/pyFirmata/
* https://media.readthedocs.org/pdf/pyfirmata/latest/pyfirmata.pdf
* Dimming a LED: http://fabian-affolter.ch/blog/dimming-a-led-with-pyfirmata/
