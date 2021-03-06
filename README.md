# How to burn Arduino code to AVR Chips
**This works for only `Atmega8A, Atmega32A,  Atmega32, Atmega16A` for now.**

Long story short, do the following things and I think you'll be done. 

## Disclaimer
If you mess up the whole process and brick your chip I won't be responsible. No need to worry though, you can do it if you do as I say.

## The things you should gather before you proceed:
* An ATmega chip, `ATmega8/32/32A/8A` should work
* An `Arduino IDE` (I've tested this on the version `1.0.5-r2` and `1.6.7`)
* A `USBasp` (Works also with avr uploader as long as it uses USBasp driver it should work) with `A-B Usb Cable`
![usbasp](http://i.imgur.com/fgbhvYV.jpg)


## USBASP Pinout
![usbasp_pinout](http://i166.photobucket.com/albums/u117/rdshear/10-10-6.jpg)

* Some premium jumper wires
* A led to test (with small resistance, say 330 Ohm would be perfect)
* Download the boards.txt files and header pin definition files
* **Keep a backup of your boards.txt file!!!**

I think that's it, let's follow the procedure.

## How to
* If you have your Arduino IDE open, please close it first

* copy the `Downloaded boards.txt` file and then paste it in your `\arduino-1.0.5-r2\hardware\arduino` dir, for me it was `E:\arduino-1.0.5-r2\hardware\arduino`

![alt text](http://i.imgur.com/ID4Uhoy.png)

* Now copy the `mega` and `mega32` folder to the `\arduino-1.0.5-r2\hardware\arduino\variants` dir, for me it was `E:\arduino-1.0.5-r2\hardware\arduino\variants` [A mega file maybe already there, if it is then replace it anyway]

![alt text](http://i.imgur.com/qh6dMVu.png)

* Add and save this text to your `programmers.txt` (dir: `\arduino-1.0.5-r2\hardware\arduino`) file if doesn't exist
```
usbasp.name=USBasp
usbasp.communication=usb
usbasp.protocol=usbasp
```

![alt text](http://i.imgur.com/nRi7uIe.png)

* Now Open the `Arduino IDE` and select your MCU

![alt text](http://i.imgur.com/raAcH5Y.png)

* Now select the programmer (`USBasp`)
 
![alt text](http://i.imgur.com/zbN5uzH.png)

* Connect your USBasp to your pc and connect the following pins from USBasp to your chip
  * MISO
  * MOSI
  * SCK
  * RESET
  * VCC
  * GND


**Make sure you short the `AVCC and VCC` together and put `+5V` and short the other `GND and GND` together and connect `GROUND`**

#### **For ATmega8**
Follow this image to find out the necessary pins

![alt text](http://i.imgur.com/0FpGIig.png)

#### **For Atmega32**
Follow this image to find out the necessary pins

![alt text](http://i.imgur.com/DmpWenQ.png)

![arduino-atmega32](http://openhardware.ro/wp-content/uploads/ATmega_16_32_Arduino_Pinout.jpg)

Now you've connected all the things together click upload, if it uploads without fail then you're done!

* If you want to test a led, `follow the uploaded pinout diagram` to find out which is the `13` pin on your MCU or other pins (you get the idea, don't you?) then connect it and test it

## Clock speed correction

* open `boards.txt`
* Now find the desired mcu's 
* For example: Arduino NG or older we can find these codes
```
##############################################################

atmegang.name=Arduino NG or older

atmegang.upload.tool=avrdude
atmegang.upload.protocol=arduino
atmegang.upload.speed=19200

atmegang.bootloader.tool=avrdude
atmegang.bootloader.unlock_bits=0x3F
atmegang.bootloader.lock_bits=0x0F

atmegang.build.mcu=atmegang
atmegang.build.f_cpu=16000000L
atmegang.build.board=AVR_NG
```

* edit the following line and make the f_cpu value 1Mhz like this: `atmegang.build.f_cpu=1000000L` save the file
* Now you can see that the clock speed is fixed


## Important Links
[Achu's blog](https://achuwilson.wordpress.com/2011/12/15/arduino-ide-for-programming-atmega-microcontrollers/)


[Open-Hardware](http://openhardware.ro/using-atmega32-arduino-ide/)

## Note
* If the clock is not syncrhonized perfectly, try synchronizing using different clock speed e.g: 1MHz, 8MHz but not more than that
