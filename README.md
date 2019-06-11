
# AladdinLCD 

This VHDL was written as a fun educational exercise to replace the CPLD logic on the cheap AladdinXT 4032 Original Xbox modchip. It converts the modchip to a basic LCD driver, consequently it looses the ability to load a custom bios.
This is best used with a TSOP flashed or soft modded console.

The Lattice LC4032V CPLD on the cheap Alladin modchips is extremely limited, so this is a hacky bare minimum to reduce macro-cell usage to fit onto the CPLD. Therefore it will not support any other functionality, unless you decide to migrate it to a higher macro cell count CPLD (i.e 4064 variant) and add other features.

- This does not support adjusting the backlight via the dashboard settings.
- This has very limited contrast control through the dashboard settings. It couldn't even manage an 8-bit PWM signal.
For the dashboard settings: **0%=No Contrast, 25%=Full Constrast**. Anything else wont work as expected.
If this isn't good enough for your particular LCD, use an external trimmer.
![lcd installed](https://i.imgur.com/CkHGifg.jpg)

## Instructions
1. Remove the flash memory and socket from the Aladdin Chip to expose the required usable IO pads. Be careful not too damage the pads.
2. Connect JTAG programmer to the JTAG pins shown below. Apply 3.3V power to the Aladdin PCB. 
3. Program CPLD with the `SVF` file in this repository . I programmed it with [UrJTAG](http://urjtag.org/) using a [compatible programming cable](http://urjtag.org/book/_system_requirements.html#_supported_jtag_adapters_cables). The general programming sequence in UrJTAG is something like: (Commands written in **bold**).

    **cable usbblaster**  *Type `help cable` for other cables.*  
    **detect**  *To confirm that the cpld is detected.*  
    **svf ALADDINLCD.SVF progress** *To program the CPLD.*  
    ![programming output](https://i.imgur.com/hocVP1j.png)
4. Wire the LCD as per the diagram below.
5. Install onto LPC Header in your Xbox. There is no other connections to worry about. *If you have a 1.6 motherboard you will need to rebuild the LPC as you would for a modchip install.*
6. Enable `SmartXX` LCD in your dashboard.
7. Set contrast to a value between `0 and 25%` to display correctly. 25% is full contrast with this mod. Values above 25% won't work as expected. I find ~20% a good value.


### Wiring
![wiring diagram](https://i.imgur.com/yHu28u4.jpg)

