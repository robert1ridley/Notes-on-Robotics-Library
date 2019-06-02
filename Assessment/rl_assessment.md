# Robotics Library

## Robotics Library 的简介

Robotics Library是一个面向对象的机器人工程学解决方案，本框架是用C++写的。代码在Github上，在这个链接可以看到：https://github.com/roboticslibrary/rl ，目前版本为0.7。
它的范围包括数学、运动学和动力学、硬件抽象、运动规划、碰撞检测和可视化。网上也有关于本框架设计的论文：https://www.roboticslibrary.org/Rickert2017a.pdf 。

## 体系结构

图1.1（本代码库的基本结构：
![Architecture Overview](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/overview-only.png?raw=true "Overview")

作者强调了四个关于本框架的体系结构的重点：
1. 一个pure library提供一致的API，所有的类都从某些已定义过的基本类继承。本框架不是一个中间件，跟其他机器人工程学框架不一样。
2. 一致和完整的实施：所有在机器人工程学领域内重要的算法都能用，比如运动学、动力学、轨迹生成、路径图计划等，且都有一致的标注和接口。
3. 代码库的复用性：本代码库提供一些包装器，以便用户可以使用其他代码库，比如可视化、碰撞检测等代码库。
4. 平台独立：本框架的C++实施能在不同的平台上编译起来。

### 自己对Robotics Library体系结构的分析：

我感觉Robotics Library 使用层次的体系结构（Layered Architecture)。
- 在最底层有一个数学库，该库包括一些高性能的矩阵和向量操作，这些操作都在上一层的算法（比如运动学、动力学、路径图计划等算法）广泛使用。

图1.2（math里的Matrix.h文件）:
![Matrix](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/matrix.png?raw=true "Matrix")

图1.3（mdl里的Kinematic.h文件）:
![Kinematic](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/kinematic.png?raw=true "Kinematic")

- 图1.2是本代码库最底层的Matrix实施，它利用一个开源的线性代数代码库叫Eigen，图1.3是math上一层的一个文件叫Kinematic，在这个文件里有一些算Jacobian的函数，这些函数利用下一层提供的Matrix 接口。
- 我觉得体系结构不是严格的层次结构，因为某层提供的接口可能被该层以上不同的层利用，比如路径图计划层在于Kinematics的上一层，但是它还利用一些math层提供的接口，因此我感觉本框架也有一些component-based 体系结构的特点（即每个component容易复用，且没有严格的层次约束，看图1.4）。

图1.4（Layered和Component-based体系结构）：
![Layered Components](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/layered-component.png?raw=true "LayeredComp")


### Robotics Library 利用的设计模式：

Robotics Library是用C++写的，在代码里，一个常见的设计模式是Factory模式：
- 在'sg'目录里有一个文件叫`XmlFactory.cpp`，它有一个函数叫'load'，但是因为利用Factory设计模式，这个函数更有灵活性（图1.5）。

![Factory Approach](https://raw.githubusercontent.com/robert1ridley/Notes-on-Robotics-Library/master/resources/factory.png?raw=true "Factory")

- 图1.5里的`XmlFactory::load`函数有两个实施方法，这是Factory设计模式的一个特点，第一个函数只接受两个参数`filename`和`scene`，如果用户只提供这两个参数，函数就直接load XML文件。不过`XmlFactory::load`函数的第二个实施方法还接受`doBoundingBoxPoints`和`doPoints`两个参数，要是用户提供这两个参数，该实施方法将执行。
