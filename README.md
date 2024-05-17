EXP-1

DATE:


SIMULATION AND IMPLEMENTATION OF LOGIC GATES, ADDERS AND SUBTRACTORS
## AIM: 
To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

## APPARATUS REQUIRED: 
Xilinx 14.7 Spartan6 FPGA

## PROCEDURE: 
STEP:1 Start the Xilinx navigator, Select and Name the New project. 

STEP:2 Select the device family, device, package and speed.

STEP:3 Select new source in the New Project and select Verilog Module as the Source type. 

STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.

STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax.

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 

STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window. 

STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained.

STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. STEP:12 Load the Bit file into the SPARTAN 6 FPGA

STEP:11 On the board, by giving required input, the LEDs starts to glow light, indicating the output.

## Logic Gates:
### Logic Diagram :

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)

### VERILOG CODE:
```
module alllgates(a,b,w1,w2,w3,w4,w5,w6,w7);
input a,b;
output w1,w2,w3,w4,w5,w6,w7;
and g1(w1,a,b);
or g2(w2,a,b);
not g3(w3,a);
xor g4(w4,a,b);
xnor g5(w5,a,b);
nand g6(w6,a,b);
nor g7(w7,a,b); 
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/f7f8604f-f676-498e-97da-25bf8b7aed34)

## Half Adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)

### VERILOG CODE:
```
module halfadder(x,y,s,c);
input x,y;
output s,c;
xor g1(s,x,y);
and g2(c,y,x);
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/6f587021-ab61-4a75-9d69-a3d7ff867265)

## Full adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)

### VERILOG CODE:
```
module fulladder(a,b,cin,sum,carry);
input a,b,cin;
output sum,carry;
wire w1,w2,w3;
xor g1(w2,a,b);
and g2(w1,b,a);
xor g3(sum,w2,cin);
and g4(w3,cin,w2);
or g5(carry,w3,w1);
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/6a0fec58-7f25-4ebd-8c61-e1b1c275d14e)

## Half Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)

### VERILOG CODE:
```
module halfsubtractor(x,y,d,b);
input x,y;
output d,b;
wire w;
xor g1(d,x,y);
not g2(w,x);
and g3(b,y,w);
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/4cbf1e5f-1524-4e51-a56c-631a18539e70)

## Full Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)

### VERILOG CODE:
```

module fullsub(a,b,bin,diff,borrow);
input a,b,bin;
output diff,borrow;
wire w1,w2,w3,w4,w5;
xor g1(w3,a,b);
not g2(w1,a);
and g3(w2,b,w1);
xor g4(diff,w3,bin);
not g5(w4,w3);
and g6(w5,bin,w4);
or g7(borrow,w5,w2);
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/9f3daa25-88d4-4fff-bd5e-6fda0860ad48)

## 8 Bit Ripple Carry Adder

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)

### VERILOG CODE:
```
module ripplemod(a, b, cin, sum, cout);
input [07:0] a;
input [07:0] b;
input cin;
output [7:0]sum;
output cout;
wire[6:0] c;
fulladd a1(a[0],b[0],cin,sum[0],c[0]);
fulladd a2(a[1],b[1],c[0],sum[1],c[1]);
fulladd a3(a[2],b[2],c[1],sum[2],c[2]);
fulladd a4(a[3],b[3],c[2],sum[3],c[3]);
fulladd a5(a[4],b[4],c[3],sum[4],c[4]);
fulladd a6(a[5],b[5],c[4],sum[5],c[5]);
fulladd a7(a[6],b[6],c[5],sum[6],c[6]);
fulladd a8(a[7],b[7],c[6],sum[7],cout);
endmodule
module fulladd(a, b, cin, sum, cout);
input a;
input b;
input cin;
output sum;
output cout;
assign sum=(a^b^cin);
assign cout=((a&b)|(b&cin)|(a&cin));
endmodule
```

### Output:
![image](https://github.com/SanthoshK265/vlsilab-EXP-1/assets/143738585/6c9f11f2-7561-4e86-86d8-bd7e53018c7e)

## RESULT:
Thus the Logic Gates, Adders and Subtractors are Synthesis and stimulated Successfully Using Xilinx ISE.
