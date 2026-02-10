# The [DST-2](https://github.com/TudorSupica/DST-2/)
![isometric](https://github.com/TudorSupica/DST-2/blob/main/PCB/3D/3D_iso.JPG)

   The DST-2 is the second version of the DST distortion pedal series. Its main goal was to make the pedal much more modular and easier to debug, since I want all the future pedals to be compatible with one another. 
  
  The modularity comes from the use of JST connectors and modules like the [TMC-1](https://github.com/TudorSupica/TMC-1) and the [TMF](https://github.com/TudorSupica/TMF). These modules aim to standardise the pedal-making process and make all the future pedals compatible.

  The debugging aspect of the board comes from the use of test pads labeled accordingly, so that when a problem arises, it can be easily debugged and fixed. The test pads I added mainly target features like power supply and signal line. I also connected the four screw holes in the corners of the board to GND, so that when debugging I won’t have to look for a ground test point.

  Another feature that I introduced with this board is the use of SMD components rather than THT ones (except for a couple diodes and the transistors). This change aimed to minimize the board size, to ensure it is going to fit alongside the other modules in the metal enclosure.

  # [The Schematic](https://github.com/TudorSupica/DST-2/blob/main/Schematic/)
   The schematic is made up of a few blocks: a buffer stage, an initial amplifying stage, a variable gain stage, a clipping stage, a filtering stage, and a final buffer stage. 

![Schematic](https://github.com/TudorSupica/DST-2/blob/main/Schematic/DST-2_schematic.JPG)

   ### The buffer stage 
   The buffer stage is a voltage follower made up of the transistor *Q1* and *R1*, *R2* and *C1*, *C2*.
   
   This stage has a voltage gain of (*ideally*) 1, so that the voltage at the collector of *Q1* is exactly the signal but 180º out of phase (*basically the signal but inverted, lmao maths*). But the real advantage of the buffer stage comes from the high-impedance input and low-impedance output of the stage. 
  
   The resistor *R1* biases the transistor whilst the resistor *R2* provides thermal stability (*you **could** add another capacitor in parallel with R2, so that it shorts at higher frequencies providing better stability thus a better frequency response*). The capacitors *C1* and *C2* are decoupling capacitors. They eliminate the DC characteristic of the signal so that I can bias it however I need to (*again, lmao maths*).

   ### The initial amplifying stage
   The initial amplifying stage is made up of the transistor *Q2*, the resistors *R3* thru *R6* and the capacitors *C3* thru *C5*.

   The resistor *R3* and capacitor *C3* make up a high-pass filter with a cutoff frequency of about 33 Hz. The capacitor *C3* is also used to decouple the signal, and the resistor *R4* is used to bias the base signal of the transistor *Q2*.

   The resistor *R5* and the capacitor *C4* make up the feedback loop of the stage, whilst the resistor *R6* gives the amplifying ratio of the stage (*its ratio is roughly R6/internal resistance of the BE junction*).

   Finally, the capacitor *C5* is used to decouple the signal before it reaches the next stage.

   ### The variable gain stage
   The variable gain stage is made up of a few components, mainly a double op-amp SOIC-8 IC (*even tho the TL072 or the LM358 work fine, I'd strongly recommend some better op-amps such as the OPA2134*) with some support components such as resistors and capacitors.
  
   # [The PCB](https://github.com/TudorSupica/DST-2/blob/main/PCB/)
  Yappa yappa PCB yappa yappa type shi


   # After initial testing

After initial testing, the pedal seems to work but just barely. There is a whole lot of induced noise. The values for the filter are all over the place and make the pedal sound too muffled. Overall just a bad tone. I've since learned that JST connectors are really really unreliable and that the use of separate "modules" for the footswitch and the jack connectors is a bad idea. It adds complexity and are really really prone to failure / noise. I plan on redesigning it without all that fuss, one board to rule them all. The footswitch placement is still an issue tho. I can’t mount it directly on the PCB since I can’t reliably predict the final height of the whole assembly (it can be soldered higher or lower). Therefore, it needs to remain separate, with wires manually routed to it. The same applies to the jack connectors. The barrel connector on the other hand, i can have it on the PCB no problem since it needs some stability to work properly. The potentiometers need to be routed manually also.

   ## Conclusions:
-new pcb
-manually route wires to pots/conns/switch
-change filter values
-pick another IC for the board (OPA2134)
