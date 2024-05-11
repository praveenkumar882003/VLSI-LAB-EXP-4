# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS


**AIM :**
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.2.
 
**APPARATUS REQUIRED :** Vivado™ ML 2023.2
   
**PROCEDURE:**

1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)



**EXPERIMENTS :**

#1

D FLIP FLOP :-

Code:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
OUTPUT:-

Simulation :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/f4e4c4bb-00ae-4af4-9ade-c29148506622)


Elaborated Design : 

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/dfea0900-e135-41d5-8069-83c57fdd66bb)

#2

JK FLIP FLOP:-

Code:

```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```

OUTPUUT:-

Simulation Output:

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/59657390-64cd-45b3-b682-3b3402599cd7)

Elaborated Design:

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/ac32b15d-c5f9-410f-b164-5f0edd482fc8)

#3

MOD 10 COUNTER :-

Code :
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```

OUTPUT:-

Simulation :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/c7c9d5f9-c4c1-4cf3-afaa-37fae535bbbf)


Elaborated Design :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/36fa6bf5-bd9a-4409-90a5-3363c06016ea)


#4

Ripple Counter:-

Code :

```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```

OUTPUT:-

Simulation:

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/82e833de-ed3e-4be7-84a8-575e9ca6ba59)


Elaborated Design :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/693992cc-accf-4c32-87ee-833fee1991fa)

#5

SR FLIPFLOP :-

Code :
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```

OUTPUT:-

Simulation :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/790c549b-2ee1-4465-9d37-be8013e3c3ee)

Elaborated Design :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/91c30531-ba14-417b-90f8-49854ecb55cd)

#6

T FLIP FLOP :-

Code :
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```

OUTPUT:-

Simulation :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/5f9a0f68-127d-4ef2-89f6-63d082c4754e)

Elaborated Design :

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/c2e7da26-b435-4f2b-a0bc-c5cc1f511b12)

#7

UP DOWN COUNTER :-

Code:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

OUTPUT:-

Simulation:-

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/482318ce-7631-4fab-9c34-f8fa88e0a95b)

Elaborated Design:-

![image](https://github.com/lycanthrope004/VLSI-LAB-EXP-4/assets/121667830/4c02787d-aec7-4d1f-bfcb-bfdf2cdc5577)


RESULT :

Simulate And Synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN is  Successfully Verified using Vivado Software.

