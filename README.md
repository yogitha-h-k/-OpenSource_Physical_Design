# -OpenSource_Physical_Design
contents studied and created during the Advanced Physical Design Workshop using OpenLANE and SKY130 PDK

Introduction To RTL to GDSII Flow

RTL Synthesis
Static Timing Analysis(STA)
Design for Testability(DFT)
Floorplanning
Placement
Clock Tree Synthesis(CTS)
Routing
GDSII Streaming


About Google SkyWater PDK

DAY 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
step-1:./flow.tcl is the script which runs the OpenLANE flow and -interactive starts the flow in the interactive mode. 
![image](https://user-images.githubusercontent.com/93296554/183036477-9219a889-10ad-4cf0-b04c-30626fde92a9.png)
step2 :imprting openlane packages:package require openlane 0.9
step3:preparing the design:prep -design picorv32a
step4:run_synthesis(the design is synthesised!)


![image](https://user-images.githubusercontent.com/93296554/183043895-e6437db4-f2d1-4885-af0d-4bdd7d907f5d.png)


![image](https://user-images.githubusercontent.com/93296554/183045846-e2e93650-a109-4a27-9664-d6f4f90ec7eb.png)

Flop percentage=10.84%(no of dflops/total number of cells)

DAY 2- Good floorplan vs bad floorplan and introduction to library cells
Chip Floorplanning:
The placement of logical blocks, library cells, and pins on a silicon chip is known as chip floorplanning. The allocation is completed to fit the given space and aspect ratio.

Utilization Factor and Aspect Ratio:
Utilization Factor is a measure of how much of the entire core area is used by standard cells.

Power Planning:
Power planning is done to set up a network for the cell's supply of power.
The undesired voltage drop and ground bounce are rectified in this stage.

Pin Placement:
Pin placement is a important part of floorplanning as the timing delays and number of buffers required is dependent on the position of the pin.
![image](https://user-images.githubusercontent.com/93296554/183027044-85a85d29-1397-42a8-8e89-fbf258de59a5.png)

Noise margin should be considered as interconnects have certain L and R.Hence the use of Decouple capacitors.
![image](https://user-images.githubusercontent.com/93296554/183028188-206fd7bf-4734-4339-98f9-8e1f1fc47831.png)

Arragement of blocks along with Decouple capacitors:

![image](https://user-images.githubusercontent.com/93296554/183028919-5b035f1a-75e3-4761-bbe6-956070978488.png)


Lab:

technology file|merged LEF file|DEF File are used here.
![image](https://user-images.githubusercontent.com/93296554/183049382-6dabe73e-ddd5-405d-b903-31e4eb3f756f.png)

Magic tool is used to vizualize the layout of the floorplan.
![image](https://user-images.githubusercontent.com/93296554/183049231-3a62c68c-7121-49a4-a330-b97378459806.png)

![image](https://user-images.githubusercontent.com/93296554/183049859-cb717a38-c28e-4a4d-a077-46d496cbbf01.png)


PLACEMET:run_placement
Placement uses the DEF file produced during floorplan as an input. In OpenLANE, placement happens in two steps:

Global Placement
Detailed Placement
![image](https://user-images.githubusercontent.com/93296554/183334581-e19faf71-da39-4e07-ac65-46caaaad9c6e.png)

![image](https://user-images.githubusercontent.com/93296554/183291764-db966abb-17e5-44c4-baac-adfed294c525.png)





DAY-3

![image](https://user-images.githubusercontent.com/93296554/183249821-f9be73d9-7f8d-4fdf-831b-3ddc8497d218.png)

![image](https://user-images.githubusercontent.com/93296554/183250317-8875eeac-065b-470a-b804-e2173031f333.png)
![image](https://user-images.githubusercontent.com/93296554/183250478-874174f7-06e5-4d57-b5f1-cab4de905c1d.png)
![image](https://user-images.githubusercontent.com/93296554/183251138-f09f97fd-f0ba-4a2d-a5c2-14e422efe97a.png)
![image](https://user-images.githubusercontent.com/93296554/183256363-528a8086-8519-4ce4-a9b6-78da772e8600.png)


![image](https://user-images.githubusercontent.com/93296554/183291873-fd1047dd-b0fe-40a1-bf72-f5ff73338c45.png)



DAY 4
grid for routing using info file


![image](https://user-images.githubusercontent.com/93296554/183281052-fc4b1ed6-ad98-4369-a534-8bdf704139ad.png)


![image](https://user-images.githubusercontent.com/93296554/183291930-4a68474e-8b38-4abf-9b11-140d22ef6160.png)

![image](https://user-images.githubusercontent.com/93296554/183292049-023c6d7c-db4a-483a-9ec7-ee908b6feade.png)

DAY 5

run_routing
![image](https://user-images.githubusercontent.com/93296554/183292114-4ac1f7fb-b950-4952-9062-0a8a0b14821d.png)
![image](https://user-images.githubusercontent.com/93296554/183292171-c04916dd-380c-4680-90de-cb1e9782cf09.png)
![image](https://user-images.githubusercontent.com/93296554/183292197-3277da3d-dae6-492e-b6fc-c18343461c68.png)




![image](https://user-images.githubusercontent.com/93296554/183291977-fcbb0418-96c9-464b-9c79-a31230033bc3.png)

Use the following commands before creating the power distribution network :
 openroad
 read_db picorv32_cts.db  
 read_liberty $::env(LIB_SYNTH_COMPLETE) 
 link_design picorv32a
 read_sdc ...../src/my_base.sdc
 set_propagated_clock [all_clocks]
 report_checks -path_delay min_max -format full_clock_expanded -digits 4
 
For generating the power distribution network we use the following command :
gen_pdn

after routing design in magic:
![image](https://user-images.githubusercontent.com/93296554/183292309-0f415fe5-9ec7-46cc-9c20-a9fb7be27a00.png)







