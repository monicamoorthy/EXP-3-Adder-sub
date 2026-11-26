# EXP-3-Adder-sub
## Design and Verification of Half Adder and Half Subtractor<br><br>
### Aim
To design and verify basic one-bit arithmetic circuits using Verilog HDL.<br><br>
### Theory / Synopsis
A Half Adder adds two single-bit binary numbers, A and B, and produces a Sum and a Carry output. A Half Subtractor subtracts one single-bit binary number B from another A, producing a Difference and a Borrow output. Both circuits are purely combinational and form the basic building blocks of larger arithmetic units such as Full Adders and Full Subtractors.<br><br>

Boolean Functions<br>

Half Adder:<br>
•	Sum = A ⊕ B<br>
•	Carry = A . B<br>
Half Subtractor:<br>
•	Difference = A ⊕ B<br>
•	Borrow = A' . B<br><br>

### Files to be Created<br>
File name	Purpose<br>
half_add_sub.v	Arithmetic-circuit RTL<br>
half_add_sub_tb.v	Stimulus and VCD generation<br><br>

### Verilog Program<br>
```
module half_adder (
    input  wire A,
    input  wire B,
    output wire Sum,
    output wire Carry
);
    assign Sum   = A ^ B;   // XOR
    assign Carry = A & B;   // AND
endmodule
 
module half_subtractor (
    input  wire A,
    input  wire B,
    output wire Diff,
    output wire Borrow
);
    assign Diff   = A ^ B;      // XOR
    assign Borrow = (~A) & B;  // A' . B
endmodule

```
<br><br>
### Testbench Program<br>
```
module tb3;
    reg A, B;
    wire Sum, Carry;
    wire Diff, Borrow;
 
    // Instantiate the Half Adder
    half_adder ha_uut (
        .A(A),
        .B(B),
        .Sum(Sum),
        .Carry(Carry)
    );
 
    // Instantiate the Half Subtractor
    half_subtractor hs_uut (
        .A(A),
        .B(B),
        .Diff(Diff),
        .Borrow(Borrow)
    );
 
    initial begin
        // ---- VCD dump setup ----
        $dumpfile("half_add_sub.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb3);                // dump all signals in this testbench hierarchy
 
        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t A=%b B=%b | Sum=%b Carry=%b | Diff=%b Borrow=%b",
                   $time, A, B, Sum, Carry, Diff, Borrow);
        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;
 
        #10 $finish;
    end
endmodule

```
<br><br>

### Truth Table<br>
<img width="645" height="87" alt="TT3" src="https://github.com/user-attachments/assets/37e33bb3-d647-45d5-b610-c255d7e41b8b" /><br><br>

### Simulation Procedure

STEP 1 – Open Terminal<br>
Open a terminal in the experiment folder.<br>

STEP 2 – Load Synopsys Environment<br>
source /synopsys/start.sh<br>

STEP 3 – Compile Using VCS<br>
vcs half_add_sub.v half_add_sub_tb.v -full64<br>
If compilation is successful, VCS generates the simulation executable:<br>
simv<br>

STEP 4 – Run Simulation<br>
./simv<br>
The terminal displays the input combinations and corresponding outputs Sum, Carry, Diff, and Borrow.<br>
A VCD waveform file is also generated:<br>
half_add_sub.vcd<br>

STEP 5 – Open DVE<br>
dve -full64<br>
Other option<br>
dve -full64 &<br>
A DVE environment will open.<br>

DVE Waveform Verification<br>
In DVE:<br>
•	Open the testbench hierarchy.<br>
•	Locate the signals:<br>
o	A<br>
o	B<br>
o	Sum<br>
o	Carry<br>
o	Diff<br>
o	Borrow<br>
•	Add the signals to the waveform window.<br>
•	Run/inspect the waveform.<br>

•	Verify that Sum = 1 whenever A and B are different (A⊕B), and Carry = 1 only when A=1 AND B=1.<br>

•	Verify that Diff = 1 whenever A and B are different (same XOR pattern as Sum), and Borrow = 1 only when A=0 AND B=1.<br>

•	Confirm that Carry and Borrow never both go high for the same input pair, since they represent different (AND vs A'B) conditions.<br>

The waveform should agree with the truth table.<br><br>

### Expected Result

The Half Adder and Half Subtractor were realized using Verilog HDL:<br>

•	Sum = A⊕B, Carry = A.B<br>
•	Diff = A⊕B, Borrow = A'.B<br>

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table.<br><br>

### Output<br>
<img width="1847" height="1017" alt="DE 3d" src="https://github.com/user-attachments/assets/fca79387-43e4-43e8-8230-1ab01c63d7a7" />
<br><br>


### Viva-Voce Questions

•	What is a Half Adder, and what are its limitations compared to a Full Adder?

•	What is a Half Subtractor, and what does the Borrow output signify?

•	Why is the Sum/Difference expression identical (A⊕B) for both circuits, while Carry and Borrow differ?

•	What gate realizes the XOR function, and why is it central to both circuits?

•	What is the purpose of a Verilog testbench?

•	Why is a VCD file generated, and what does $dumpvars(0, tb) do?

•	What is the purpose of ./simv?

•	What is the difference between simulation and synthesis?

•	How would you extend this design to a Full Adder/Full Subtractor?<br><br>

### Result

Thus, the Half Adder and Half Subtractor were designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.





