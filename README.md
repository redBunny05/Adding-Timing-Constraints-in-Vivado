# Adding-Timing-Constraints-in-Vivado
In this repository I am trying to perform STA( Static Timing Analysis ) using Vivado's Timing Constraint wizard and TCL terminal. In this exercise we will try to analyze some design metrices like timing summary, slack histogram, clock interactions and generate them as well
Timing is what is today's epicentre of high performance devices having faster computation power. Whether the complexity of the structure is simple or sophisticated, it is properly timed. 
In this small exercise we will design a 3-bit asynchronus up counter, simulate it with the help of testbench, constraint the design using Constraints wizard and TCL window. Also we will try to observe value of slack when we introduce certain delays to meet hold and setup requirements. And lastly check for any clocking violations using DRC.


# THE PROJECT
Before moving towards our problem statement let's revisit some topics and revise there logic and definition.
1. Counter - A counter is a sequential circuit which counts the value according to its design. It can be operated synchronously/asynchronously i.e. on one the active edges or on both edges respectively. Clock, reset, enable and data are input pins whereas one output pin.
2. Testbench - It is a verilog/VHDL code used to provide stimulus to the DUT(Device Under Test) and observe the output.
3. STA - Static timing analysis is a method of validating timing performance of the design by checking all the possible paths which can violate timing.
4. Propagation Delay - The flip-flop requires certain amount of time to respond to the input data. THis reasponse is in the form of delay. Propagatiion is the forms of TpLH (propagation delay Low-high) and TpHL (progation delay High-low).
5. Setup time - minimum amount of time by which the data must be stable i.e. it shouldn't transit before the active edge of the clock arrives.
6. Hold time - minimum anount of time by which the data must be stable after the arrival of active edge of the clock.
7. Slack - It is a real quantity and measured as the difference between data required time and data arrival time. Positive slack means there are no setup and hold violations i.e the correct data is caputred (appropriate setup time) and correct data is latched (appropriate hold time).

We will frequently use this concepts for better understanding and how these terms are implied in the practical design. 
Moving on let's design a 3-bit async counter
Being a 3-bit up-counter it will count values from 0-7. Verilog file has been attached in this project along with the scripts to create the project, add code and testbenches. 
In the simulation we can observe the response w.r.t the test vector provided to the DUT. One can change the clock period or rst period to infer changes in the output. 
After the simulation we have to synthesize the design so that the HDL code will be synthesized into gate-level representation. The gate level schematic can be viewed in the synthesis tab. At this stage if we try to implement the design and try to generate bitstreams error would be generated as we haven't constrained our design. 
For this problem statement our primary focus is on how to constraint time in our design. So let's have a step-by-step approach towards the same.

## Constraining Time ##
