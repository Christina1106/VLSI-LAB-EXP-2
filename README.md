SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

**LOGIC DIAGRAM**

ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)


DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)


MULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)


DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)


MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)


  
PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

VERILOG CODE

Exp2_Decoder3to8.v
```
module decoder_3to8(
input [2:0]a,
output [7:0]d);
assign d[0]=(~a[2])&(~a[1])&(~a[0]);
assign d[1]=(~a[2])&(~a[1])&(a[0]);
assign d[2]=(~a[2])&(a[1])&(~a[0]);
assign d[3]=(~a[2])&(a[1])&(a[0]);
assign d[4]=(a[2])&(~a[1])&(~a[0]);
assign d[5]=(a[2])&(~a[1])&(a[0]);
assign d[6]=(a[2])&(a[1])&(~a[0]);
assign d[7]=(a[2])&(a[1])&(a[0]);
endmodule
xor G2(S, w1, Ci);
and G3(w2, w1, Ci);
and G4(w3, X, Y);
or G5(Co, w2, w3);
endmodule
```

![Screenshot 2024-04-08 010102](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/a1031021-fdfa-4bda-8dc7-33e8a32f973b)



Exp2_Demultiplexer1to8.v
```
module demux_1_8(y,s,a);
output reg [7:0]y;
input [2:0]s;
input a;
always @(*)
begin
y = 0;
case(s)
3'd0:y[0]=a;
3'd1:y[1]=a;
3'd2:y[2]=a;
3'd3:y[3]=a;
3'd4:y[4]=a;
3'd5:y[5]=a;
3'd6:y[6]=a;
3'd7:y[7]=a;
endcase
end
endmodule
```
![Screenshot 2024-04-07 225836](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/2c85cb4f-d9f2-4203-9053-b0bb6528e549)
![Screenshot 2024-04-07 225929](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/f6bdedee-0b96-4b15-a383-2d357ce8fc65)


Exp2_Encoder8to3.v
```
module encoder_8_to_3(a0,a1,a2,d0,d1,d2,d3,d4,d5,d6,d7); 
input d0,d1,d2, d3,d4,d5,d6,d7;
output a0, a1,a2;
assign a0 (d1 | d3 | d5 | d7);
assign a1=(d2 | d3 | d6 | d7);
assign a2 = (d4 | d6 | d5 | d7);
endmodule
```
![Screenshot 2024-04-21 225422](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/8df21f28-e407-4105-ad9f-29f23197a682)
![image](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/4e2cd811-6e7c-46ec-af90-223a7283081c)


Exp2_Magnitudecomparator.v
```
module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
if (a==b)
begin
eq = 1'b1;
lt = 1'b0;
gt = 1'b0;
end
else if (a>b)
begin
eq = 1'b0;
lt = 1'b0;
gt = 1'b1;
end
begin
eq = 1'b0;
lt = 1'b1;
gt = 1'b0;
end
end
endmodule
```
![Screenshot 2024-04-07 232645](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/405455dd-ef9e-4eb8-acfd-43a5de31aeef)
![Screenshot 2024-04-21 204953](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/492bc624-78cd-4af5-a82d-cb61e585f19c)




Exp2_Multiplexer8to1.v
```
module mux_8tol (in, sel, out);
input [7:0] in: input [2:0] sel;
output reg out;
always @(*)
begin
case (sel)
3'b000: out = in[0];
3'b001: out = in[1];
3'b010: out = in[2];
3'b011: out = in[3];
3'b100: out = in[4];
3'b101: out = in[5];
3'b110: out = in[6];
3'b111: out = in[7];
default: out = 1'bx;
endcase
end
endmodule
```
![Screenshot 2024-04-07 222858](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/8234cefe-2b7c-41ee-822e-6c8d73593b0c)
![Screenshot 2024-04-07 223310](https://github.com/Christina1106/VLSI-LAB-EXP-2/assets/161043650/8b94b474-fdc1-4b76-b700-25a8e8996ee4)



RESULT


