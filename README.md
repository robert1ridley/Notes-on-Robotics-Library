# Notes-on-Robotics-Library

These notes are based on the code in this repository https://github.com/roboticslibrary/rl.

## General Notes on Architecture

![Alt text](resources/overview?raw=true "Title")

Library reuse: Well-designed libraries from related fields, such as collision detection or visualization, are made available through wrappers. Especially in collision detection, several high-quality libraries already exist with different compromises in performance, precision, and advanced func- tionality (such as distance queries or raycasts). RL provides access to them under a common scene graph data structure and encapsulates their functions in an abstraction layer (Section II-E).
