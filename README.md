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
![EA3-screw-removal](/images/ea-3-screw-removal.png)

## Locate the UART
Inside the EA you will see the UART header as shown.  The pins are ordered right to left and are as follows:
1. - TX
2. - GND
3. - RX
4. - +3.3VDC

