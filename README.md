# Notes-on-Robotics-Library

These notes are based on the code in this repository https://github.com/roboticslibrary/rl.

## General Notes on Architecture

![Architecture Overview](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/overview.png?raw=true "Title")

Library reuse: Well-designed libraries from related fields, such as collision detection or visualization, are made available through wrappers. Especially in collision detection, several high-quality libraries already exist with different compromises in performance, precision, and advanced functionality (such as distance queries or raycasts). RL provides access to them under a common scene graph data structure and encapsulates their functions in an abstraction layer (Section II-E).

### Mathematical Functions

In order to have a clear separation of concerns, we implement generic geometric functions that are independent from a robot’s kinematic or dynamic model in the mathematics component, which is kept free from any software dependencies.

![Math Functions](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/math_functions_class_hierarchy.png?raw=True "Functions")

