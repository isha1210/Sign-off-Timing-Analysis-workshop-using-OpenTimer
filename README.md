# Sign-off-Timing-Analysis-workshop-using-OpenTimer

About the workshop: 
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface.

The workshop covers all the basic concepts in STA and Timing constraints. It starts with basics of Static Timing Analysis, timing paths, startpoint, endpoint and combinational logic definitions. It explains setup and hold checks, how STA tools calculate setup and hold violations. 

It also covers design rule checks, time borrowing on latches, timing arcs, cell delays and models, impact of clock network on STA

# Contents


# OpenTimer 
Starting with setting up the lab space. 

![image](https://user-images.githubusercontent.com/92804006/152235842-b67905a1-0f80-4d10-a8aa-9bc5ffea3cff.png)

# Why OpenTimer?
OpenTimer is a new static timing analysis (STA) tool to help IC designers quickly verify the circuit timing. It is developed completely from the ground up using C++17 to efficiently support parallel and incremental timing. It is a high-Performance Timing Analysis Tool for VLSI Systems that supports Industry standard format (.lib, .v, .spef, .sdc), Graph- and path-based timing analysis and Parallel incremental timing for fast timing closure

# Simple.v - Verilog File

![simplev](https://user-images.githubusercontent.com/92804006/152232200-e2bbff2f-839b-4e61-8657-620bdd83c8f2.jpg)

![osu](https://user-images.githubusercontent.com/92804006/152232284-c55fafe5-7920-4e93-af48-1eba4279d185.jpg)


![run](https://user-images.githubusercontent.com/92804006/152232377-46d9c1c2-3404-4d4f-b0d9-1ebfb81e2e6f.jpg)

# Running command for Simple.lib
![simplelib](https://user-images.githubusercontent.com/92804006/152233574-d55a3df5-dd9e-448a-9be8-3fd6e8fd4848.jpg)

#
![stareport](https://user-images.githubusercontent.com/92804006/152233653-4d3e6fac-3920-4bf6-ab62-d90fc5ca02ad.jpg)

# Setup check

![setupcheck](https://user-images.githubusercontent.com/92804006/152234297-ba6d51ec-c1dc-42fa-85b8-6e336f23701f.jpg)

# Opening the Out.txt file
![outtxtlab3_op](https://user-images.githubusercontent.com/92804006/152234107-8fb98200-c9b1-4a4c-b074-fe0a95e91872.jpg)

![outtxtlab3_command](https://user-images.githubusercontent.com/92804006/152234079-bd49ebbc-2838-4992-87a2-d7be8bda26dc.jpg)

# Defining different possible paths for the diagram.
![paths](https://user-images.githubusercontent.com/92804006/152234220-cf5276d1-937a-432a-bf66-4fe181a78a2d.jpg)
