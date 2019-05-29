# Notes-on-Robotics-Library

These notes are based on the code in this repository https://github.com/roboticslibrary/rl.

## General Notes on Architecture

![Architecture Overview](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/overview.png?raw=true "Title")

Library reuse: Well-designed libraries from related fields, such as collision detection or visualization, are made available through wrappers. Especially in collision detection, several high-quality libraries already exist with different compromises in performance, precision, and advanced functionality (such as distance queries or raycasts). RL provides access to them under a common scene graph data structure and encapsulates their functions in an abstraction layer (Section II-E).

### Design Principles

1. Pure Library with Single API: Consistent interfaces across application; all classes inherit from defined base classes. Not designed as middleware.
2. Consistent and Complete implementation: hardware drivers and motion-planning algorithms are unified in class hierarchy
3. Library reuse: encapsulated layer for reuse of existing robotics libraries

### Mathematical Functions

In order to have a clear separation of concerns, we implement generic geometric functions that are independent from a robot’s kinematic or dynamic model in the mathematics component, which is kept free from any software dependencies.

![Math Functions](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/math_functions_class_hierarchy.png?raw=True "Functions")	

### Hardware Abstraction Layer

Hardware devices lend themselves well for an object-oriented, hierarchical implementation. While devices of similar types, such as actuators, force-torque sensors, grippers, or cameras, share a common set of basic features, individual devices may provide additional features specific to a certain manufacturer. These common interfaces are organized as a class hierarchy in an object-oriented hardware abstraction layer as shown below.

![Hardware Abstraction Layer](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/hardware_abstraction_classes.png?raw=True "Hardware")

