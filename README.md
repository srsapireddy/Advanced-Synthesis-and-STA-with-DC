# Advanced-Synthesis-and-STA-with-DC
## Introduction
Design Compiler is an Advanced Synthesis Tool used by leading semiconductor companies across world. Design Compiler RTL synthesis solution enables users to meet today's design challenges with concurrent optimization of timing, area, power and test. Design Compiler includes innovative topographical technology that enables a predictable flow resulting in faster time to results.

Synthesis in VLSI is the process of converting your code (program) into a circuit. In terms of logic gates, synthesis is the process of translating an abstract design into a properly implemented chip. Synthesis of logic circuits plays a crucial role in optimizing the logic and achieving the targeted performance, area and power goals of an IC.

This workshop includes the following concepts:

Design fundamentals.
* Setting up DC for synthesis.
* Understanding and Analyzing the STA reports.
* Understanding and writing the Synopsys Design Constraints [SDC].
* Analyzing the quality of netlist synthesized.

## Introduction to Logic Synthesis
1.1. Introduction to DC
* Design Compiler RTL synthesis solution enables users to meet today's design challenges with concurrent optimization of timing, area, power and test. Design Compiler includes innovative topographical technology that enables a predictable flow resulting in faster time to results. Topographical technology provides timing and area prediction within 10% of the results seen post-layout enabling designers to reduce costly iterations between synthesis and physical implementation. Design Compiler also includes a scalable infrastructure that delivers 2X faster runtime on quad-core platforms.

* Design Compiler is the core of Synopsys' comprehensive RTL synthesis solution, including Power Compiler, DesignWare, PrimeTime and DFTMAX. Design Compiler NXT is also available and includes includes best-in-class quality-of-results, congestion prediction and alleviation capabilities, physical viewer, and floorplan exploration. Additionally Design Compiler NXT produces physical guidance to IC Compiler, place-and-route solution for tighter correlation to layout and faster placement runtime.

* The industry's most comprehensive synthesis solution:
![image](https://github.com/user-attachments/assets/73a04b50-a1e6-487a-85f0-e17044298335)
### Benefits:
1. Concurrent optimization of timing, area, power and test.
2. Results correlate within 10% of physical implementation.
3. Removes timing bottlenecks by creating fast critical paths.
4. Gate-to-gate optimization for smaller area on new or legacy designs while maintaining timing Quality of Results (QoR).
5. Cross-probing between RTL, schematic, and timing reports for fast debug.
6. Offers more flexibility for users to control optimization on specific areas of designs.
7. Enables higher efficiency with integrated static timing analysis, test synthesis and power synthesis.
8. Support for multi voltage and multi supply.
9. 2X faster runtime on quad-core compute servers.

# DC SHELL

sky130RTLDesignAndSynthesisWorkshop Directory has: My_Lib - which contains all the necessary library files; where lib has the standard cell libraries to be used in synthesis and verilog_model with all standard cell verilog models for the standard cells present in the lib. Ther verilog_files folder contains all the experiments for lab sessions including both verilog code and test bench codes.

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

## Faster cells and Slower Cells
A cell delay in the digital logic circuit depends on the load of the circuit which here is Capacitance.

Faster the charging / discharging of the capacitance --> Lesser is the Cell Delay

Inorder to charge/discharge the capacitance faster, we use wider transistors that can source more current. This will help us reduce the cell delay but at the same time, wider transistors consumer more power and area. Similarly, using narrower transistors help in reduced area and power but the circuit will have a higher cell delay. Hence, we have to compromise on area and power if we are to design a circuit with low cell delay.

## Constraints
A Constraint is a guidance file given to a synthesizer inorder to enable an optimum implementation of the logic circuit by selecting the appropriate flavour of cells (fast or slow).

# Basics of STA
2.1. Introduction to STA
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface.
![image](https://github.com/user-attachments/assets/a428a6a8-74cb-42b5-a7a6-329825b94f09)



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

## Advanced Constraints
Clock A digital clock is a repeating digital waveform used to step a digital circuit through a sequence of states. A clock signal oscillates between a high and a low state and is used like a metronome to coordinate actions of digital circuits. A clock signal is produced by a clock generator. Digital circuits rely on clock signals to know when and how to execute the functions that are programmed. If the clock in a design is like the heart of an animal, then clock signals are the heartbeats that keep the system in motion. In serial communication of digital data, clock recovery is the process of extracting timing information from a serial data stream to allow the receiving circuit to decode the transmitted symbols. This is one method of performing a process commonly known as clock and data recovery.
![image](https://github.com/user-attachments/assets/91f9ff40-3b67-44c6-b72f-d8679961708f)

## 3.1. Clock Tree Modelling - Uncertainty
Clock uncertainty is the difference between the arrivals of clocks at registers in one clock domain or between domains. it can be classified as static and dynamic clock uncertainties. Pre-layout and Post-layout Uncertainty. Pre CTS uncertainty is clock skew, clock Jitter and margin. After CTS skew is calculated from the actual propagated value of the clock.

Static clock uncertainty: it does not vary or varies very slowly with time. Process variation induced clock uncertainty. An example of this is clock skew.

Timing Uncertainty of clock period is set by the command set_clock_uncertainty at the synthesis stage to reserve some part of the clock period for uncertain factors (like skew, jitter, OCV, CROSS TALK, MARGIN or any other pessimism) which will occur in PNR stage. The uncertainty can be used to model various factors that can reduce the clock period. It can define for both setup and hold.

Skew: This phenomenon in synchronous circuits. The Difference in arrival of clock at two consecutive pins of a sequential element.

max insertion delay: delay of the clock signal takes to propagate to the farthest leaf cell in the design.

min insertion delay: delay of the clock signal takes to propagate to the nearest leaf cell in the design.

Latency: The delay difference from the clock generation point to the clock endpoints.

Source latency: Source latency is also called insertion delay. The delay from the clock source to the clock definition points. Source latency could represent either on-chip or off-chip latency.

Network latency: The delay from the clock definition points (create_clock) to the flip-flop clock pins.

Jitter: Jitter is the short term variations of a signal with respect to its ideal position in time. It is the variation of the clock period from edge to edge.it can vary +/- jitter value. From cycle to cycle the period and duty cycle can change slightly due to the clock generation circuitry. This can be modeled by adding uncertainty regions around the rising and falling edge of the clock waveform.

Sources of jitter:

Internal circuitry of the PLL. Thermal noise in crystal oscillators. Transmitters and receivers of resonating devices.
![image](https://github.com/user-attachments/assets/1c830653-e94b-42c9-b2b4-b59dbf9a1928)



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
![image](https://github.com/user-attachments/assets/d7abf6e0-d196-4d1f-bf7e-f1cc573557a0)

![image](https://github.com/user-attachments/assets/207b3d34-2267-4014-892e-c14652015ce9)

* list_attributes -app > a: Lists all attributes and saves them to a file.
* get_clocks *: Retrieves all clocks in the design.
* create_clock -name MYCLK -period 10 [get_ports clk]: Creates a clock named MYCLK with a 10-unit period on the clk port.
* get_attribute [get_clocks MYCLK] period: Retrieves the period of the clock MYCLK.
* get_attribute [get_clocks MYCLK] is_generated: Checks if MYCLK is a generated clock.
* report_clocks *: Generates a report of all clocks in the design.

![image](https://github.com/user-attachments/assets/4722cc38-70aa-4af7-b495-d61ba463dc6f)


## 25% Duty cycle Clock
![image](https://github.com/user-attachments/assets/15d3f19c-2f53-4e73-be5a-01f3db81018c)

* create_clock -name MYCLK -period 10 [get_ports clk] -wave {0 2.5}: This command creates a clock named MYCLK with a period of 10 time units and a waveform where the clock is high from 0 to 2.5 time units.
* report_clocks *: This command generates a report listing all the clocks in the current design, showing their period, waveform, and attributes.

# Clock Network Modelling - Uncertainty, report_timing
![image](https://github.com/user-attachments/assets/66cc8472-9cd0-42fd-9a5b-9dac13913f4b)

* create_clock -name MYCLK -period 10 [get_ports clk] -wave {15 20}: This command creates a clock named MYCLK with a period of 10 units, and the waveform is specified from 15 to 20 units.
* set_clock_latency -source 1 [get_clocks MYCLK]: This command sets the source latency of the clock MYCLK to 1 unit.
* set_clock_latency 1 [get_clocks MYCLK]: This command sets the clock latency to 1 unit.
* set_clock_uncertainty -hold 0.1 [get_clocks MYCLK]: This command sets the clock uncertainty for the hold time to 0.1 units.
* set_clock_uncertainty 0.5 [get_clocks MYCLK]: This command sets the clock uncertainty for the setup time to 0.5 units.

![image](https://github.com/user-attachments/assets/c026731e-dccc-4414-a1fa-83e2526323c2)
![image](https://github.com/user-attachments/assets/7857734f-9d0d-4bbd-ad6d-2459065f62e5)

```
report_timing -to REGA_reg/Q -delay min
report_timing -to REGA_reg/Q -delay max
```

![image](https://github.com/user-attachments/assets/764d5c42-38eb-481c-9fad-2619e50c422b)
![image](https://github.com/user-attachments/assets/fe6f168a-61fe-4715-804d-229e6dbfe3a7)
* These commands will report the timing paths with the minimum and maximum delays to the output Q of the register REGA_reg.

# IO Delays
Commands:
```
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A]
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_B]
report_port -verbose
```
![image](https://github.com/user-attachments/assets/b6bd4c06-6c07-4a74-b488-044b719a68d9)

```
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_A]
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_B]
report_timing -from IN_A -trans -nosplit
```
![image](https://github.com/user-attachments/assets/f6bed287-7ceb-4b1f-8435-427b8e91999b)
```
set_output_delay -max 5 -clock [get_clocks MYCLK] [get_ports OUT_Y]
set_output_delay -min 1 -clock [get_clocks MYCLK] [get_ports OUT_Y]
report_timing -from OUT_Y -trans -nosplit
```
![image](https://github.com/user-attachments/assets/3c2eb008-dc50-4ffb-a07d-2538d2601410)
```
set_load -max 0.4 [get_ports OUT_Y]
report_timing -to OUT_Y -cap -trans -nosplit
```
![image](https://github.com/user-attachments/assets/787c9d11-9d07-488a-8be6-1b84947af77e)
```
set_load -min 0.1 [get_ports OUT_Y]
report_timing -to OUT_Y -cap -trans -nosplit -delay min
```
![image](https://github.com/user-attachments/assets/20f07e8a-0f8e-464c-8111-87bed232b3ad)

# SDC generated_clk
![image](https://github.com/user-attachments/assets/b397f0fe-abe0-49ab-b7d8-24173a7cc263)

```
create_generated_clock -name MYGEN_CLK -master MYCLK -source [get_ports clk] -div 1 [get_ports out_clk]
report_clocks *
```
![image](https://github.com/user-attachments/assets/43a2dd48-275c-433e-97df-92fba2c451ae)
Creates a generated clock in the current design at a declared source by defining its frequency with respect to the frequency at the reference pin. The static timing analysis tool uses this information to compute and propagate its waveform across the clock network to the clock pins of all sequential elements driven by this source.

The generated clock information is also used to compute the slacks in the specified clock domain that drive optimization tools such as place-and-route.


# SDC vclk, max_latency, rise_fall IO Delays
## Virtual clock - purpose and timing
A virtual clock is used as a reference to constrain the interface pins by relating the arrivals at input/output ports with respect to it with the help of input and output delays.
![image](https://github.com/user-attachments/assets/b2e12118-6e7d-4ed8-ae33-9bf5a81535fc)


```
create_clock –name VCLK –period 10
```
## Set driving cells
It specifies the drive characteristics of input or inout ports that are driven by the cells in the technology library. These commands associate a library pin with input ports so that delay calculation can be accurately modelled.
### VCLK
```
create_clock -name MYCLK -per 10
```
![image](https://github.com/user-attachments/assets/75576339-fe8d-40c4-b7a3-9dc58a42f470)
![image](https://github.com/user-attachments/assets/7f4fd3dd-198f-4391-9360-8e6409f80c81)
![image](https://github.com/user-attachments/assets/d352297a-c675-4b35-a6ba-31e1dcfe8020)
![image](https://github.com/user-attachments/assets/22075028-5b2e-4314-a87e-e41771c1c9ec)
![image](https://github.com/user-attachments/assets/ec61a7e3-9c59-4371-b389-f6079e2012a4)
![image](https://github.com/user-attachments/assets/44f021e0-b40d-4a2f-a3ee-9418c91fc0be)
![image](https://github.com/user-attachments/assets/425f59e6-58de-403f-ab17-eaa4ee763ab8)

























