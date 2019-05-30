# Robotics Library

## Robotics Library 的简介

Robotics Library是一个面向对象的机器人工程学解决方案，本框架是用C++写的。代码在Github上，在这个链接可以看到：https://github.com/roboticslibrary/rl ，目前版本为0.7。
它的范围包括数学、运动学和动力学、硬件抽象、运动规划、碰撞检测和可视化。网上也有关于本项目设计的论文：https://www.roboticslibrary.org/Rickert2017a.pdf 。

## 体系结构

本代码库的基本结构：

![Architecture Overview](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/overview-only.png?raw=true "Overview")

作者强调了四个关于本框架的体系结构的重点：
1. 一个pure library提供一致的API，所有的类都从某些已定义过的基本类继承。本框架不是一个中间件，跟其他机器人工程学框架不一样。
2. 一致和完整的实施：所有在机器人工程学领域内重要的算法都能用，比如运动学、动力学、轨迹生成、路径图计划等，且都有一致的标注和接口。
3. 代码库的复用性：本代码库提供一些包装器，以便用户可以使用其他代码库，比如可视化、碰撞检测等代码库。
4. 平台独立：本框架的C++实施能在不同的平台上编译起来。

### 自己对Robotics Library体系结构的分析：

* Robotics Library 使用层次的结构（Layered Architecture)：
- 在最底层有一个数学库，该库包括一些高性能的矩阵和向量操作，这些操作都在上一层的算法（比如运动学、动力学、路径图计划等算法）广泛使用。

图1.1:

![Matrix](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/matrix.png?raw=true "Matrix")


