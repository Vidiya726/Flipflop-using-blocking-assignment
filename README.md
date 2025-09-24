# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps

module SR_FF(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=0;
else
    begin
    case ({s,r})
        2'b00:q=q;
        2'b01:q=1'b0;
        2'b10:q=1'b1;
        2'b11:q=1'bx;
    endcase
    end
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_SR_FF;
reg s,r,clk,rst;
wire q;
SR_FF uut(s,r,clk,rst,q);
always
#5 clk =~clk;
initial begin
    clk=0;s=0;r=0;rst=1;
    #10 rst=0;
    #10 s=1;r=0;
    #10 s=0;r=0;
    #10 s=0;r=1;
    #10 s=1;r=1;
    #10 s=0;r=0;
    #20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="Screenshot 2025-09-21 120244" src="https://github.com/user-attachments/assets/953973e6-9f25-4b0a-8e2c-2eba1578d820" />


### JK Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module JK_FF(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=0;
else if (j==0 && k==0)
q=q;
else if (j==0 && k==1)
q=1'b0;
else if (j==1 && k==0)
q=1'b1;
else
q=~q;
end
endmodule

```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_JK_FF;
reg j,k,clk,rst;
wire q;
JK_FF uut(j,k,clk,rst,q);
always
#5 clk =~clk;
initial begin
    clk=0;j=0;k=0;rst=1;
    #10 rst=0;
    #10 j=1;k=0;
    #10 j=0;k=0;
    #10 j=0;k=1;
    #10 j=1;k=1;
    #10 j=0;k=0;
    #20 $finish;
    end
endmodule


```
#### SIMULATION OUTPUT

<img width="1918" height="1075" alt="Screenshot 2025-09-21 123522" src="https://github.com/user-attachments/assets/b1e28ca6-e9aa-4601-8250-071e088a3fe9" />


### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module D_FF(clk,rst,d,q);
input clk,rst,d;
output reg q;
always @ (posedge clk)
begin
if(rst==1)
    q=0;
else 
    q=d;
end
endmodule


```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module D_FF_tb;
reg clk,rst,d;
wire q;
D_FF uut(clk,rst,d,q);
always #5 clk = ~clk;
initial
begin
clk=0;
d=0;
rst=1;
#10
rst=0;
d=0;
#10
d=1;
end
endmodule


```

#### SIMULATION OUTPUT
<img width="1919" height="1079" alt="Screenshot 2025-09-24 083517" src="https://github.com/user-attachments/assets/81de3339-44b1-4561-b4b3-56dd2ffebbe9" />

### T Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module T_FF(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @ (posedge clk)
begin
if(rst==1)
    q=0;
else if(t==0)
    q=q;
else
    q=~q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module T_FF_tb;
reg clk,rst,t;
wire q;
T_FF uut(clk,rst,t,q);
always #5 clk = ~clk;
initial
begin
clk=0;
t=0;
rst=1;
#10
rst=0;
t=0;
#10
t=1;
end
endmodule


```

#### SIMULATION OUTPUT


<img width="1918" height="1079" alt="Screenshot 2025-09-21 124746" src="https://github.com/user-attachments/assets/00179f5d-c9b1-4526-a2e7-7c9e7f54a07a" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
