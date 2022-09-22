# Project Checkpoint 1
 - Author: Zilin Xu
 - Date: 09/16/2022
 - Course: ECE 550DK, Dukekunshan University
 - Term: Fall 2022
 - Professor: Xin li

## Duke Community Standard, Affirmation
 I affirm that each submission complies with the Duke Community Standard and the guidelines set forth for this assignment.  

Project Description
This is an ALU designed by Verilog. It includes operation for 32-bit addition, substraction, 32-bit barrel shifter with SLL and SRA, bitwise OR and bitwise AND. Also it can be able to detect the overflow in addition and substraction. Besides, it can judge two 32-bits inputs' relationship: equal or less than.  The inputs are data_operandA, data_operandB, ctrl_ALUopcode, ctrl_shiftamt. The outputs are data_result, isNotEqual, isLessThan, overflow.  Please take time to see my attached imagine files.


Bug Description and my idea
However, my project has an unexpected bug that I cannot sucessfully debug by myself. The error says "Error (12014): Net "data_operandA[31]", which fans out to "rightshift1:SRA0|a[31]", cannot be assigned more than one value" and shows as the diagram named "error". After Google it and many time's simulation,  I think this error mainly says that I assign a same variable for several times. Due to lack of knowledge and Wednesday and Thursday evening has no office hour to discuss with TA, I cannot finally work through with this bug. Since I did everything right with vriable names and those waveforms detection in the beginning of project. However I figure out another way to run the given testbench and I will show my work and testbench result as diagram. I hope the grader can have more consideration with grading my work. Since I put tons of effort at both CISK and classroom to finish it. It was really hard for me with only Computer Science background to understand Verilog and hardware.

My method to deal with the bug
Since the error shows I assign a value for same variable several times, I separatedly them by leaving the part I want to run testbench. For add and substraction, i comment other lines of code for other operations. And the code's diagram named "add_substract_code". The test bench result didn't shows the error of add and substraction. Which means my these two operation are right.It is normal that when I am doing the test bench for certain part, others will shows error. And for the rest part I used the same way. I  test bitwise Or and bitwise And together with their imagine files. The leftshift and rightshift are also together. I also attached their waveforms result.  If the grader want to use testbench to run my alu.v, you can comment other part to get the result of certain part.  I will really appreciate if you take time to see my attached files and score my work with consideration.
Module add
I apply the CSA structure according to lecture slides. For a 32-bit adder I use three 16-bit adder and a mux to compute it.  For the 16-bit adder I used two 8-bit adder and four 2-bit adder to get an 8-bit adder. For this adder it can also compute the overflow in addition. 

Module substract
According to lecture, we can compute the result of adding one input and another input's 2's complement to get the substraction result. I apply another module called flip to get 2's complement. Then use the add module to add them together. 

Module and
I applied and_gate to each bit of input. To get the result.

Module or
I applied or_gate to each bit of input.  To get the result.

Module leftshift
As the lecture slides said, I apply Mux with five stages since we can most shift 32 bits which is 5-bit input for binary. The first column mux will simply connect two adjacent input bits and generate corresponding w1 values. The second column will have two w1 wires as input and they should have two bits distance. The thid column will have last operation's inputs (i.e. w2) with a distance of 4 bits. The forth column and fifth column have similar operations as before. The output should be w5 which are the last output from fifth column mux.  Notice that, since this is left shift, we will have 0 in the right-most bits generated by left shift. So for last part of each column mux, we will have some bits connect with "0". For each column the number of bits connecting "0" are different.

Module rightshift1
Similar with leftshift operation before. But different and important thing is, when we right shift an input, the first bit will stays same as the original first bit.  So I have a variable w6 to store the first bit and for each column there should be left most bits to connect with w6. So that the output 's left most bits will have same value as the original first bit depends on the number of bits we want to right shift. Also notice that, the order of wires that input mux should be opposite as we did in left shift. The rest stuff will be similar. 

Module isLessThan
I first substact two input. Then check the first bit with and_gate and output the result. If isLessThan has 0 as output, it means a is greater or equal than b. In order to deal with cornor case,  I use a xor gate the compute the final result with overflow from substaction and the result we get before. (i.e. w2).

Module isNotEqual
For two inputs a and b, I firstly get result of a-b and b-a. Then apply islessthan to these two outputs. If both output from isLessThan are 0, which means they are same. 

Module Overflow
Overflow is determined after addition and substraction and it is also inside these two modules. If the carry-in of the last bit is not equal with the carry_out of last bitduring the addition or substraction, we set overflow to 1.





