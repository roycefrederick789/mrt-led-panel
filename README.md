# MRT LED Panel
This project used a shift register to control the simplified MRT LED panel, inspired by the MRT LED panel inside the Singapore MRT. As part of applying what I learned in Digital Electronics, this project controls the LEDs using a shift register chip SN74HC595N, a chip I have in my component kits. As shift register is used, there are no computer programs needed to control the light which makes it purely hardware project. The main component needed is the shift register SN74HC595N.

## Demo Video


https://github.com/user-attachments/assets/d509c4c7-96b2-4ac7-a817-4ed0a8f62484


The ON LEDs represent the MRT stops that the train has yet to pass. The OFF LEDs mean the MRT has reached/passed the stations.

## How does it work?
An 8-bit shift register is used in the circuit. Each set of LED and current-limiting resistor is connected between the 5V supply and the chip output pin. When the output pin is LOW, the respective LED is on because there is a 5 V voltage drop across the circuit. When the output pin is HIGH, the voltage across two terminals is 0, and no current is flowing through the LED. As a result, initially, all LEDs are on. 

To turn off the LEDs one by one, a shift register is used to set the output pins to a HIGH state sequentially. The SER pin is always set to a HIGH state in this project. Upon clicking the ON1 button, SRCLK stores the HIGH data from the SER pin onto the register. Then, clicking the ON2 button transfers the data from the register to the output pin. This action sets the first output pin to the HIGH state. Repeating the step—clicking the ON1 button followed by the ON2 button—would push the data from the first output pin to the second output pin and transfer the data from the SER pin to the first output pin. For more details, please refer to the next section.

By clicking the reset button followed by the ON2 button, it would set all the output pins back to the LOW state and all LEDs are back on.

## How does SN74HC595N shift register work?
A shift register is a digital circuit that stores and moves binary data (HIGH or LOW) from input to the output pins one at one time. That is to say that in the first cycle, the data from the input moves to the first output pin. Then, in the next cycle, the data from the first output pin moves to the second output pin, whereas the first output pin receives the new data from the input pin. This will happen again for the next cycles.

In SN74HC595N, the following pins are set:
-	The SER pin is used to receive input data from the external. In my project, it is always set to a HIGH state (5V) because the aim is to set all the output pins to a HIGH state one by one.
-	The SRCLK pin is used to store the SER pin data in the shift register upon receiving rising edge signal. A button (ON1) is used to provide a rising edge signal.
-	The RCLK pin is used to move the data from the register to the output pins upon receiving a rising edge signal. Another button (ON2) is used to provide a rising edge signal.
-	The SRCLR (active-low) is a reset pin and by default is set to a HIGH state. Setting the reset pin to a LOW state sets all the data in the register to LOW states. Then, upon clicking the ON2 button, all data from the register (LOW states) is moved to the output pins, and all output pins become LOW.
-	The remaining pins: VCC is connected to the 5 V source, GND is connected to ground, and OE (active-low) is set to a LOW state to activate the output pins. 
