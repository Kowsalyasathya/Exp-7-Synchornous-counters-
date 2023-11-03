# Exp-6-Synchornous-counters - up counter and down counter 
## AIM: To implement 4 bit up and down counters and validate  functionality.
## HARDWARE REQUIRED:  
PC, Cyclone II , USB flasher
## SOFTWARE REQUIRED:  
Quartus prime
## THEORY 
## UP COUNTER 
The counter is a digital sequential circuit and here it is a 4 bit counter, which simply means it can count from 0 to 15 and vice versa based upon the direction of counting (up/down). 

The counter (“count“) value will be evaluated at every positive (rising) edge of the clock (“clk“) cycle.
The Counter will be set to Zero when “reset” input is at logic high.
The counter will be loaded with “data” input when the “load” signal is at logic high. Otherwise, it will count up or down.
The counter will count up when the “up_down” signal is logic high, otherwise count down

Since we know that binary count sequences follow a pattern of octave (factor of 2) frequency division, and that J-K flip-flop multivibrators set up for the “toggle” mode are capable of performing this type of frequency division, we can envision a circuit made up of several J-K flip-flops, cascaded to produce four bits of output.
The main problem facing us is to determine how to connect these flip-flops together so that they toggle at the right times to produce the proper binary sequence.
Examine the following binary count sequence, paying attention to patterns preceding the “toggling” of a bit between 0 and 1:
Binary count sequence, paying attention to patterns preceding the “toggling” of a bit between 0 and 1.

Note that each bit in this four-bit sequence toggles when the bit before it (the bit having a lesser significance, or place-weight), toggles in a particular direction: from 1 to 0. 

Starting with four J-K flip-flops connected in such a way to always be in the “toggle” mode, we need to determine how to connect the clock inputs in such a way so that each succeeding bit toggles when the bit before it transitions from 1 to 0.

The Q outputs of each flip-flop will serve as the respective binary bits of the final, four-bit count:
Four-bit “Up” Counter
![image](https://user-images.githubusercontent.com/36288975/169644758-b2f4339d-9532-40c5-af40-8f4f8c942e2c.png)
## DOWN COUNTER 
As well as counting “up” from zero and increasing or incrementing to some preset value, it is sometimes necessary to count “down” from a predetermined value to zero allowing us to produce an output that activates when the zero count or some other pre-set value is reached.

This type of counter is normally referred to as a Down Counter, (CTD). In a binary or BCD down counter, the count decreases by one for each external clock pulse from some preset value. Special dual purpose IC’s such as the TTL 74LS193 or CMOS CD4510 are 4-bit binary Up or Down counters which have an additional input pin to select either the up or down count mode.
![image](https://user-images.githubusercontent.com/36288975/169644844-1a14e123-7228-4ed8-81a9-eb937dff4ac8.png)
4-bit Count Down Counter
## Procedure
1.Create a New Project: Open Quartus and create a new project by selecting "File" > "New Project Wizard." Follow the wizard's instructions to set up your project, including specifying the project name, location, and target device (FPGA).

2.Create a New Design File: Once the project is created, right-click on the project name in the Project Navigator and select "Add New File." Choose "Verilog HDL File" or "VHDL File," depending on your chosen hardware description language.

3.Write the Combinational Logic Code: Open the newly created Verilog or VHDL file and write the code for your combinational logic.

4.Compile the Project: To compile the project, click on "Processing" > "Start Compilation" in the menu. Quartus will analyze your code, synthesize it into a netlist, and perform optimizations based on your target FPGA device.

5.Analyze and Fix Errors: If there are any errors or warnings during the compilation process, Quartus will display them in the Messages window. Review and fix any issues in your code if necessary. View the RTL diagram.

6.Verification: Click on "File" > "New" > "Verification/Debugging Files" > "University Program VWF". Once Waveform is created Right Click on the Input/Output Panel > " Insert Node or Bus" > Click on Node Finder > Click On "List" > Select All. Give the Input Combinations according to the Truth Table amd then simulate the Output Waveform.
## PROGRAM 
/*
Program for flipflops  and verify its truth table in quartus using Verilog programming.
Developed by: Kowsalya M
RegisterNumber:  212222230069
*/
### UPCOUNTER:
```
module upcounter(A,clk);
output reg [3:0]A;
input clk;
always@(posedge clk)
begin
A[0]=((((A[1])&(A[2]))&A[3])^A[0]);
A[1]=(((A[2])&(A[3]))^A[1]);
A[2]=((A[3])^A[2]);
A[3]=1^A[3];
end
endmodule
```
### DOWNCOUNTER:
```
module downcounter(A,clk);
output reg [3:0]A;
input clk;
always@(posedge clk)
begin
A[3]=((((~A[2])&(~A[1]))&(~A[0]))^A[3]);
A[2]=(((~A[1])&(~A[0]))^A[2]);
A[1]=((~A[0])^A[1]);
A[0]=1^A[0];
end
endmodule
```
## RTL LOGIC UP COUNTER AND DOWN COUNTER
### UPCOUNTER:
![279398776-6401bf5e-8663-4a53-9df4-3d56cc9dbfe7](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/410ca56e-453b-49e5-8445-18391ee37c4c)
### DOWNCOUNTER:
![279398898-1a3a27a1-8818-4720-b09f-047f3de2317f](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/37e80418-e5f1-4049-826d-8d53c8dab962)
## TIMING DIGRAMS FOR COUNTER  
### UPCOUNTER WAVEFORM:

![279399047-691b2ef4-bfa8-410e-9294-e4388d85fbd4](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/b29b9e50-034f-4d53-afd4-568b311de03d)
### DOWNCOUNTER WAVEFORM:
![279399451-6767f1a4-1887-4585-9e20-0d764334ccb6](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/d8811d4e-5570-4648-8ff2-eb3641711c47)
### TRUTH TABLE :
### UPCOUNTER TURTH TABLE:
![279399682-ddb0687a-2f30-4ba0-81ab-38c4ad0ae129](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/6c96e705-67d0-4080-a2cd-139b732741d4)

### DOWNCOUNTER TURTH TABLE:
![279399824-08b44849-7624-4ce4-95ba-d78c9534d516](https://github.com/Kowsalyasathya/Exp-7-Synchornous-counters-/assets/118671457/96964a34-f48a-4642-94f2-c79b3ced2e4f)
## RESULTS :
Thus, The Synchornous counters of up counter and down counter circuit are studied and the truth table for different logic gates are Successfully verified.
