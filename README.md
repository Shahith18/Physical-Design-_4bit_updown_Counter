# Exp 5 Physical Design of a 4-Bit Up-Down Counter

## Aim:

Execute floorplanning, power planning, and placement for the synthesised 4-bit up-down counter design.

## Tool Required:

Physical Design: Innovus

## Mandatory Inputs for PD: 

1. Gate Level Netlist [Output of Synthesis]
   
2. Block Level SDC [Output of Synthesis]
   
3. Liberty Files (.lib)
   
4. LEF Files (Layer Exchange Format)
   
## Procedural Steps:

Ensure the Synthesis for the target design is complete, and then open a terminal from the corresponding workspace. 

• Initiate the Cadence tools and cmd:innovus (Press Enter) 

• For Innovus tool, a GUI opens, and the terminal also enters the Innovus command prompt, where the tool commands can be entered. 

After importing the Design, Perform the following Physical Design stages:

→ Floor Planning 

→ Power Planning

→ Placement
Note : Check the paths to properly read in the input files. 

•	Else, if you would like to import your design using GUI, open the Innovus tool and from the GUI, go to File → Import Design.

o	A new pop-up window appears. 

o	First, load the netlist. You can browse for the file and select “Top cell : Auto Assign”.

•	Similarly, select your LEF files from the specified path.

•	Once LEF Files are loaded, Next step is to create the power supply pins both VDD and VSS

•	In order to load the Liberty File and SDC, create delay corners and analysis view, select the “Create Analysis Configuration” option at the bottom.

o	An MMMC browser Pops Up.

<img width="819" height="670" alt="image" src="https://github.com/user-attachments/assets/12b66c0e-44d0-437e-878e-7620932e7edd" />

The order of adding the MMMC Objects is as follows. 

1. Library Sets
   
2. RC Corners
 
3. Delay Corners
   
4. Constraints (SDC)
   
Once all of them are added, Analysis Views are created and assigned to Setup and Hold. 

In order to add any of the objects, make a right click on the corresponding label → Select New. 

Adding Liberty Files (slow.lib, fast.lib) under “Library Sets

• add slow.lib with a label Slow or any identifier of your own.

### Fig.1 Add slow Library set

• add fast.lib with a label Fast or any identifier of your own.
<img width="1920" height="1080" alt="Screenshot (110)" src="https://github.com/user-attachments/assets/ea81af3c-6a1e-412b-8e52-adc56860e935" />


### Fig.2 Add fast Library set

• Adding RC Corners can also be done in a similar process. The temperature value can be found under the corresponding liberty file. Also, cap table and RC Tech files can be added from Foundry where available.
<img width="1920" height="1080" alt="Screenshot (110)" src="https://github.com/user-attachments/assets/bba843aa-64ef-43a7-8662-d81b0cc7eb00" />


### Fig.3 Add RC corner

• Delay Corners are formed by combining Library Sets with RC Corners.
<img width="1920" height="1080" alt="Screenshot (96)" src="https://github.com/user-attachments/assets/a9296c23-da55-4b37-a36f-c3759e74b7cf" />



### Fig.4 Add Delay corner Max_delay & Min_delay

• Similarly, SDC can be read under the MMMC Object of “Constraints”.
<img width="1920" height="1080" alt="Screenshot (112)" src="https://github.com/user-attachments/assets/830c1135-82ac-478a-9b5d-068446204819" />


### Fig.5 SDC Constraint file

• Analysis Views are formed from combinations of SDC and Delay Corner.
<img width="1920" height="1080" alt="Screenshot (113)" src="https://github.com/user-attachments/assets/a3497cd6-eac9-46fb-972e-733acfe5f2c0" />


### Fig.6 Add Analysis View Worstcase & Bestcase

• Once “Best” and “Worst” Analysis views are created, assign them to Setup and Hold.
<img width="1920" height="1080" alt="Screenshot (114)" src="https://github.com/user-attachments/assets/6db2b54c-8363-4962-8d13-dd09701d5d60" />


### Fig.7 Add Setup Analysis View & Hold Analysis View

• Once all the process is done, Click on “Save&Close” and save the script generated with any name of your choice. 

• Make sure the file extension remains .view or .tcl 

• After saving the script, go back to Import Design window and Click “OK” to load your design.

<img width="1920" height="1080" alt="Screenshot (97)" src="https://github.com/user-attachments/assets/cbc23214-2e30-4edd-bc42-0fbe7e0a5e00" />


In the Import Design window click the save option to save the Default.globals file

• A rectangular or square box appears in your GUI if and only if all the inputs are read properly.


### Fig.8 Core area

• The internal area of the box is called “Core Area”. 

• The horizontal lines running along the width of Core are “Standard Cell Rows”. Every alternate of them are marked indicating alternate VDD and VSS rows. 

• This setup is called “Flipped Standard Cell Rows”.
<img width="1920" height="1080" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/f808181b-bac1-4c1c-a219-a1ccb6ac77a8" />


### → Floorplan 

#### Steps under Floorplan : 

1. Aspect Ratio [Ratio of Vertical Height to Horizontal Width of Core]

2. Core Utilisation [The total Core Area % to be used for Floor Planning]
 
3. Channel Spacing between Core Boundary to IO Boundary
 
• Select Floorplan → Specify Floorplan to modify/add concerned values to the above Factors. On adding/modifying the concerned values, the core area is also modified.

### Fig.9 Specify Floorplan 

• The Yellow patch on the Left Bottom are the group of “Unassigned pins” which are to be  placed along the IO Boundary along with the Standard Cells [Gates].
<img width="1920" height="1080" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/afb8f3ee-1314-4ec5-ab8d-4716d696d3ae" />

#### → Power Planning

#### Steps under Power Planning : 

1. Connect Global Net Connects
   
2. Adding Power Rings
   
3. Adding Power Strings
   
4. Special Route

Under Connect Global Net Connects, we create two pins, one for VDD and one for VSS connecting them to corresponding Global Nets as mentioned in Globals file / Power and Ground Nets.

1. Select Power → Connect Global Nets.. to create “Pin” and “Connect to Global Net” as shown and use “Add to list”.
   
2. Click on “Apply” to direct the tool in enforcing the Pins and Net connects to Design and then Close the window.
   
• In order to tap in Power from a distant Power supply, Wider Nets and Parallel connections improve efficiency. Moreover, the cells that would be placed inside the core area are expected to have shorter Nets for lower resistance. 

• Hence Power Rings [Around Core Boundary] and Power Stripes [Across Core Boundary] are added which satisfies the above conditions.

• Select Power → Power Planning → Add Rings to add Power rings ‘around Core Boundary’.

• Select the Nets from Browse option OR Directly type in the Global Net Names separated by a space being Case and Spelling Sensitive. 

• Select the Highest Metals marked ‘H’ [Horizontal] for Top and Bottom and Metals marked ‘V’ [Vertical] for Right and Bottom. This is because Highest metals have Highest Widths and thus Lowest Resistance. 

• Click on Update after the selection and “Set Offset : Centre in Channel” in order to get the Minimum Width and Minimum Spacing of the corresponding Metals and then Click “OK”. 

• Similarly, Power Stripes are added using similar content to that of Power Rings.

• On adding Power Stripes, The Power mesh setup is complete as shown. However, There are no Vias that could connect Metal 9 or Metal 8 directly with Metal 1 [VDD or VSS of Standard Cells are generally made up of Metal 1]. 

• The connection between the Highest and Lowest Metals is done through Stacking of Vias done using “Special Route”. 

• To perform Special Route, Select Route → Special Route → Add Nets → OK. 

• After the Special Route is complete, all the Standard Cell Rows turn to the Color coded for Metal 1 

### Fig.10 Power plan 

The complete Power Planning process makes sure Every Standard Cell receives enough power to operate smoothly.
<img width="1920" height="1080" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/f15000f3-56eb-486d-845c-7d2e07236e06" />


#### → Placement 

1. The Placement stage deals with Placing of Standard Cells as well as Pins.
    
2. Select Place → Place Standard Cell → Run Full Placement → Mode → Enable ‘Place I/O Pins’ → OK → OK .
   
• All the Standard Cells and Pins are placed as per the communication between them, i.e., Two communicating Cells are placed as close as possible so that shorter Net lengths can be used for connections as Shorter Net Lengths enable Better Timing Results.

### Fig.11 Placement of standard Cells 

• You can toggle the Layer Visibility from the list on the Right. The List of Layers available are shown on the right under “Layer” tab with colour coding.

<img width="1920" height="1080" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/3e84885f-5f53-48c0-92bf-520c99266ced" />

## Result

Thus, the physical design stages up to placement for the 4-bit up-down counter were completed and verified.
