# Exp-5-Design-and-Simulate the-Memory-Design-using-Verilog-HDL
# Aim
To design and simulate a RAM,ROM,FIFO using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.
Apparatus Required
Vivado 2023.1
Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the RAM,ROM,FIFO
3. Create the Testbench
Write a testbench to simulate the memory behavior. The testbench should apply various and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output.
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# RAM
# Code
```
module ram(
input clk,rst,en,
input [7:0] d,
input [9:0] a,
output reg [7:0] do);
reg [7:0] ram [1023:0];
always@(posedge clk)
begin
 if(rst)
   do <= 0;
 else if(en)
   ram[a] <= d;       
 else
   do <= ram[a];      
end
endmodule
```
 # Test bench
 ```

module ram_tb;
reg clk_t,rst_t,en_t;
reg [7:0] d_t;
reg [9:0] a_t;
wire [7:0] do_t;
ram dut(.clk(clk_t),.rst(rst_t),.en(en_t),.d(d_t),.a(a_t),.do(do_t));
initial
begin
 clk_t=1'b0;
 rst_t=1'b1;
 en_t=1'b0;
 d_t=8'd0;
 a_t=10'd0;
 #50 rst_t=1'b0; 
 en_t=1'b1; a_t=10'd985; d_t=8'd55;
 #40;
 en_t=1'b1;
 a_t=10'd1000;
 d_t=8'd125;
 #40;
 en_t=1'b0;
 a_t=10'd1000;
 #40;
en_t=1'b0;
a_t=10'd985;
 #40;
 $finish;
end
always #10 clk_t = ~clk_t;
endmodule
```
# output Waveform
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5bf7d566-b3b9-46f7-a8d1-24c98870e991" />

# ROM
 # code
 ```
module rom(
input clk,rst,
input[9:0]a,
output reg [9:0]do );
reg[7:0] rom[1023:0];
initial 
begin
rom[10'd100]=8'd100;
rom[10'd1023]=8'd125;
end
always@(posedge clk)
begin
if(rst)
do<=8'b0;
else
 do<=rom[a];
end
endmodule
```
 
# Test bench
```
module rom_tb;
reg clk_t,rst_t;
reg [9:0] a_t;
wire [7:0] do_t;
rom dut(.clk(clk_t),.rst(rst_t),.a(a_t),.do(do_t));
initial
begin
 clk_t=1'b0;
 rst_t=1'b1;
 a_t=10'd0;
 #50 rst_t=1'b0;
 a_t=10'd100;
 #100;
 a_t=10'd1023;
 #100;
 a_t=10'd200;
 #100;
 $finish;
end
always #10 clk_t=~clk_t;
endmodule
```
# output Waveform
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/652ba9bf-788b-44b3-87ea-41a53e5d948b" />


# Conclusion
The RAM, ROM, FIFO memory with read and write operations was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the memory operations and observing the output waveforms. The experiment demonstrates how to implement memory operations in Verilog, effectively modeling both the reading and writing processes.
 
 

