# Sign-off Timing Analysis 5-day workshop using OpenTimer

About the workshop: 
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface. This process does not verify logic of a design and works only for synchronous clock types.

The workshop covers all the basic concepts in STA and Timing constraints. It starts with basics of Static Timing Analysis, timing paths, startpoint, endpoint and combinational logic definitions. It explains setup and hold checks, how STA tools calculate setup and hold violations. 

It also covers design rule checks, time borrowing on latches, timing arcs, cell delays and models, impact of clock network on STA


# OpenTimer 
Starting with setting up the lab space. 

![image](https://user-images.githubusercontent.com/92804006/152235842-b67905a1-0f80-4d10-a8aa-9bc5ffea3cff.png)

# Why OpenTimer?
OpenTimer is a new static timing analysis (STA) tool to help IC designers quickly verify the circuit timing. It is developed completely from the ground up using C++17 to efficiently support parallel and incremental timing. It is a high-Performance Timing Analysis Tool for VLSI Systems that supports Industry standard format (.lib, .v, .spef, .sdc), Graph- and path-based timing analysis and Parallel incremental timing for fast timing closure


# Design rule checks : 

1. Slew/Transition Analysis: 
 a. Time take to reach from 30% Vdd to 70% Vdd is the rise slew time. 

 b. Time take to reach from 70% Vdd to 30% Vdd is the fall slew time.

2. Load analysis: It depends on the minimum and maximum capacitance and the fanout load.

3. Clock Skew analysis : It is the difference in the dealy of clock. There are 2 types - Positive and negative skew.

4. Pulse Width Checks : It checks if the signal has undergone width loss as compared to the original (Master) clock.


# Types of designs
1. Combinational Design : These just use gates to build the circuit, there is no use of any kind of memory.

2. Flop based designs : These are sequential circuits and make use of both logic gates and flops. 
 
 a. Edge triggered : These kind of flops get triggered by rising or falling edges of the clocks.
 
 b. Level triggered : These kind of flops get triggered by the high level of the clock. 
 
 
 # Time borrowing 

All latch based designs are level triggered. In level triggered, if data gets delayed in one half clock cycle, it still gets captured and it borrows some time from the next cycle (if the delay in this cycle is less or no delay). This hence, has the flexibility for no less data loss.
 
 
 # Defining different possible paths for the diagram.

![image](https://user-images.githubusercontent.com/92804006/152668504-9b871923-5c9f-49de-a358-a92bcae030ec.png)

# Path Specifications

To define a specific path from the circuit diagram we use 3 commands : 

1. -from : This is generally used for defining the start poimts.

2. -to : This is generally used for defining the end poimts.

3. -through  : This is generally used for defining the intermediate nodes.

![pathspecs](https://user-images.githubusercontent.com/92804006/152485145-6da5c0d3-972f-49e9-b082-d9f83c0bbf1b.jpg)


For example consider the path in above image - The solution will be : 

-from -> F1/Ck

-to -> F5/D

-through -> {U1/A} {U1/Z}


# Cross Talk and Glitches

1. Cross talk is the noise caused by coupling of switching activity of the victim with switching activity of the aggressors. This is a timing failure in the circuit.

![image](https://user-images.githubusercontent.com/92804006/152668507-905ed944-9014-42e0-b71f-615f1db8bcd3.png)

2. Glitches can happen due to the charge transfered by switching. This is a function failure. 

![image](https://user-images.githubusercontent.com/92804006/152668510-5481e734-eae4-44aa-ba42-e10e5056b4eb.png)


# Clock gating checks 

There are 2 main things: 

![clkgating](https://user-images.githubusercontent.com/92804006/152483215-f34fe1ec-6735-4f68-8017-2613009d2311.jpg)

1. A signal must control the path of clock.

2.  The clock and enable should be inputs to a gate.


# Clock Groups 

There are 4 types of clock groups -  Synchronous, Asynchronous, Physically exclusive, Logically exclusive clocks.

STA can work only for synchronous kinds of clocks. This means both clocks clk1 and clk2 should sync - same phase and time.

If one wants to change the type of clock, say to asynchronous, use command : set_clock_groups_asynchronous group{clk1 clk2 clk3} group{clk4 clk5 clk6}. 
Make note, here, that all 6 clks are not relaated to each other individually but the asynchrosity is applicable between the 2 groups.

Let's look at some clock properties. 

![clkprop](https://user-images.githubusercontent.com/92804006/152482002-39fcd154-5082-4b4a-b4a9-7fb22ee29687.jpg)


# Setup check

STA finds the most restrictive setup by expanding the clock into a common base  period and finding the most restrictive launch and capture. 

If the peroid of one clock cycle is Tperiod, setup time Tsetup, delay due to combinational logic Tcomb, clock skew Tskew, setup uncertainty Su due to jitter in clock

The equation for setup check : Tcomb + Tsetup <= Tperiod + Tskew - Su

![setupcheck](https://user-images.githubusercontent.com/92804006/152234297-ba6d51ec-c1dc-42fa-85b8-6e336f23701f.jpg)


# ECO – Engineering Change Order

• In the ECO cycle, we perform various analysis one by one for every check which we need to close but not closed till PnR stage.

• There are specialized signoff tools that help us to analyze the issue and also suggest the changes we need to do in order to close the issue.

• The suggested change is captured in an eco file.

• In this lab we will focus on ECO for timing purposes, this is done to fix setup and hold violations.


# Simple.v - Verilog File
Using command leafpad simple.v

![simplev](https://user-images.githubusercontent.com/92804006/152236901-a3743f38-36da-4b25-9698-22c3d5379af5.jpg)

![osu](https://user-images.githubusercontent.com/92804006/152232284-c55fafe5-7920-4e93-af48-1eba4279d185.jpg)

# Running and opening the Liberty file.

![run](https://user-images.githubusercontent.com/92804006/152232377-46d9c1c2-3404-4d4f-b0d9-1ebfb81e2e6f.jpg)

# Running command for Simple.lib 
1. Simple_Early :  leafpad simple_Early.lib

![simplelib](https://user-images.githubusercontent.com/92804006/152233574-d55a3df5-dd9e-448a-9be8-3fd6e8fd4848.jpg)

2. Simple_Late : leafpad simple_Late.lib

![image](https://user-images.githubusercontent.com/92804006/152237556-59069cdd-d80a-4694-8f13-394b14267c11.png)


# Opening the Out.txt file

# Using the commands :  
1. ot-shell -i run.tcl -o out.txt  to add files and
2.  opening the file using the command leafpad out.txt

For each run.tcl file, we have out out.txt report that shows slack and hence timing violated.

# Day 3 :

![outtxtlab3_op](https://user-images.githubusercontent.com/92804006/152234107-8fb98200-c9b1-4a4c-b074-fe0a95e91872.jpg)


![outtxtlab3_command](https://user-images.githubusercontent.com/92804006/152234079-bd49ebbc-2838-4992-87a2-d7be8bda26dc.jpg)

# Day 4 : 

![runtcllab4](https://user-images.githubusercontent.com/92804006/152487968-6b69f3a3-127a-4df3-98f0-0c52728529d3.jpg)


![slack_outtxtlab4](https://user-images.githubusercontent.com/92804006/152488111-95534819-eb54-4227-bd4f-124c96387350.jpg)



![cppr_cancelation](https://user-images.githubusercontent.com/92804006/152490232-07b743d9-a360-4db0-bb29-bb242690d6cb.jpg)



![runtcllab5](https://user-images.githubusercontent.com/92804006/152488142-4549665a-0627-438e-9cf6-e780cedcc4f7.jpg)



![outtxtlab5](https://user-images.githubusercontent.com/92804006/152488167-9e4709da-64db-42c5-99d1-61dcb22370ae.jpg)


# Day 5: 

![runlab6](https://user-images.githubusercontent.com/92804006/152488188-87b646af-140a-4705-8c49-80f27b1c0163.jpg)


![runlab7](https://user-images.githubusercontent.com/92804006/152488307-11ecc586-1552-4a59-a196-67f4920e7e0a.jpg)


 Some extra commands at our disposal from the above run file : 


![funcom](https://user-images.githubusercontent.com/92804006/152488409-14c98797-b411-4187-91ba-7a6d78067e01.jpg)


![outlab7](https://user-images.githubusercontent.com/92804006/152488320-22e06df1-cb32-43a6-b8c4-194af1d25d32.jpg)


# Acknowledgements 

Kunal Ghosh, Co-Founder (VSD Corp. Pvt. Ltd)

Vikas Sachdeva - Vlsideepdive
