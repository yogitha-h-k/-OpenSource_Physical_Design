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




DAY-3-Design library cell using Magic Layout and ngspice characterization

How polysilicon is placed using photolithography:
![image](https://user-images.githubusercontent.com/93296554/183250317-8875eeac-065b-470a-b804-e2173031f333.png)

LDD-Lightly doped drain(concept of P+,P- and N+,N-)
![image](https://user-images.githubusercontent.com/93296554/183250478-874174f7-06e5-4d57-b5f1-cab4de905c1d.png)

Final design to fabricate after 16 mask layers

![image](https://user-images.githubusercontent.com/93296554/183251138-f09f97fd-f0ba-4a2d-a5c2-14e422efe97a.png)


Magic Tool offers a very user-friendly interface for designing the different layers of the layout. Additionally, it includes  DRC check fetaure. The  below displays a CMOS Inverter configuration.


![image](https://user-images.githubusercontent.com/93296554/183249821-f9be73d9-7f8d-4fdf-831b-3ddc8497d218.png)



Extract SPICE Netlist from Standard Cell Layout:
Extract the circuit from the layout design.
extract all
Convert the extracted circuit to SPICE model.
ext2spice cthresh 0 rthresh 0
ext2spice

![image](https://user-images.githubusercontent.com/93296554/183256363-528a8086-8519-4ce4-a9b6-78da772e8600.png)


![image](https://user-images.githubusercontent.com/93296554/183335891-d0e0a025-2ecc-4e15-bbf7-a4177bc256a2.png)



The waveform of the inverter's output relative to input is depicted in the figure below. This waveform is used to determine a number of timing metrics, including rise time delay, fall time delay, and propagation delay.


![image](https://user-images.githubusercontent.com/93296554/183291873-fd1047dd-b0fe-40a1-bf72-f5ff73338c45.png)


DAY 4:

![image](https://user-images.githubusercontent.com/93296554/183347790-a7ee3e8f-4302-402f-a969-9e0210550644.png)

 setting grid for routing by using the above values (using info file)
 ![image](https://user-images.githubusercontent.com/93296554/183281052-fc4b1ed6-ad98-4369-a534-8bdf704139ad.png)
 
 To create the lef file:lef write
This is the lef file that was created and describes the ports of the layout.

![image](https://user-images.githubusercontent.com/93296554/183349935-87c13a14-00fe-4a00-bfad-8f1157a9ea24.png)


![image](https://user-images.githubusercontent.com/93296554/183350855-9642a690-9281-4d2a-81ac-3335be9baf69.png)
area with delay:0:196832.720![image](https://user-images.githubusercontent.com/93296554/183350913-f049d95a-264c-4f4a-a939-e0a608ef8e7a.png)
area with delay = 1: 209181.872![image](https://user-images.githubusercontent.com/93296554/183351016-87d6300c-3369-4fc1-873c-ee4c58428405.png)

STATIC TIMMING ANALYSIS:

![image](https://user-images.githubusercontent.com/93296554/183351851-523d7806-2072-4a89-8249-ed405269284e.png)

The following code needs to be written to a file called pre_sta.conf inside openlane dir:

set_cmd_units -time ns -capacitance pf -current mA -voltage V -resistance kOhm -distance um
read_liberty -max ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
read_verilog /home/mariosurfe91/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/lab2/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns

Copy the following sdc example file out of scripts.

set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 12.000
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.65
set ::env(SYNTH_MAX_FANOUT) 4

set IO_PCT 0.2
create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set input_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]

![image](https://user-images.githubusercontent.com/93296554/183352342-4d9e0362-f766-4b7e-a832-4b6adfcce8ae.png)

static timing analysis inside opnelane flow.tcl
execute command openroad and the follwing commands:


openroad
read_lef /openLANE_flow/designs/picorv32a/runs/lab2/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/lab2/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/lab3/results/synthesis/picorv32a.synthesis_cts.v
read_liberty -min $::env(LIB_FASTEST)
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4

![image](https://user-images.githubusercontent.com/93296554/183354342-320f1fa2-f5b4-4410-92e3-18c9981a6312.png)


Clock Tree Synthesis using TritonCTS

With OpenLANE, the TritonCTS tool is used to create clock trees. As CTS is conducted on a placement, it should always be done after floor layout and placement. def file produced during the placement phase.


The OpenLANE command used to run CTS:run_cts







!
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







