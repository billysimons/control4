# control4 UART Recovery
How to connect to Control4 EA series controllers (and maybe others) using the onboard UART to diagnose issues.

## What you need
* Raspberry PI
* F/F Jumper Wires
* PZ0 Screwdriver

I used a Rapberry PI to access the onboard UART.  The advantage of the RPI is the logic levels are already 3.3v so theres no additional hardware required.

# Method
## Opening the EA Controller
Turn the EA upside down and remove the two screws at the front of the controller as shown (you dont need to remove the others).
![EA3-screw-removal](/files/ea-3-screw-removal.png)

Once the two screws are removed, you should be able to slide the cover off like this:
![EA3-part-open](/files/ea-3-part-open.png)

Then, slide the lid off to expose the board. You can see the UART next to the PSU (it might different on different controllers).  It is labelled DEBUG UART and is the only soldered 4 pin header on the board.
![EA3-fully-open](/files/ea-3-fully-open.png)

## Locate the UART
Inside the EA you will see the UART header as shown.  The pins are ordered right to left and are as follows:
1. - TX
2. - GND
3. - RX
4. - +3.3VDC

![EA3-uart-pinout](/files/ea-3-uart-pinout.png)

## Connect to the Pi
Im using a Pi3, you need to connect the pins as follows:

| Pi  | EA-3 |
| ------------- | ------------- |
| TX  | RX  |
| RX  | TX  |
| GND  | GND  |

##Configure Pi
On your Pi, run `sudo raspi-config` and check if it has the option advanced options -> serial. If it has, set it to disabled and you're done.  This stops the Pi from using its onboard UART with the Kernel console so you can use it to connect to the EA-3.

SSH to your Pi and run `screen /dev/ttyS0 115200` and then boot the EA-3.

If you get junk text, check your baud rates (115200 above) and your ground pins.  On my Pi I had to reboot it a couple of times for it to work properly (not sure why).

Ive attached a sample of the boot log so you can get an idea of whats available.  You can get root access by interrupting the boot process - type `c4` within a few seconds of power on.  After this, you can then boot up with your own kernel string into single user mode.
