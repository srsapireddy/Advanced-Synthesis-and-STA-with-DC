# Advanced-Synthesis-and-STA-with-DC

# DC SHELL
## Running DC Shell
```
dc_shell -64
```
![image](https://github.com/user-attachments/assets/20bc7c52-9e65-4428-a24a-c6aa0c7055ff)

## DC Shell Synthesis
```
set search_path [list /home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files]
set target_library "/home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db"
set link_library "* $target_library"

read_verilog lab1_flop_with_en.v
current_design lab1_flop_with_en

compile

write -f verilog -out synthesized_lab1_flop_with_en.v

```

### Generated Synthesized File
#### Verilog File
![image](https://github.com/user-attachments/assets/9f2654a5-bda7-4bad-8520-a2e36d3f5b0f)
#### Synthesized File
![image](https://github.com/user-attachments/assets/84681ab6-f9b4-4705-8e7f-cb36bed2bedb)

# DESIGN VISION
### Invoking Design Vision
![image](https://github.com/user-attachments/assets/9f9f0e87-c97a-4abb-ba9c-344a8a7dbaf5)

### Design Vision Logical Hierarchy window
#### Commands
```
set target_library "/home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db"
set link_library "* $target_library"
read_file -format verilog /home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab1_flop_with_en.v
current_design lab1_flop_with_en
compile
```
### After running commands
![image](https://github.com/user-attachments/assets/55d1d94a-0f75-447a-90f7-eb08b08386d8)

### Schematic View of the design
![image](https://github.com/user-attachments/assets/f06c77d3-1c40-47a5-970e-0dbaa81669ff)

# Basics of STA
### Exploring library files
![image](https://github.com/user-attachments/assets/4de6a464-3a84-4b7d-873a-03408b37ade3)
![image](https://github.com/user-attachments/assets/b57a4be9-2485-4de1-b530-87f3127b3dab)
![image](https://github.com/user-attachments/assets/52049a03-141d-4a5e-b237-a5419958af80)

## Commands to load design
```
set target_library "/home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db"
set link_library "* $target_library"
read_file -format verilog /home/ssdx5/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_circuit.v
current_design lab8_circuit
```

## GET NETS
![image](https://github.com/user-attachments/assets/f374f041-e7fe-4aab-9af5-33a91ff9bf85)

## GET CELLS
![image](https://github.com/user-attachments/assets/e50124f9-1497-477f-9ba6-db98f1e0b0a2)
The process began by setting a variable cell_obj to represent cell U6 using the get_cells command, which was successful. However, when attempting to list attributes of this cell with list_attributes $cell_obj, an error occurred. This error suggests that the command might not be properly recognized, or there may be an issue with how the tool interprets the cell object.

Next, the clear command was used, but this resulted in an error since clear is not a valid command in the dc_shell environment. Following this, all cells in the design were listed using get_cells *, which correctly returned the cells q_reg, U5, and U6.

The commands then checked whether cells U6 and U5 were hierarchical using the get_attribute command. The tool returned no value for U6, indicating it is not hierarchical, and returned false for U5, confirming it is also not hierarchical.

An attempt was made to filter cells based on their hierarchical status using get_cells * -hierarchical -filter "is_hierarchical == false", but this command failed. The error message indicated that the tool found the command ambiguous or misinterpreted it, suggesting the filtering syntax was incorrect or unsupported in this context.

A foreach_in_collection loop was then successfully used to iterate over all hierarchical cells, retrieve each cell's name and reference name (or type), and print them. This command returned three cells: q_reg, U5, and U6, along with their corresponding types, which are sky130_fd_sc_hd__dfrtp_1, sky130_fd_sc_hd__mux2_1, and sky130_fd_sc_hd__clkinv_1, respectively.

Finally, the current design was successfully written to a DDC (Design Data Compiler) file named lab8_circuit.ddc using the write -f ddc -out lab8_circuit.ddc command. Despite earlier issues with command interpretation, the design was correctly saved to a file, indicating the process was ultimately successful.

## GET_PORTS
![image](https://github.com/user-attachments/assets/47848d1a-7d84-4314-87ee-5ba0063cb12a)
* get_ports *: Lists all ports in the design.
* foreach_in_collection my_port [get_ports *] { ... }: Loops over all ports to retrieve and print their names and/or attributes.
* get_ports rst: Retrieves a specific port named rst.
* get_attribute [get_ports rst] direction: Retrieves the direction (input/output) of the rst port.

# Loading Design get_pins, get_clocks, querying_clocks
### get_pins
![image](https://github.com/user-attachments/assets/a218b5d8-5a26-4532-8d10-f932a03fcac1)
* get_pins *: Lists all pins in the design.
* foreach_in_collection my_pin [get_pins *] { ... }: Loops over all pins to retrieve and print their names.

### list_attributes
```
list_attributes -app > a
```
![image](https://github.com/user-attachments/assets/c22165d4-2d62-41ca-8ed1-ea91af9fea1b)
* The list_attributes command with the -app option is used to list all relevant attributes for the current application context, which in this case includes clock-related and pin-related attributes.
* Redirecting the output to a file makes it easier to handle and review, especially when there are many attributes.

# Creating Clock Waveforms for lab8_circuit
![image](https://github.com/user-attachments/assets/7a3061b5-bfaf-4d90-acd6-ea5de35c3159)
![image](https://github.com/user-attachments/assets/367be343-5c51-42ea-9c54-d9a40aca7a22)
* list_attributes -app > a: Lists all attributes and saves them to a file.
* get_clocks *: Retrieves all clocks in the design.
* create_clock -name MYCLK -period 10 [get_ports clk]: Creates a clock named MYCLK with a 10-unit period on the clk port.
* get_attribute [get_clocks MYCLK] period: Retrieves the period of the clock MYCLK.
* get_attribute [get_clocks MYCLK] is_generated: Checks if MYCLK is a generated clock.
* report_clocks *: Generates a report of all clocks in the design.

![image](https://github.com/user-attachments/assets/158e489d-eb5d-4310-b673-8da87bb354f2)

## 25% Duty cycle Clock
![image](https://github.com/user-attachments/assets/e614d3bb-1fe4-4ecb-8e78-cd2c3e314450)
* create_clock -name MYCLK -period 10 [get_ports clk] -wave {0 2.5}: This command creates a clock named MYCLK with a period of 10 time units and a waveform where the clock is high from 0 to 2.5 time units.
* report_clocks *: This command generates a report listing all the clocks in the current design, showing their period, waveform, and attributes.

# Clock Network Modelling - Uncertainty, report_timing
![image](https://github.com/user-attachments/assets/93314a7f-4928-4b26-8227-c3047c3b95fa)
* create_clock -name MYCLK -period 10 [get_ports clk] -wave {15 20}: This command creates a clock named MYCLK with a period of 10 units, and the waveform is specified from 15 to 20 units.
* set_clock_latency -source 1 [get_clocks MYCLK]: This command sets the source latency of the clock MYCLK to 1 unit.
* set_clock_latency 1 [get_clocks MYCLK]: This command sets the clock latency to 1 unit.
* set_clock_uncertainty -hold 0.1 [get_clocks MYCLK]: This command sets the clock uncertainty for the hold time to 0.1 units.
* set_clock_uncertainty 0.5 [get_clocks MYCLK]: This command sets the clock uncertainty for the setup time to 0.5 units.

![image](https://github.com/user-attachments/assets/b08aa46b-146a-43ff-b4ee-2e432065cc96)











