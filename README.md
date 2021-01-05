# ATXPowerSupply (Completed 05/19/2017)

# Important Note
**This was the first PCB I designed. Please keep that in mind if you decide to reference this design.**

# Inspiration
Soon after graduating college while applying for jobs as an emedded systems engineer, I realised that knowing how to effectively design PCB's was a good skill to have. 
I also had some personal projects in mind that I wanted to work on to improve my skills with various MCU's. So I figured I would manufacture my own PCB designs. Most blogs recommend 
starting with EagleCAD as it has good community support and is especially popular with hobbyists. Unlike other free professional softwares, Eagle is only limited by the 
size of the board and not by the number of nets like Orcad PCB designer. 

At the time, I found an old ATX power supply lying in storage at the department of Electrical Engineering. It was leftover from some senior design project so with their permission, 
I took it. Thats when I got the idea to design a simple breakout for this board I could use with whatever projects I had lined up. 

# Table of Contents
1. Objective
2. Feature List
3. Design Breakdown
4. Issues
5. Final Comments

## Objective
The objective of the project was to learn EagleCAD as a complete new comer. It would also be an opportunity to learn about various design methodologies and considerations that
go into PCB design. Finally, I would have a good power supply breakout board.

## Feature List
- Connects to a standard 20 pin ATX power supply connector
- A standard toggle switch should be able to enable/disable the power supply
- Each power line should be broken out into a seperate 2.54mm header
- Should have an LED to indicate if power is on or not

## Design Implementation
The design is fairly simplistic. A 20 pin ATX female header is placed on one side of the board to connect to the power supply. A standard SPDT toggle switch is connected to Power Enable
pin of the ATX supply. This enables/disables the power supply. An LED is driven off the 5V power line with a current limiting resistor to indicate if power is on or not. Finally,
there are 4 power lines borken out standard 2.54mm 10 pin header:

    - 12V  32A 
    - 5V   16A
    - 3.3V 16A
    - -12V 0.3A
    
Finally, a 20 pin header is used to breakout the ground pins.

## Issues
Because all of my projects I used this supply for consumed very little power, I never experienced any issue. But looking back now in 2021, I can see quite a few areas of concern
and little use of some common PCB design practices.

1. None of the traces are thick enough to handle currents as high as 32A. In the end, the PCB should be designed for the worst case conditions. Using an [online trace width 
calculator](https://www.7pcb.com/trace-width-calculator.php) you can get a good idea of how thick your traces should be for max current. 
2. The 2.54 mm breakouts would probably melt in high current situations. 
3. I didn't use the bottom layer (Layer 16) as a mirror for the power lines. This is a common way of doubling the current carrying capacity of a single net.
4. Often to dissipate heat and improve current carrying capacity, the power lines can be turned into planes covering a larger area rather than a single trace. Connecting the planes on both layers together 
(Layer 1 and 16) using via's, assuming its a standard 2 layer board is recommended.
5. The GND plane is also only on layer 1 and not on layer 16 as well. Joining these 2 layers with via's would allow for much better current and heat dissipation. 
6. I ignored the DRC errors. DRC stands for **Design Rules Check**. You can assign rules that must be followed such as the distance if via's from the edge of the board
or the minimum trace widths. Unless your circuit has specific design requirements, I recommend sticking with the default rules or setting the design rules recommended by your manufacturer.
From personal experience I can assure you it will save you a lot of headache at some point.

## Final Comments 
There is a fundamental flaw in this project which is also the source of the issues stated above. I was using this power supply for breadboards and low power consumption applications.
There is no conceivable situation where I would require 32A of current, or even 16A or 8A. For up to 4A of current per power line, this design will do. As a result,
I didn't design it for high current applications. 

For the intent of use, this design works fine ... mostly. Common practices of using both layer 1 and 16 for traces and ground planes are good but not always necessary.
It's not great but for my very first PCB, I'm happy with it. It worked and served it's purpose. 


