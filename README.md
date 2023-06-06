Soldering station
Author:Xander Aerts

Content
1	Introduction	1
2	Material and methods	2
3	Results	4
3.1	Schematics and PCB	4
3.1.1	Schematics	4
3.1.2	PCB	6
3.2	Case and final product	6
3.2.1	Case	6
3.2.2	Final product	7
4	Discussion	7
5	Reference list	8




1 Introduction
This project aims to design a functional and durable prototype soldering station that is based on the design that Elektor made a few years ago. Because the design has been in use for several years, it forms a stable base to start from. As a prototype it needs to easily troubleshoot and repair in order to make the testing process easier. This application note will not only discuss the final outcome and the approach that it took to get there but also the different materials that were used, as well as the different challenges and decisions encountered throughout the different phases of the project.

2 Material and methods
One of the primary tasks was designing the PCB. For this purpose, Altium Designer was used. This program offers a considerable amount of possibilities and documentation making it a very suitable choice for this project. 
Another significant task was to design the mechanical case to house the electronics in. The reason Fusion 360 was chosen for this is because it allows for exact measurements to be used in a 3D design. Other software like Blender can also be used to create a 3D design. Blender however doesn’t allow exact measurements to be used out of the box as easily as Fusion does. This makes Fusion a better choice to create a case that needs to be precisely designed to house the electronics. In order to 3D print a slicing program is needed to break the 3D model into different layers. Ultimaker Cura was used here instead of Prusa because of more experience with the Cura software.
Most of the components that were used for this project are the same as the ones that Elektor recommends. There are however some components that are slightly different.  In this design for example the BC 547 CG was used instead of the BC 547 C transistor. The most important characteristics are identical of course, only some minor differences are present. The descriptions and datasheets were used to compare the different characteristics of these components.
As for the testing equipment both a multimeter and a transformer were used to safely test the PCB during and after the PCB assembly.

Both the schematic library and the PCB footprint library needed to be made as shown in the first step. Followed by designing the schematics using the previously made schematic library.
Importing the schematics into the PCB layout and placing the different components in such a way that everything would function as intended is what the second step consisted of.
After that all the traces were routed and checked so that they would match the needed requirements. This was done to ensure that the electrical connectivity as well as the signal transmissions would work properly between the different components.
In the fourth stage , the PCB was assembled in different steps to ensure a proper functionality. The first step consisted of assembling the power supply, followed by the CPU, Thermocouple, and the PWM control without the ATMEGA and           	opamp IC’s.  

The PCB was tested every time a new section had been added to the PCB as shown in the fifth step. If it didn’t work it would be troubleshooted, repaired and tested again until it functioned as intended. The testing in step five would happen as followed: 
* Firstly there would be checked for a shortage with a multimeter if needed. 
* After this, the power supply would be plugged into the electrical outlet followed by measuring the 5 Volt output of the power supply depending on the section that was added before.
The sixth step consists of creating a design illustration for the case. Besides brainstorming about the final aesthetic design there were also the practical decisions to be made such as providing mounting holes for the transformer and the PCB for example. Followed by the finalization of the overall design and the assembly process, the individual parts were developed starting with the bottom plate followed by the middle and top part. Each part was, after being completed, printed and tested. Parts that had fatal flaws or to many mistakes, were redesigned and reprinted.
Once every component functioned properly, they were assembled together. This didn’t included just the PCB and case but also the inlet filter and cable for the soldering iron. The entire system was, after the final assembly, tested once again in the final step to ensure that everything still worked properly.




















3 Results
3.1 Schematics and PCB
3.1.1 Schematics
The following schematic (Figure 2.0) shows the diagram of the power supply. Its operation is quite straightforward. The relay RY1 selects the desired voltage controlled by the microcontroller that will be connected through transistor T5. One of the bridge rectifiers will, depending on the desired voltage, rectify the AC electricity. Followed by a circuit that outputs a stabilized voltage. Its value depends on the requested voltage. These voltages are later used to power other parts of the circuit.

The microcontroller cannot power the soldering iron directly. Because of this, the first three transistors T1, T2, and T3 make sure that the signal remains accurate after it passes the MOSFET by removing unwanted noise that could potentially create an unwanted digital signal. This was done so that the MOSFET would switch at the needed requirements followed by a choke that further removes any unwanted noise. All of this is shown in Figure 2.1.


In Figure 2.2, the two opamps in the thermocouple section receive a voltage from the internal temperature sensor of the soldering iron. They compare the voltage to another reference voltage value and send the result to the microcontroller, which evaluates it and changes the output signal to the soldering iron accordingly. The capacitors that are separated from the main circuit are intended to remove any unwanted noise in the voltage used to power the opamps.

Figure 2.3 shows the final stage of the design: the display. This schematic is split into 2 parts to create a more flexible design that is easy to mount in a mechanical case. The left part that contains the encoder sends the users input to the CPU through the connectors TB12 and TB14 to the main PCB. The display driver, in combination with the display itself, is located on the right side of the schematic and is connected to the CPU though the connectors TB11 and TB15. The display is used to show different error codes, menu’s, and temperatures.

The main section that controls all of these different individual circuits is the CPU, as shown in Figure 2.4. A great deal of the connectors around the CPU can be used to expand the design further by providing access to the unused GPIO pins of the microcontroller. The capacitors and the choke at the top of the schematic  are for decoupling and noise reduction. These make sure that there is a constant DC voltage without any unwanted noise supplied to the CPU.

    
3.1.2 PCB
The PCB design is organized into six different sections as shown in figure 3.1. Starting from the top left corner there is the encoder section, followed by the display section underneath it. Further down the PCB, toward the left side, is the power supply section. The traces are wider here to allow for more current. Right beside the power supply, located on the right side of the PCB, there is the CPU with multiple different connectors. Below the power supply, the thermocouple and the PWM-control sections are located. The PCB design is structured in such a way that the encoder and display sections can be separated from the main PCB. This allows for more flexibility during the case design phase.
3.2 Case and final product
3.2.1 Case
The case consists of 3 parts to reduce printing time. 
* Firstly the bottom plate where the transformer and PCB will be mounted on. 
* Secondly the wall that contains holes for the inlet filter, the cable and the encoder. 
* And thirdly the top part containing the display. 
    All these components have bevelled edges to create a somewhat aesthetic design.
    In addition to the primary case design, the soldering iron holder by Wilfred Swinkels[1] was used.
3.2.2 Final product
The final product consists of two units, the primary unit housing the electronics as can be seen in Figure 3.2. And a secondary unit referred to as the soldering iron holder. The device can be powered on and off using the switch from the inlet filter on the back. The soldering iron will automatically reach the temperature that was previously set. By rotating the knob on the front users can change the temperature to the wanted value.
4 Discussion
One of the problems that were encountered during the first step was caused by working on the libraries and the schematics at the same time. This raised the problem that the schematics wouldn’t update automatically when footprints were added to the PCB library. The problem was eventually solved by updating the schematics manually. When I reflect back on this problem I realize that I should have finished the libraries first followed by the schematics.
The footprints themselves were also a notable challenge because of a very limited amount of experience with this and a great number of non-professional footprints that would possibly raise problems in the PCB design phase. A considerable amount of footprints were modified by hand because of this. There were also a handful of components created from the ground up because some of them didn’t exist or because they were made for specific components that were already available and didn’t need to be bought.
Besides fixing some errors that the program gave there were also different decisions to be made. The most important one was the display. Different design possibilities were available here. One of the first designs was to work with a finished module that already had the display and the display driver attached to it. The problem with this was the lack of documentation about the internal wiring of the finished module. This gave too much risk so the design was made modular afterwards. A modular design would also allow for more flexibility in the end because both the Elector design and finished modules with the right internal wiring could be used.
One issue with one of the components, the encoder that Elektor said they used didn’t match the required specifications they gave. The reason for this is that the product number they wrote down was for an encoder that didn’t have a pushbutton while the design specifically needs one with a pushbutton.
The case design also presented some significant challenges, partially due to a limited time. Designing a compact case proved to be one of the first main challenges due the relatively large components. The second main issue that arose during development was the printing time. To solve this problem the upper part of the housing was divided into two smaller parts. After printing the middle part however some other problems were encountered about the design. The first one was that the two middle mounting blocks prevented the final product to ever be taken apart without damaging the case. The second  challenge was caused by the thickness of the walls arising the problem that the encoder wouldn’t fit. This would have been easily fixed by redesigning the middle part but while printing it again, the 3D printer’s nozzle clogged which caused the 3D print to fail. Due to time running out,  the middle part with the previous mentioned problems was reused by solving the different problems. This was possible by cutting the middle mounting blocks away and reducing the thickness around the mounting hole of the encoder.

5 Reference list
    [1] RT series, WMRP series, soldering iron stand. by theswink - Thingiverse


ELECTRONICS-ICT	Project Design 2020-2021

		2 / 3

ELEKTRONICA-ICT
Project Ontwerpen

		2 / 3

