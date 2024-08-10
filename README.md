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







