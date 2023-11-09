C++团队开发规范
=====

.. _介绍:

介绍
------------

本文档旨在为高质量C++团队编程提供指导，使他们能够采用良好的编程风格和经过验证的编程实践，从而获得安全、可靠、可测试和可维护的代码。C++旨在支持数据抽象、面向对象编程和通用编程，同时保持与传统C编程技术的兼容性。

参考文档
----------------

1. ANSI/IEEE Std 754, IEEE Standard for Binary Floating-Point Arithmetic, 1985. 

2. Bjarne Stroustrup. *The C++ Programming Language, 3**rd* *Edition*. Addison-Wesley, 

\2000. 

3. Bjarne Stroustrup. *Bjarne Stroustrup's C++ Glossary**.*

4. Bjarne Stroustrup. *Bjarne Stroustrup**'s C++ Style and Technique FAQ*. 

5. Barbara Liskov. *Data Abstraction and Hierarchy*, *SIGPLAN Notices*, 23, 5 (May, 1988). 

6. Scott Meyers. *Effective C++: 50 Specific Ways to Improve Your Programs and Design,* 

*2**nd* *Edition.* Addison-Wesley, 1998. 

7. Scott Meyers. *More Effective C++: 35 New Ways to Improve Your Programs and* 

*Designs.* Addison-Wesley, 1996. 

8. Motor Industry Software Reliability Association. *Guidelines for the Use of the C* 

*Language in Vehicle Based Software*, April 1998. 

9. ISO/IEC 10646-1, Information technology - Universal Multiple-Octet Coded Character 

Set (UCS) - Part 1: Architecture and Basic Multilingual Plane, 1993. 

10. ISO/IEC 14882:2003(E), *Programming Languages – C++*. American National Standards 

Institute, New York, New York 10036, 2003. 

11. ISO/IEC 9899: 1990, *Programming languages - C*, ISO, 1990. 

12. JSF Mission Systems Software Development Plan.

13. JSF System Safety Program Plan. DOC. No. 2YZA00045-0002. 

14. *Programming in C++ Rules and Recommendations*. 

Copyright © by Ellemtel Telecommunication Systems Laboratories 

Box 1505, 125 25 Alvsjo, Sweden 

Document: M 90 0118 Uen, Rev. C, 27 April 1992. 

Used with permission supplied via the following statement: 

*Permission is granted to any individual or institution to use, copy, modify and distribute* 

*this document, provided that this complete copyright and permission notice is maintained* 

*intact in all copies.* 

总体设计
----------------

**可靠性：**可执行代码应该以可预测的方式一致地满足所有要求。

**可移植性：**源代码应该是可移植的（即不依赖于编译器或链接器）。

**可维护性：**源代码应该以一致、可读、简单的方式编写，设计简单，易于调试。

**可测试性：**应编写源代码以促进可测试性。最小化以下内容，每个软件模块的特性将有助于实现更易于测试和维护的模块：

- 1.代码大小

- 2.复杂性

- 3.静态路径计数（通过一段代码的路径数）

**可重用性：**鼓励设计可重用组件。组件重用可以消除冗余的开发和测试活动（即降低成本）。

**可扩展性：**期望需求在产品的生命周期中不断发展。因此，一个系统应该以可扩展的方式进行开发（即可以管理需求中的扰动通过本地扩展而不是大规模修改）。

**可读性：**源代码应该以易于阅读、理解和理解的方式编写理解

请注意，遵循本文件中包含的指导方针并不能保证生产无错误、安全的产品。但是，遵守这些准则以及软件开发计划[12]中定义的过程，将帮助程序员产生干净的尽量减少常见错误和错误来源的设计。

耦合和内聚
~~~~~~~~~~~~~~

耦合和内聚是已分解为模块的系统的特性。内聚性是衡量同一模块中各部分配合程度的指标。耦合是系统中不同模块之间交互量的度量。因此，内聚力处理模块中的元素（元素在多大程度上适合作为模块的一部分模块），而耦合处理模块之间的关系（模块的紧密程度粘合在一起）。

面向对象的设计和实现通常支持所需的耦合和内聚特性。OO技术背后的设计原则导致了模块。模块之间干净的接口使模块能够松散耦合。此外，数据封装和数据保护机制提供了一种帮助执行耦合和内聚目标。

源代码应该作为一组模块来开发，尽可能松散地耦合。注意，泛型编程（需要使用模板）允许源代码

要使用松散耦合编写的代码，并且没有运行时开销。

紧密耦合软件的示例包括以下内容：

- 许多功能与硬件或其他外部软件源密切相关，以及

- 访问全局数据的许多功能。

有时，紧密耦合的软件是不可避免的，但它的使用应该是两者兼而有之，按照以下指南的建议进行最小化和本地化：

- 将硬件和外部软件接口限制为少量功能，

- 尽量减少全局数据的使用，以及

- 尽量减少实施细节的暴露。

代码大小和复杂性
~~~~~~~~~~~~~~

**规则1：**任何一个函数（或方法）将包含不超过200行。

理由：长功能往往很复杂，因此难以理解和测试。

注：第4.2.1节定义了详细规则以及允许偏离的规则。

**规则2**：不得有任何自修改代码。

理由：自修改代码容易出错，而且难以阅读、测试和维护。

**规则3**：所有函数的圈复杂度应小于等于20。

理由：限制功能复杂性。有关更多详细信息，请参见附录A中的AV规则3。

异常：包含带有许多case标签的switch语句的函数可能会超过此值限度

注：第4.2.1节定义了应和应规则以及允许偏离应该或应该的规则。

C++ 编码规范
------------

介绍
~~~~~~~~~~~~~~

以下规则和建议的目的是定义C++编程风格这将使程序员能够生成更多的代码：

- 正确，

- 可靠，以及

- 可维护。

为了实现这些目标，计划应：

- 风格一致，

- 可移植到其他架构，

- 没有常见类型的错误，以及

- 不同的程序员可以理解，因此可以维护。

