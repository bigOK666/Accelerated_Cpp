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
## Chapter 1
