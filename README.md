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

这里用到的输入输出库一般会将输出值暂时存在**缓存buffer**中，只有需要的时候才会将缓存的内容**flush刷**到输出设备上。 有三种方式会触发缓存内容被刷到输出设备上：
* 缓存已满。 缓存满的时候会被自动刷到输出设备上
* 输入输出库被要求从输入设备读取内容，这种情况下它会先将缓存的内容刷出去，然后再读取
* 我们要求它刷出去

### 1.2 给名字相框

这一节主要是谈另一种创建变量的方式，字符串的拼接以及常量的定义。 先上程序：
```
// ask for a person's name, and generate a framed greeting
#include <iostream>
#include <string>
int main()
{
 std::cout << "Please enter your first name: ";
 std::string name;
 std::cin >> name;
 // build the message that we intend to write
 const std::string greeting = "Hello, " + name + "!";
 
 // build the second and fourth lines of the output
 const std::string spaces(greeting.size(), ' ');
 const std::string second = "* " + spaces + " *";
 
 // build the first and fifth lines of the output
 const std::string first(second.size(), '*');
 
 // write it all
 std::cout << std::endl;
 std::cout << first << std::endl;
 std::cout << second << std::endl;
 std::cout << "* " << greeting << " *" << std::endl;
 std::cout << second << std::endl;
 std::cout << first << std::endl;
 
 return 0;
}
```

首先在声明变量`greeting`的时候我们可以发现，在声明变量的同时可以初始化这个变量的值。 然后`+`这个运算符在应用于字符串类型的时候可以用来串接字符串，但**`+`不能串接两个字符**。 也就是说只要算子里面有字符串就可以串接。 字符char和字符串string的区别就是字符串是由很多个字符组成的，在声明字符的时候用单引号`''`, 在声明字符串的时候用双引号`""`。 如果运算符对于算子有不同的意义，我们称之为运算符**重载**。 例如`1+1`中`+`的意义就是加法。

还有一点要注意的是我们可以先声明一个常量而不需要知道这个常量里面是什么值，greeting在被声明初始化的时候并不能确定里面应该有什么值，因为`name`这个变量还不确定，直到运行程序并从外部获得`name`这个变量的值后，greeting的值才明确下来。 那么常量的意义是什么呢？ 常量的意义就在于定下这个常量之后就不能再更改它了，提供了极高的安全性。

变量可以通过赋值`=`创建，也可以通过`type variable(number, value)`的形式来**构建**。 栗子中`std::string spaces(greeting.size(), ' ');`就是这样的用法。 具体形式为`变量类型 定义的变量(重复的次数，重复的值)`， 通过这种形式spaces这个变量的值就是greeting这个字符串个数那么多的空格。

## Chapter 2 循环与计数


循环是个好东西，好在可以通过简单几行代码完成重复性的工作。

### 2.1 问题阐述

同样是上一章的任务，现在要通过循环语句来完成重复性的部分，即外边框的输出，同时也通过使用循环语句使程序变得更加灵活，添加边框的行数仅需改变表示边框数量变量的值就能实现。

### 2.2 整体结构

整体结构如下，从用户获取的部分还是要保留的，我们要重构的是边框的部分。

```
#include <iostream>
#include <string>
int main()
{
 // ask for the person's name
 std::cout << "Please enter your first name: ";
 // read the name
 std::string name;
 std::cin >> name;
 // build the message that we intend to write
 const std::string greeting = "Hello, " + name + "!";
 // we have to rewrite this part...
 
 return 0;
}
```
### 2.3 确定外框的行数

这一节来完成外边框的基础部分。
```
// the number of blanks surrounding the greeting 文字到边框的间距，最少为0行
const int pad = 1;
// total number of rows to write 有了边距就可以确定一共要打多少行了
const int rows = pad * 2 + 3;
```
```
// separate the output from the input
std::cout << std::endl;
// write rows rows of output
int r = 0;
// invariant: we have written r rows so far
while (r != rows) {
	// write a row of output (as we will describe in §2.4/22)
 std::cout << std::endl;
 ++r;
}
```
循环体的内部我们下一节来完成


#### 2.3.1 while循环语句

循环语句的基本逻辑为: 当循环条件为真时，就按顺序执行循环体内的语句，执行结束后返回条件判断，若为真则继续执行循环体内的语句，若条件为假则跳过循环体，执行循环之后的语句。
```
while (condition) 
 
statement
```
上一节用到的while语句所表达的意思就是如果r不等于rows, 就一直重复执行输出空行并让r增1。

#### 2.3.2 如何设计循环语句
设计循环语句前，为了保证每次运行循环的语句都能达到预想的目的，需要设置**loop invariant**，也就是循环常量。 对于设计while循环来说，需要注意两点：当while循环结束时，条件(condition)此时需为FALSE；每当while循环将要检验条件时，loop invariant都是TRUE。 在2.3节的while循环语句开头，我们就设计了loop invariant为“已经输出了r行”。 设计loop invariant的要点是要包含循环体内的某个变量，例如“r"。

### 2.4 把行打出来
程序的目的是将欢迎的文字用星号框起来，通过观察我们可以发现每行的列数是固定的，因此我们可以定义列数为
```
const std::string::size_type cols = greeting.size() + pad *2 +2;
```
size_type是std::string域下的类型名称，用来定义字符串中的字符数量，所有字符串中的字符数量都用这个数据类型。这个数据类型是无符号数据类型，简单来讲可以承载很大的数。

现在我们可以用循环来输出字符了：

```
std::string::size_type c = 0;
//invariant: we have written c characters so far in the current row
while(c != 0) {
	//write one or more characters
	//adjust the value of c to maintain the invariant
}
```
是的，上面的代码只写了要干啥，主要内容还没写，我们往下看。
#### 2.4.1 把框打出来
需要打星星的地方是固定的，仔细想一下只有四种情况需要打星星：第一行，最后一行，每行的开头（第一列），最后一列。 那么我们需要的打框的部分就出来了：
```
//invariant: we have written c characters so far in the current row
while(c!=cols){
	if(r==0 || r==rows - 1 || c==0 || c==cols - 1){
		std::cout << "*";
	} else{
		//write one or more characters
		//adjust the value of c to maintain the invariant
	}
}
```
这里引入了两个新知识点，一个是if条件语句，另外一个是逻辑运算符“或”||。 if 条件语句很直白，当条件为真时，执行对应的语句，如果为假，则执行else引导的语句，else 那部分可以省略。

```
if (condition)
	statement1
else 
	statement2
```
逻辑运算符包括与（&&），或（||），他们都是左序运算符，也就是说先从最左边的条件开始判断，他们还有“短路判断”特性。 对于或||来说，一旦所判断的条件里有一个为TRUE，那么它将不再判断尚未评定的条件，而是直接将结果定为TRUE。

#### 2.4.2 输出非边框字符
与上一节相似，这一节我们只需要找出在什么条件下需要输出字符就行了。 从行上来讲，当行为pad+1时，就是需要输出字符的那一行。 从列上来讲，当列为pad+1时，就是该输出字符的时候了。 那么，代码来了：
```
if(r == pad + 1 && c == pad +1) {
	std::cout << greeting;
	c += greeting.size();
}
```
一个小知识点： += 是复合型赋值，a += 1 相当于 a = a + 1

### 2.5 程序的全貌
这一节介绍了另一个循环的语法for:
```
for (int r = 0; r != rows; ++r){
	//不改变r值的语句。
}
```
设r的初始值为0，当r不等于rows时，执行循环体，然后r自增1。这就是for的用法，将控制循环次数的变量全都放到条件内，便于检查。

程序的全貌：
```
#include <iostream>
#include <string>
// say what standard-library names we use
using std::cin; using std::endl;
using std::cout; using std::string;
int main()
{
 // ask for the person's name
 cout << "Please enter your first name: ";
 // read the name
 string name;
 cin >> name;
 // build the message that we intend to write
 const string greeting = "Hello, " + name + "!";
 // the number of blanks surrounding the greeting
 const int pad = 1;
 // the number of rows and columns to write
 const int rows = pad * 2 + 3;
 const string::size_type cols = greeting.size() + pad * 2 + 2;
 // write a blank line to separate the output from the input
 cout << endl;
 // write rows rows of output
 // invariant: we have written r rows so far
 for (int r = 0; r != rows; ++r) {
 string::size_type c = 0;
 // invariant: we have written c characters so far in the current row
 while (c != cols) {
 // is it time to write the greeting?
 if (r == pad + 1 && c == pad + 1) {
 cout << greeting;
 c += greeting.size();
 } else {
 // are we on the border?
 if (r == 0 || r == rows - 1 ||
 c == 0 || c == cols - 1)
 cout << "*";
 else
 cout << " ";
 ++c;
 }
 }
 cout << endl;
 }
 return 0;
}
```

### 2.6 计数

通过for的应用我们可以发现，计数时我们是从0开始，然后到rows结束，计数范围为[0, rows),左闭右开。 为什么不从1开始计数呢，因为从1开始计数的话，就是[1, rows], 个数为rows-1+1, 相较于上一种计数方式运算起来要复杂一些，上一种计数方式为rows-1。  

习题没啥特别的，开始下一章！

## Chapter 3 处理数据

前面两章主要是对于字符的输出，这章我们就开始计算数据了！

### 3.1 计算学生成绩
如果计算学生学期总成绩的方式为期末考试占40%，期中考试占20%，作业占40%，那么我们计算学生总成绩的代码为：
```
#include <iomanip>
#include <ios>
#include <iostream>
#include <string>
using std::cin; using std::setprecision;
using std::cout; using std::string;
using std::endl; using std::streamsize;
int main()
{
 // ask for and read the student's name
 cout << "Please enter your first name: ";
 string name;
 cin >> name;
 cout << "Hello, " << name << "!" << endl;
 // ask for and read the midterm and final grades
 cout << "Please enter your midterm and final exam grades: ";
 double midterm, final;
 cin >> midterm >> final;
 // ask for the homework grades
 cout << "Enter all your homework grades, "
 "followed by end-of-file: ";
 // the number and sum of grades read so far
 int count = 0;
 double sum = 0;
 // a variable into which to read
 double x;
 // invariant:
 // we have read count grades so far, and
 // sum is the sum of the first count grades
 while (cin >> x) {
 ++count;
 sum += x;
 }
 // write the result
 streamsize prec = cout.precision();
 cout << "Your final grade is " << setprecision(3)
 << 0.2 * midterm + 0.4 * final + 0.4 * sum / count
 << setprecision(prec) << endl;
 return 0;
}

```
这里需要先介绍两个新的库<iomanip> 和<ios>，我们这个程序用到的是<ios>中的streamsize, 用来定义数据流的大小，<iomanip>用到的是setprecision，用来定义输出数值的精确度。

程序里有几个要点需要注意一下：
+ cout 输入的字符串可以通过空格从视觉上分成多行，但实际会作为一个字符串输出。
+ 小数一般用double，双精度在现在来说已经没那么耗资源了。
+ 除了从外部输入的值以外，一般都要给个合适的初始值，否则系统将会自动分配默认值为初始值，不好控。
+ 在cout的输入中我们先设了输出精确度为3，setprecision(3)，在结尾处又将精确度重置为cout的默认值setprecision(pred)，当然也可以用cout.precision(prec)来重置它，而直接用setprecision更简洁一些。

#### 3.1.1 测试输入
程序中使用了一个while新的用法： `while(cin >> x)`，如果输入成功存到x,那么while为真并继续，如果输入结束或者输入值因类型不同无法存入x，则条件为假循环结束。

`>>`是左运算符，`cin>>x`先将输入存到x（副作用）,然后返回cin来显示是否成功。因此if(cin>>x)可以理解为cin>>x然后if(cin)。

在我们目前的应用中，有三种情况会是的循环条件为假：
+ 到达输入数据的结尾
+ 输入数据与x类型不匹配
+ 输入硬件问题

一旦我们不能从数据流读入数据，我们必须重置这个数据流来继续从数据流读入数据，将在第四章讲到。

#### 3.1.2 循环常量
循环常量为已经读取了数过的成绩（++count）并且总和为数过成绩的总和（sum+=x）

### 3.2 使用中位数而不是平均数
这一节其实就是要把家庭作业的所有数据存起来排序来找到中位数。 相对于平均数来说，中位数更能代表实际的平均水平，因为平均数有可能因为一两次的极低分数而被拉低。

#### 3.2.1 将数据存到向量中

向量vector可以将一系列同一类型的数据存到一起：vector<datatype> variable_name。

```
double x;
vector<double> homework;

while(cin>>x){
	homework.push_back(x);
}
```
`push_back()`是vector类中的一种方法，可以将元素添加到向量的末尾。

#### 3.2.2 生成输出
为了找到中位数，我们需要知道向量中元素的个数：
```
typedef vector<double>::size_type vec_sz;
vec_sz size = homework.size(); 
```
typedef起到了简化的作用，通过typedef， vec_sz实际上就是vector<double>::size_type。

知道向量的个数之后，我们就可以将向量以非降序排序，之所以是非降序是因为有时会出现几个相同的值。 排序算法在<algorithm>里就有现成的，`sort(homework.begin(), homework.end());`

通过判断元素个数为奇偶数就可以找到相应的中位数了：
```
vec_sz mid = size / 2;
double median;
median = size % 2 == 0 ? (homework[mid] + homework[mid-1]) / 2 : homework[mid];
```

#### 3.2.3 注意事项
+ 在vector为空的情况下要中断程序返回1
+ vector<double>::size_type是无符号整型，当无符号整型与一般的整型在同一表达式中时，*计算的结果也将是无符号整型*


## Chapter 4 函数与数据
这一章主要是将功能性的代码整合为函数以及可编译的单独文件，以便重复使用。

### 4.1 将计算整合起来
当我们要多次用到同一种计算行为的时候，我们就该考虑将这个计算行为转变成函数来调用了。就像在上一章计算总成绩：
```
// compute a student's overall grade from midterm and final exam grades and homework grade
double grade(double midterm, double final, double homework)
{
 return 0.2 * midterm + 0.4 * final + 0.4 * homework;
}
```
括号中是函数的输入变量，也叫形参，大括号里的是函数主体，返回的可以是个值也可以是其他函数。

#### 4.1.1 找中位数
从向量中找中位数的方法也可以多次使用：
```
// compute the median of a vector<double>
// note that calling this function copies the entire argument vector
double median(vector<double> vec)
{
 typedef vector<double>::size_type vec_sz;
 vec_sz size = vec.size();
 if (size == 0)
 throw domain_error("median of an empty vector");
 sort(vec.begin(), vec.end());
 
 vec_sz mid = size / 2;
 return size % 2 == 0 ? (vec[mid] + vec[mid-1]) / 2 : vec[mid];
}

```
值得注意的是当向量为空时，我们需要向程序使用者发出警告/提醒“exception"，这里我们用到的是`throw domain_error("what?")`。 domain_error是exception object的一种，被定义在<stdexcept>中,用来表明程序的输入超出了程序所能处理的范围。

形参作为输入会被拷贝到程序定义的局部变量中，例如输入的向量被拷贝到vec中。 这样的好处是当vec被排序时，原向量不会发生改变。

#### 4.1.2 重新编写计算分数
```
// compute a student's overall grade from midterm and final exam grades
// and vector of homework grades.
// this function does not copy its argument, because median does so for us.
double grade(double midterm, double final, const vector<double>& hw)
{
 if (hw.size() == 0)
 throw domain_error("student has done no homework");
 return grade(midterm, final, median(hw));
}

```
这个函数的知识点很重要，第三个形参为`const vector<double>& hw`意为reference to vector of const double，双精度常量向量的参照,也就是说给const vector<double>起了一个别名叫hw。
```
vector<double> homework;
vector<double>& hw = homework; // hw is a synonym for homework
```
homework和hw是同一个东西，改动其中任一变量都会使另一变量发生改变。
```
// chw is a read-only synonym for homework
const vector<double>& chw = homework;

```
加了const前缀后，可以保证我们不会对chw做任何变动。

由于参照是原变量的另一个名字，因此不会有参照的参照，这样并没有意义，所有的参照都会指向原变量。 

非常量的参照不能指向常量或者常量参照：
```
vector<double>& hw2 = chw;//非法
```
因为常量不能被更改。

由于形参是const参照，所以可以指向const和非const的向量，而且由于形参是参照，我们就省去了拷贝的资源。

另外一个知识点是函数的重载。在grade函数内部我们又调用了grade，但其实这是两个函数只不过同名而已，不同的地方在于形参不一样，C++通过形参来区分同名的函数，即为函数的重载。

#### 4.1.3 读取家庭作业成绩

在读取用户输入的家庭作业成绩时，我们需要得到两个返回值，一个是输入的成绩向量，另一个是输入完成的状态，而C++的函数只能返回一个值，这一节我们介绍一个间接的方法来获得两个值。

主要诀窍就是使用参考变量：
```
istream& read_hw(istream& in, vector<double>& hw) {
 // we must fill in this part
 
 return in;
}
```
程序返回值为istream类型的in