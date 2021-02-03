# 2-pass Assembler

## Details

- This project is the implementation of a **two-pass assembler**. 
- A basic two pass assembler involves the conversion of a given assembly code to its corresponding machine code. 
- This is a 12 - bit assembler, hence the output machine code will have 12 bits.

## Key Features:

● This assembler handles labels and their referencing in the provided assembly
code.
● It also allocates virtual addresses to the provided labels and variables/symbols
used in the assembly code.
1.2) Machine Requirements:
● 12 bit accumulator architecture.
● Should have at least 2^8 bit memory.

## Workflow:
● **First Pass**:
a) We initiate a variable named location counter to traverse throughout the
raw assembly code line by line. It increments its value by one after each
iteration.
b) We scan the lines from a text file using a buffered reader, and read the
next line in each provided iteration.
c) Firstly, we look out for the type of instruction and the number of
parameters passed with it. We also throw required errors in just the first
scanning of the question.
d) Then, we look out for labels in the given instruction. We have defined a
particular format of labels(mentioned later in this documentation).
e) We seperate the label and store it in the label table if it does not have an
error.
f) Next, we check for the opcode in the line. If it is a valid opcode, the
argument passed with the opcode is stored in the symbol table.
Necessary errors are thrown if present.
g) When the label is used in the branch statement, it is stored in the label
table with the value of -1. If it is defined in the code anywhere, then the
value of the label in the label table is replaced with the value of the
location counter of the line where the definition occurs.
Similarly, the symbols are stored in the symbol table with the value of -2. If
it is defined later in the code ( assumption : a symbol is considered defined
when it is used with INP opcode later anywhere in the input file ), then the
value of the symbol in the symbol table is updated with the value of the
location counter where the definition occurs.
h) If after pass 1, any symbol in the symbol table or any label in the label
table has a value of -1 or -2 respectively stored against it, an error is
thrown that the symbol or label is used but not defined.
i) If any error is reported, the compiling is stopped and the user is asked to
remove the error and try again
j) Hence, output file is created only if there are no errors in pass 1.
k) If there is no error in the code, another table is made for designing an input
to pass 2.

● **Second Pass**:
a) This pass is the final step of the process, in which the conversion of the
assembly code to machine code takes place.
b) The table which has the input for pass 2 is read line by line and machine
code generated.
c) The label calls are replaced by the value of location counter at label
definitions and variables are replaced by their storage addresses (which is
the value of the location counter at the INP statement for the given
symbol), both provided by the location counter during the first pass.
