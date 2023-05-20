# Layout optimization



In the manufacturing field material handling is a necessary but costly activity. Increased material handling will create extra costs due to labor, machine and time requirements while possibly causing quality defects and increasing shop floor lead time. That is why often in practice the shop floor layouts are redesigned to minimize material handling related costs. Though making layout changes on the shop floor and moving machines also have associated costs. These costs are incurred since the production needs to be paused and labor hours are required to make the necessary changes to the layout.

This real life layout redesign decision can be modeled and solved as an optimization problem. The objective would be to minimize all costs including cost of making layout changes and cost of material handling.

The problem is defined here: https://miro.neos-server.org/app/facloc

The approach used here involves the use of a Constrained Quadratic Model (CQM) from Dwave (https://cloud.dwavesys.com/). The solution is computed using the LeapHybridCQMSampler 

A facility layout optimization model is presented, it consists of four machines: CNC, Mill, Drill, and Punch. These machines are the most common machines in any manufacturing facility.

There are also a set of three products with pre-specified routings as shown below:

- P1: Receiving -> CNC -> Drill -> Punch -> Shipping
- P2: Receiving -> Mill -> Drill -> Punch -> Shipping
- P3: Receiving -> CNC -> Drill -> Mill -> Punch -> Shipping

### Objective
The objective function is to minimize the total cost of material handling and cost of layout changes. The material handling cost is calculated using Euclidean distances between the locations of work centers and the routing that needs to be followed by each product family times the cost associated for a unit of movement. 
The cost of changes in the layout is calculated by summing the cost associated with moving each machine over the set of machines that are moved. ost of moving a machine is assumed to be \$300/distance and cost of material handling is \$100/distance.
Due to the fact that the objective function is composed of two conflicting parts, two weigh coeffecients must be set to prevent the calculation to be too sweked towards one. These value can, in their turn, be optimized by trial and error.

### Constraints

1. Minimum Distance Constraint: In a manufacturing setting due to quality reasons, specific work centers should not be adjacent to one another. Thus a minimum distance between two work centers can be specified by the user and used as a constraint in redesigning the layout.
2. Location Constraint: Each work center has a constraint for its location and movement in the floor space which is defined by rectangular region.
Lower left corner each machine is assumed to be the co-ordinates of the machine.

### User Inputs
Initial co-ordinates of each machine and receiving and shipping points
Costs of moving machines per unit of distance
Costs of transporting products per unit of distance
Minimum distance between machines
Location constraint for a machine (based on the rectangular region)

### Output
Total cost of moving 3 products and the machines with a visual representation

## References
Course ISYE 635 slides, Tools and Enviroments for Optimization, Spring 2013
