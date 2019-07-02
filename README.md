# Accelerated_Cpp
This repo contains the mind flow and exercises of the book Accelerated C ++
## Chapter 0
使用最经典的HelloWorld来介绍C++的语法
```
// a small C++ program
#include <iostream>
int main()
{
 std::cout << "Hello, world!" << std::endl;
 return 0;
}
```

### 0.1 注释
C++ 中用`\\`来表示注释的内容，这个符号一直作用到行末，注释不会被编译，是给人看的。

### 0.2 `#include`
C++ 中可以使用两种库(library)，一种是标准库(standard library)，这种库已经随C++安装好，引用的话用尖括号`#include <iostream>`，另一种是用户自定义的库，需要用`#include "libraryFile.h"`。

* `iostream`是标准输入输出库，可以支持连续的输入输出，而不支持随机或者带有用户界面的输入输出。

### 0.3 主函数main
函数`function`是带有名字的能执行一定功能的一组代码。 每个C++程序必须包含一个名字为`main`的函数。在我们运行编译好的C++程序时，程序会从`main`函数开始运行。 

`main`函数会被要求返回一个整数值`int`来表明运行的结果是否成功。 如果返回`0`则表示运行成功。

### 0.4 花括号`{}`
被包含在花括号内部的内容被看作一个整体单位(unit)，也就是说花括号是用来界定内容的组织与归属的， 比如`main(){}`中花括号的内容属于`main`函数。

### 0.5 使用标准库来输出
`std::cout << "Hello, world!" << std::endl;`使用了标准库的输出运算符(operator)`<<`，`"Hello, world"` 和 `std::endl`依次被输出运算符赋给了`std::out`。

`std::cout`会将被赋予的值输出到屏幕窗口中。 `std`被称为**命名空间**，命名空间是一系列名字/函数的集合，`cout`就是这个命名空间中的一个函数/名字，`endl`的作用是结束当前行并换行。

### 0.6 返回值

`return`会在程序结束时将其后面的值返回到调用这个函数的程序，返回的值要与最初定义的返回值类型一致， 也就是说`int main()`声明了返回值为`int`整型，因此`return`的值也应为整数。

### 0.7 深入理解
这个最基本的程序也揭示了C++常用的两个基本概念：**表达式(expression)**与**作用范围/观测范围(scope)**。

表达式是用来计算某些东西并输出计算结果，有些表达式除了结果以外也会产生额外效应。 简单来讲，有些表达式是用来计算的，有些表达式不是用来计算的【哈哈哈哈说的跟废话一样。 举个栗子，表达式`3+4`产生结果为`7`，表达式`std::cout << "Hello, world!"`将字符串`Hello World`输出到`std::cout`，这一步是结果，产生的额外效应是字符串被输出到了窗口并开始下一行。

表达式包括**运算符(operators)**和**算子(operand)**，运算符是被算子处理/干的。 每个算子都有其自己的**类型**, 整数的类型为`int`， `std::cout`的类型为`std::ostream`。

`std::endl`也被称为manipulator，起调整控制的作用，它不传递字符，而是结束当前行并开始新的一行。

**作用范围scope**有好多种，这个程序用了两种，一种是**命名空间**，如果要使用命名空间里的函数/名字，必须先声明这个命名空间，举个栗子`std::cout`先声明了命名空间为std，然后说了要用的名字/功能为cout。 命名空间规定了名字的所属。`::`也是个运算符哟。

**花括号**是另外一种作用范围，它界定了main程序的作用范围。

### 总结

* 看前面几节的内容，已经够精简易懂了。
* 表达式以`;`结尾。
* main函数可以不声明返回值，即无`return`，则默认返回0。
* 函数体必须用花括号抱起来。

## Chapter 1 字符串

这一章会涉及变量的声明，初始化以及输入和字符串库的应用。

### 1.1 输入

下面的程序会从窗口读取输入的名字并在窗口打出问候语:

```
// ask for a person's name, and greet the person
#include <iostream>
#include <string>
int main()
{
 // ask for the person's name
 std::cout << "Please enter your first name: ";
 // read the name
 std::string name; // define name
 std::cin >> name; // read into
 // write a greeting
 std::cout << "Hello, " << name << "!" << std::endl;
 return 0;
}

```
为了读取输入，计算机得有个地方储存这个输入，这个储存的地放叫做**变量**。 变量是有名字的**对象**，要知道，**对象**与**变量**是不同的，有的对象是没有名字的。

定义变量的时候需要同时指明这个变量的类型。 在栗子中，`std::string name;`,局部变量`name`的类型为`std::string`，这个类型在标准库中已经被定义好了，我们只要将这个标准库导入就行，即`#include <string>`。 由于`name`是在函数内部声明的，所以它是局部变量，在程序运行到函数结尾的时候，这个变量会被摧毁。

在定义变量的同时也可以对变量进行初始化，就是说在定义的时候就给这个变量一个初始值。 如果这个变量是个字符串`String`，在不初始化的情况下这个字符串变量会是个空字符串`empty/null string`，不包含任何字符。

`std::cin >> name`将从窗口读取的字符串储存到变量`name`中。 `std::cin`的作用是从窗口读取非空格字符串：从第一个非空格字符起，直到遇到空格字符为止。
