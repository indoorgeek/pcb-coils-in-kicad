# PCB Coils in KiCad
<img src="https://github.com/indoorgeek/pcb-coils-in-kicad/assets/63697764/4243e7ba-d84a-451a-b756-9bff48d093fc" width=100% height=100%> <br/>
previously, I had made a [Mechanical 7 Segment Display](https://www.youtube.com/watch?v=3phLYcJFsy8) that uses electromagnets to push the segments. The project was so well-received, it even got published in Hackspace Magazine! I received so many comments and suggestions that I had to make an improved version of it. So, thank you, everyone!

Originally I had planned to make at least 3 or 4 such digits to display some kind of useful information on it. The only thing that stopped me from doing it were the power-hungry electromagnets. Thanks to them, each digit draws about 9A! That’s a lot! Although providing that much current was not a problem but I knew it can be a lot better. But then I came across Carl’s [FlexAR](https://flexar.io/) project. It is basically an electromagnet on a flexible PCB. He has made some awesome projects using it. Do check out his work! Anyway, it got me thinking if I could use the same PCB coils to push/pull the segments. This means that I could make the display smaller and less power-hungry.

# The Plan
I decided to try the following combinations:
- 35 turns - 2 layers
- 35 turns - 4 layers
- 40 turns - 4 layers
- 30 turns - 4 layers
- 30 turns - 4 layers (with a hole for the core)
- 25 turns - 4 layers

If you look at the PCB file, which KiCad generates, in a text editor, you can see that each and every segment’s position is stored in the form of x and y coordinates along with some other information. Any changes here will be reflected in the design as well. Now, what if we could enter all the positions needed to form a complete coil? Thanks to [Joan Spark](https://gist.github.com/JoanTheSpark), he has written a Python [script](https://gist.github.com/JoanTheSpark/e3fab5a8af44f7f8779c) which after entering a few parameters spits out all the coordinates needed to form a coil.

# PCB Design
<img src="https://github.com/indoorgeek/pcb-coils-in-kicad/assets/63697764/e83c5005-3f30-4ce0-817c-58a61983d79b)" width=100% height=100%> <br/>
I got my PCBs manufactured from [JLCPCB!](https://jlcpcb.com/DAA). Get your PCBs beautifully fabricated from JLCPCB for just 2$!

First place a connector on the schematic and wired it as shown above. This wire will become a coil in the PCB layout. Next, you need to remember the net number. The first one will be net 0, the next will be net 1, and so on. Next, open the python script using any suitable IDE.

Choose the trace width you will be using. After that, try experimenting with **sides**, **start radius** and **track distance**. Track distance should be double the track width. The greater the number of 'sides', the smoother will be the coil. Sides = 40 works best for most of the coils. These parameters will remain the same for all coils.

You need to set a few parameters like **center**, **number of turns**, **copper layer**, **net number** and most importantly, the direction of rotation (**spin**). While going from one layer to another, the direction must change in order to keep the direction of the current same. Here, spin = -1 represents clockwise while spin = 1 represents counterclockwise. For example, if the front copper layer is going clockwise then the bottom copper layer must go counterclockwise.

Run the script and you will be presented with a lot of numbers in the output window. Copy and paste everything into the PCB file and save it.

Open the PCB file in KiCad and there’s your beautiful coil.

Finally, make the remaining connections to the connector and you’re done!
