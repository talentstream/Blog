---
title: c++ primer
date: 2023-04-15 21:19:35
---

### 前言

由于面试被狠狠拷打，决定恶补c++。有些概念太长会以图片显示

### 变量和基本类型

#### 基本类型

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418202838.png)

一些类型选择的建议：

- 数值不可能为负时，选用无符号类型
- 使用int执行整数运算，如果超过int范围，选用longlong
- 算术表达式中不要使用char或bool,只有在存放字符或bool值才使用它们。因为char在有些机器是有符号的，而在一些机器上又是无符号的。
- 执行浮点数运算用double，float常常精度不够，而且双精度和单精度的计算代价相差无几。

#### 类型转换

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418203722.png)

- 将非bool型算术值赋给bool时，为0则结果为false，否则为true
- 当bool值给非bool型，为false则结果为0，true 为 1
- 当浮点数赋给整数类型时，砍掉小数点后面的
- 当整数赋给浮点时，小数部分为0
- 当给unsigned赋给一个超出范围的值时，结果是初始值加表示数值总数取模后的余数，在这里就是(-1+256)%256
- 当给一个有符号类型一个超出范围的值时，结果时未定义的。程序可能继续工作、可能崩溃，也可能产生垃圾数据。

当一个算数表达式既有unsigned又有int时，int就会转化为unsigned

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418204711.png)

当 u = 0 时，迭代输出0，然后执行--u，此时 u = -1 被自动转化为4294967295，此时会无限循环

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418204946.png)

#### 字面值常量

以0开头代表八进制数，0x或0X开头代表十六进制，比如：
![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418205302.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418205426.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418205542.png)

#### 变量

当对象在创建时获得了一个特定值，我们说这个对象被初始化了。如果定义变量时没有指定初值，则变量被默认初始化，此时被赋予了“默认值”。定义于任何函数体之外的变量被初始化为0，定义在函数体内部的内置变量将不被初始化，由于是未被定义的，试图拷贝或以其他形式访问此值将引发错误。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418205841.png)

#### 声明与定义

c++将声明和定义区分开来，声明使得名字为程序所知，定义负责创建与名字关联的实体。

变量声明规定变量的类型和名字，在这一点上定义与之相同，但除此之外，定义还申请存储空间，也可能为变量赋一个初始值。

```c++
extern int i; // 如果想声明一个变量而非定义它，在变量名前添加关键字extern
int j;// 声明并定义 j
extern double pi = 3.1416; // extern语句如果包含初始值就不再是声明，而变成定义了。
// 如果在函数体这样写，将会引发错误。
```

### 指针和引用

#### 引用

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418211425.png)

- 引用即别名。
- 引用本身并不是一个对象，不能定义引用的引用。
- 引用类型要与之绑定的对象严格匹配。
- 引用只能绑定在对象上，不能与字面值或某个表达式的计算结果绑定在一起。

#### 指针

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418211747.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418211809.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418211905.png)

指针的值（地址）应属于下列4种状态之一：

- 指向一个对象
- 指向紧邻对象所占空间的下一个位置
- 空指针，意味着指针没有指向任何对象
- 无效指针，也就是上述情况之外的其他值，试图拷贝或以其他形式访问无效指针都将引发错误

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418212135.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418212340.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418212627.png)

```c++
int *&r = p; // 从右往左读，离变量名最近的符号对变量的类型有最直接的影响，因此r是一个引用。*说明r引用的是一个指针。
```

### const

默认状态下，const对象仅在一个文件内有效，如果程序包含多个文件，同名的const变量其实等同于在不同文件中分别定义了独立的变量。解决的方法便是在const变量前加extern

```c++
extern const int i = 5;
```

#### const与引用

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418213248.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418213820.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418214147.png)

由于const引用也经常被称为常量引用，所以在正常引用中不能做的——使用字面值或者表达式作为初始值，类型不一致，在const引用中都可以做

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418214232.png)

#### const与指针

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418214516.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418214614.png)

#### 顶层与底层const

顶层const表示指针本身是个常量，底层const表示指针所指的对象是一个常量，也就是说，顶层const表示的对象是常量，无法改变。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418215607.png)

##### constexpr 和常量表达式

常量表达式指值不会改变且在编译过程就能得到计算结果的表达式。

```c++
const int max_files = 20; // 是常量表达式
const int limit = max_files + 1;// 是常量表达式
int staff_size = 27;// 不是常量表达式
const int sz = get_size();// 不是常量表达式
```

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418220303.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418220655.png)

### 处理类型

#### 类型别名

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418220844.png)

#### auto   

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418221240.png)

#### decltype

decltype 作用是选择并返回操作数的数据类型。编译器只分析表达式得到类型，却不实际计算表达式的值

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418221458.png)

### 数组

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418222613.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230418222654.png)

使用数组下标时，通常将其定义为size_t类型。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419093955.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094201.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094228.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094312.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094545.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094557.png)

严格来说，c++没有多维数组，通常说的多维数组其实是数组的数组

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419094706.png)

### 表达式

#### 左值右值

当一个对象被用作右值的时候，用的是对象的值（内容）；当对象被用作左值的时候，用的是对象的身份（在内存中的位置）。

#### 求值顺序

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419095331.png)

#### 取余

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419095540.png)

#### ++i 还是 i++

前置版本将对象本身作为左值返回，后置版本则将对象原始值的副本作为右值返回。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419095813.png)

#### 条件运算符

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419095939.png)

#### 位运算符

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419100130.png)

#### sizeof 运算符

sizeof 返回一条表达式或一个类型名字所占的字节数。其所得值是一个size_t类型的常量表达式。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419100642.png)

#### 显式转换

- static_cast: 只要不包含底层const，就可以用。当需要把一个较大的算数类型复制给较小的类型时，同时我们不在乎潜在的精度损失，static_cast就非常有用。
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419104556.png)
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132259.png)
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132320.png)

- dynamic_cast:运行时类型识别的运算符，用于将基类的指针或引用安全地转化为派生类的指针或引用。
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132236.png)

- const_cast: 它只能改变运算对象的底层const，一般称其为“去掉const性质”，一旦去掉，编译器就不再组织我们对该对象进行写操作了。
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419105145.png)

- reinterpret_cast: 通常为运算对象的位模式提供较低层次的重新解释。
  ![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419110344.png)
```c++
int* p = new int(65);
char* ch = reinterpret_cast<char*> (p);
cout << *p << endl; // 65
cout << *ch << endl; // A
cout << p << endl; // 地址00000249CE417930
cout << ch << endl; // A
```
> 举个例子，32位系统，int是32位，指针也是32位，我既可以把一个32位的值解释成一个整数，也可以解释成一个指针。至于究竟能不能这样解释，由程序员负责。而reinterpret_cast就是干这个事的。
> [C++类型转换之reinterpret_cast](https://zhuanlan.zhihu.com/p/33040213)

#### RTTI 运行时类型识别

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132434.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132459.png)

typeid 作用于对象，我们应该用*bp而非bp

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132655.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230419132730.png)

### 函数

#### 局部对象

名字有作用域、对象有生命周期。

- 名字的作用域是程序文本的一部分，名字在其中可见
- 对象的生命周期是程序执行过程中该对象存在的一段时间

自动对象：我们把只存在于块执行期间的对象称为自动对象。当块的执行结束后，块中创建的自动对象的值就变成未定义的了。

形参是一种自动对象。函数开始时为形参申请存储空间，函数一旦终止，形参就被销毁。

局部静态对象：在程序的第一次执行初始化，直到程序终止才销毁。在此期间，即使对象所在的函数结束执行也不会对它有所影响。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421105708.png)

#### 传值参数

形参初始化的原理与变量初始化一样。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110256.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110522.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110618.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110649.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110735.png)

**含有可变形参的函数** ： 

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110825.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421110855.png)

#### 函数返回值

不要返回局部对象的引用或指针：函数完成后，它所占用的存储空间也随之被释放掉。因此，函数终止意味着局部变量的引用将指向不再有效的内存区域。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421111054.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421111845.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421111856.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421111906.png)

#### 函数重载

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421112312.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421112244.png)

#### 内联函数

内联函数可避免函数调用的开销，一般来说，内联机制用于优化规模较小，流程直接，频繁调用的函数。就比如说，调用函数比函数执行时间长，用内联函数就行了。

#### constexpr 函数

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421125221.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421125231.png)

#### 实参类型转换

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421125357.png)

#### 函数指针

感觉类似于c#的委托，像是给一个函数的别名

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230421130122.png)

### 初步探索类

#### const成员函数

常量对象、以及常量对象的引用或指针都只能调用常量成员函数。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422204832.png)

简单来说，就是让该函数的权限为只读，也就是说没法去改变成员函数的值。
同时，如果一个对象为const，它只有权力调用const函数，因为成员变量不能改变。

#### 构造函数

不同于其他函数，构造函数不能被声明成const。

如果我们的类没有显式地定义构造函数，那么编译器就会为我们隐式地定义一个默认构造函数。又称为合成默认构造函数，按照一下规则初始化类地数据成员

- 如果存在类内的初始值，就用它来初始化成员
- 否则，默认初始化该成员。

某些类不能依赖于合成的默认构造函数，原因如下：

- 对于一个普通的类来说，必须定义它自己的默认构造函数。只有类不包含任何构造函数的情况下才会自动生成默认构造函数。
- 对于某些类来说，合成的默认构造函数可能执行错误的操作。如果定义在块中的内置类型或复合类型（数组和指针）被默认初始化，则它们的值将是未定义的。
- 如果类中包含一个其他类类型的成员且这个成员没有默认构造函数，那么编译器将无法初始化该成员。

= default，即要求编译器生成默认构造函数，如果在类的内部，默认是内联的，如果在类的外部，默认不是内联的。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422211706.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422211751.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422211833.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422212543.png)

#### 友元

类可以允许其他类或者函数访问它的非公有成员，方法是令其他类或者函数成为它的友元。

友元声明只能出现在类定义的内部，但是在类内出现的具体位置不限。友元不是类的成员也不受它所在区域访问控制级别的约束。一般来说，最好定义在类开始的位置或者结束的位置。

友元仅仅指定了访问权限，如果希望类能够调用某个友元函数，那么必须在友元声明之外在专门对函数定义一次。

#### 类的inline

在类中，常有一些规模较小的函数适合被声明内联函数，定义在类内部的成员函数是自动inline的。

#### 可变数据成员

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422211331.png)

#### 类的静态成员


类的静态成员存在任何对象之外，对象中不包含任何于静态数据成员有关的数据。静态成员函数也不予任何对象绑定在一起，它们不包含this指针。同时，静态成员函数不能声明成const，也不能在里面调用this指针。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230422213444.png)

### c++标准库

#### 顺序容器

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425195814.png)

顺序容器的选择：

- 通常选择vector
- 有很多小元素，空间额外开销很重要，不要用list或forward_list
- 随机访问元素，用vector 或 deque
- 在中间插入或删除元素，应使用list或forward_list
- 头尾插入或删除元素，用deque
- 如果只有在输入时踩在中间位置插入元素，随后需要随机访问：考虑输入阶段用list，输入完成后拷贝到vector
- 又要随机访问，又要在中间位置插入元素，看访问操作多还是插入/删除元素操作多

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425200215.png)

#### 容器迭代器

begin指向第一个元素，end指向最后一个元素之后的位置通常称为左闭右合区间。即[begin,end)

- 如果begin == end 说明该范围为空
- 如果begin != end 说明至少包含一个元素，且begin指向该范围中的第一个元素
- begin可以递增，使得begin == end

```c++
while(begin!=end){
  *begin = val;
  ++begin;
}
```

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425200629.png)

当不需要写访问的时候，应该使用cbegin和cend

#### 容器定义和初始化

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425200725.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425200822.png)

#### 赋值和swap

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425200902.png)

assign 相对于赋值运算符(=)允许从以一个不同但相容的类型赋值（比如char* 和 string），或者从容器的一个子序列赋值。assign操作用所指定的元素的拷贝替换容器中的所有元素。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425201049.png)

swap操作交换两个相同类型的内容，保证操作很快，元素本身未被交换，只是交换了两个容器的内部数据结构。
元素不会被移动意味着，除string外指向容器的迭代器、引用指针在swap后都不会失效，除了string。
与其他容器不同，swap两个array会真正地交换元素。

#### 容器比较

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425201329.png)

#### 添加元素

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425201416.png)

- push_back、push_front、insert:放入到容器中的元素时对象值地一个拷贝而不是对象本身。
- emplace操作:则是将参数传递给元素类型的构造函数，直接在容器管理的内存空间中直接构造元素，参数必须与元素类型的构造函数相匹配。

#### 访问元素

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425201920.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202108.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202245.png)

#### 删除元素

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202408.png)

#### 改变容器大小

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202449.png)

#### string 操作

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202540.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202609.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202654.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202711.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202727.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425202750.png)

#### 容器适配器

也就是让容器看起来像一种不同的类型，比如说queue是基于deque实现的。比较常见的时stack，queue,priority_queue。

### 泛型算法

算法永远不会改变底层容器的大小，可能改变值，可能移动元素，但永远不会添加或删除元素

```c++
// 只读算法
int *result = find(vec.begin(),vec.end(),val);//查找算法
int result = count(vec.begin(),vec.end(),val);// 统计个数
int result = accumulate(v.cbegin(),vec.cend(),0);// 求和、和的初值设置为0
string result = accumulate(v.cbegin(),vec.cend(),""); // 将vec的每个元素连起来
bool result = equal(vec.cbegin(),vec.cend(),other.cbegin());// 比较算法，确定两个序列是否保存相同的值，基于两个序列相等的假设。

// 写算法
fill(vec.begin(),vec.end());// 将元素重置为0
fill(vec.begin(),vec.begin() + vec.size()/2,10);//将子序列都赋为10
fill_n(vec.begin(),vec.size(),0); // 与fill稍微不同，是从vec.begin开始将vec.size()个元素变为0。
// 要注意的是，fill_n假定begin指定一个元素，从begin开始的序列至少包含vec.size()个元素，容易犯的错误就是在空容器调用fill_n
auto ret = copy(vec.begin(),vec.end(),vec2);// 将vec拷贝到vec2中，返回目的位置迭代器即vec2为元素之后的位置
replace(a.begin(),a.end(),0,42);//将0变为42
replace_copy(a.cbegin(),a.cend(),back_inserter(b),0,42);//将a拷贝到b但是拷贝时0都编程42

// 重排元素算法
sort(a.begin(),a.end());// 从小到大排序
auto end_unique = unique(a.begin(),a.end());//排列范围的元素，指向不重复区域之后一个位置的迭代器

```

#### lambada表达式与泛型算法

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425205348.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425205429.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425205447.png)

```c++
void biggies(vector<string> &words.vector<string>::size_type sz)
{
  elimDups(words);//将words按字典序排序，删除重复单词
  stable_sort(words.begin(),words.end(),[](const string &a,const string &b){return a.size() < b.size()});
  auto wc = find_if(words.begin(),words.end(),[sz](const string &a){return a.size() >= sz});
  auto count = words.end() - wc;
  for_each(wc,words.end(),[](const string &s){cout<< s << " "});
}
```

#### lambada 捕获

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425211551.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230425211902.png)

### 动态内存和智能指针

程序使用动态内存的原因：1.程序不知道自己需要使用多少对象。 2.程序不知道所需对象的准确类型。 3.程序需要在多个对象间共享数据。
动态内存很难使用，有时候会忘记释放内存，这时会产生内存泄漏；有时指针引用内存的情况下指针已经被释放这时会产生引用非法内存的指针。

#### shared_ptr

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501202449.png)

默认初始化的智能指针保存一个空指针

```c++
shared_ptr<string> p1;// 初始化方式与vector一样
if(p1 && p1->empty())
  *p1 = "hi"
// 如果p1不为空，检查它是否指向一个空string
```

最安全的分配和使用动态内存的方法是调用一个名为make_shared的标准库函数。此函数在动态内存中分配一个对象并初始化它，返回指向此对象的shared_ptr

```c++
// 指向一个值为42的int的shared_ptr
shared_ptr<int> p3 = make_shared<int>(42);
// 指向一个值为"9999999999"的string
shared_ptr<string> p4 = make_shared<string>(10,'9');
// 指向一个值初始化的int，即为0
shared_ptr<int> p5 = make_shared<int>();

// 类似于vector的emplace，传递参数类型必须相对应，不传递的话就会进行值初始化，通常用auto来保存

auto p6 = make_shared<int>();
```

当进行拷贝或赋值操作时，每个shared_ptr都会记录有多少个其他shared_ptr指向相同的对象。
每个shared_ptr都有一个关联的计数器，通常称为**引用计数**。当我们用一个shared_ptr去初始化另一个shared_ptr，或者作为参数传递给函数，或者作为函数返回值，所关联的计数器都会**递增**。赋予一个新值，或者shared_ptr销毁（比如离开作用域）计数器递减。一旦一个shared_ptr计数器变为0，会自动释放自己所管理的对象

```c++
auto r = make_shared<int>(42);
r = q;// 给 r 赋值让它指向另一个地址
// 递增 q 指向对象的引用计数
// 递减 r 原来指向对象的引用计数
// r 原来指向的对象没有引用者，自动释放
```

#### 直接管理内存

new 分配内存，delete释放new分配的内存

```c++
int *pi = new int; // 默认初始化，*pi的值未定义
int *pi1 = new int(); // 值初始化，*pi1为0
int *pi2 = new int(1024); // pi2指向的对象的值为1024
const int *pci = new const int(1024);// 分配并初始化一个const int
const string *pcs = new const string;// 分配并默认初始化一个const 的空string
// 一个动态分配的const对象必须初始化
// 对于一个定义了默认构造函数的类类型
// 其const动态对象可以隐式初始化
// 而其他类型对象就必须显式初始化
// 由于分配对象是const，new返回的指针是一个指向const的指针

// 如果内存不够用，内存分配失败
int *p1 = new int;// new抛出std::bad_alloc
int *p2 = new (nothrow) int;// new 返回一个空指针
```

delete做两步：销毁给定指针指向的对象;释放对应的内存

```c++
int i;
int *pi1 = &i;
int *pi2 = nullptr;
double *pd = new double(33);
double *pd2 = pd;
delete i;// 错误，i不是指针
delete pi1;// 未定义,pi指向一个局部变量
delete pd;// 正确
delete pd2;// 未定义，pd2指向的内存已经被释放了
delete pi2;// 正确，释放一个空指针没有错误
```

由内置指针管理的动态内存在被显式释放(delete)前一直都会存在

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501205622.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501205711.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210052.png)

#### unique_ptr

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210525.png)

- 与shared_ptr不同，某个时刻**只能有一个unique_ptr指向一个给定对象**。当unique_ptr被销毁时，所指向的对象也被销毁。
- 与shared_ptr不同，没有类似make_shared的标准库函数，定义unique_ptr时，**需要将其绑定到一个new返回的指针上**。
- 由于一个unique_ptr拥有所指向的对象，所以**不支持普通的拷贝或赋值操作**。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210603.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210639.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210650.png)

#### weak_ptr

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230501210929.png)

weak_ptr是一种不控制所指向对象生存期的智能指针，它指向由一个shared_ptr管理的对象。将一个weak_ptr绑定到一个shared_ptr不会改变引用计数。一旦最后一个指向对象的shared_ptr被销毁，对象就会被释放。即使有weak_ptr指向对象，对象也还是会被释放。

```c++
// 创建一个weak_ptr时，要用一个shared_ptr来初始化它
auto p = make_shared<int>(42);
weak_ptr<int> wp(p); 

// 由于对象可能不存在，不能使用weak_ptr直接访问对象
// 而必须调用lock，此函数检查weak_ptr所指对象是否仍然存在
if(shared_ptr<int> np = wp.lock)
{
  //在if中，np与p共享对象
}
```

### 拷贝控制

#### 拷贝构造函数

如果一个**构造函数**的**第一个参数**是**自身类类型**的引用，且任何额外默认参数都有默认值，则为拷贝构造函数。

```c++
class Foo{
public:
  Foo();// 默认构造函数
  Foo(const Foo&);// 拷贝构造函数
};
```

如果我们没有为一个类定义拷贝构造函数，编译器会为我们构造一个。与合成默认构造函数不同，即使我们定义了其他构造函数，编译器也会为我们合成一个拷贝构造函数。编译器从给定对象中依次将每个非static成员拷贝到正在创建的对象中。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506195211.png)

**直接初始化**：实际上是要求编译器使用普通的函数匹配来选择与我们提供的参数最匹配的构造函数。

**拷贝初始化**：我们要求编译器将右侧运算对象拷贝到正在创建的对象中，如果需要的话还要进行类型转换。通常使用拷贝构造函数完成，如果有移动构造函数，则有时会使用移动构造函数。

拷贝初始化的发生情况：

- =定义变量
- 将一个对象从实参传递给非引用的形参
- 返回类型为非引用类型的函数返回的对象
- 用花括号列表 初始化一个数组中的元素或一个聚合类的成员
- 标准库容器insert/push，与之相对，用emplace创建的元素都进行直接初始化

拷贝函数在这几种情况下都会被隐式地使用，因此，拷贝构造函数不应是explicit的

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506200110.png)

#### 拷贝赋值运算符

```c++
Sales_data trans,accum;
trans = accum; // 使用Sales_data 的拷贝赋值元素符
```

与类控制对象如何初始化一样，类也可以控制其对象如何赋值。与拷贝构造函数一样，如果未定义，编译器会为它合成一个。

```c++
class Foo{
  public:
    Foo& operator=(const Foo&);//赋值运算符
}
// 赋值运算符通常返回一个指向其左侧运算对象的引用
```

拷贝赋值元素运算符会将右侧对象的每个非static成员赋予左侧对象的对应成员

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506200857.png)

#### 析构函数

析构函数释放对象使用的资源，并销毁对象的非static数据成员。析构函数**没有返回值，也不接受参数，不能呗重载，一个给定类只有唯一一个析构函数**。同时，析构函数自动运行，程序按需分配资源，通常无须当心何时释放这些资源

在析构函数中，先执行函数体，然后销毁成员。按初始化顺序的**逆序**销毁。释放对象在生存期分配的所有资源。
析构部分式隐式的，成员销毁时完全依赖于成员的类型。销毁类类型的成员需要执行成员自己的析构函数。内置类型成员没有析构函数，什么都不需要做。
隐式销毁内置指针类型的成员不会delete它所指地对象。

调用析构函数的时机：

- 变量离开其作用域时
- 对象被销毁，成员被销毁
- 容器被销毁
- 动态分配的对象，对指向它的指针应用delete时
- 临时对象，创建它的完整表达式结束时被销毁

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506201821.png)

未定义时，编译器会为它定义一个合成析构函数，析构函数体自身不直接销毁成员，成员时在析构函数体执行后隐式销毁的。

如果一个类需要自定义析构函数，几乎肯定的是，也需要自定义拷贝赋值运算符和拷贝构造函数。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506203014.png)

#### =default

使用=default来显式地要求编译器生成合成的版本
当我们使用=default时，合成的函数会被隐式地声明为inline



我们只能对具有合成版本的成员函数使用=default

#### =delete

我们可以为任何函数指定=delete（除了析构函数）
=delete函数：虽然我们声明了它们，但不能以任何方式使用它们。
=delete主要用于禁止拷贝控制成员，如果希望引导函数匹配过程，删除函数有时也是有用的。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506203438.png)


![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506203413.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506203743.png)

尽可能使用=delete来阻止拷贝，而不应该声明为private

#### 拷贝控制和资源管理

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506204218.png)

**行为像值的类**：每个类的对象都有自己的实现

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506204605.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506204742.png)

**行为像指针的类**：所有类的对象共享类的资源，比如shared_ptr。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506211340.png)

主要的不同体现在拷贝构造函数中，析构函数和拷贝赋值运算符依据引用计数有所改变

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506211509.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506211603.png)

#### 交换操作

对于重拍元素顺序的算法，定义swap时非常重要的。
如果一个类定义了自己的swap，那么算法将使用自定义版本，否则将使用标准库的swap。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506211803.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506211925.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506212016.png)

### 对象移动

在某些情况下，对象拷贝后就立即被销毁了。这时候，移动而非拷贝对象会大幅度提升性能。

#### 右值引用

通过&&来获得右值引用，只能绑定到**一个将要销毁的对象**。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230506231308.png)

变量是左值，因此我们不能将右值引用绑定到变量上，即使是右值引用类型。

标准库move函数，可以显示地将一个左值转换为对应的右值引用类型。

```c++
int &&rr3 = std::move(rr1);
// move告诉编译器，将rr1当作右值一样处理
// 除了对rr1赋值或销毁，我们不再使用它
```

#### 移动构造函数

移动构造函数的第一个参数是一个右值引用，保证移后元对象处于一个状态——销毁无害。一旦资源完成移动，源对象必须不再指向被移动的资源——这些资源的所有权归属新创建的对象。

```c++
StrVec::StrVec(StrVec &&s) noexcept //告诉标准库我们的构造函数不抛出任何异常
// 成员初始化接管s的资源
:elements(s.elements),first_free(s.first_free),cap(s.cap)
{
  s.elements = s.first_free = s.cap = nullptr;
  // 被接收后指针都置为nullptr
}
```

#### 移动赋值运算符

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507001946.png)

在这里，我们检查this 与 rhs的地址是否相同。相同不做任何事情。否则释放已有元素，然后接管右值引用的元素。再把rhs指针赋为nullptr

**在移动后，移后源对象必须可析构**。

#### 合成移动操作

如果一个类定义了拷贝构造函数、拷贝赋值运算符或者析构函数，编译器就不会为它合成移动构造函数和移动赋值运算符。
只有当一个类**没有定义任何自己版本的拷贝控制成员**，且**类的每个非static数据成员都可以移动**时，编译器才会为它合成移动构造函数或移动赋值运算符。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507002510.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507002957.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507003227.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507003912.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507004102.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507004122.png)


### 面向对象程序设计

面向对象程序设计基于三个基本概念：数据抽象、继承、和动态绑定。

#### 数据抽象、继承、动态绑定

**数据抽象**：只向外界提供关键信息，并隐藏其后台的实现细节，即只表现必要的信息而不呈现细节。C++ 类为数据抽象提供了可能。它们向外界提供了大量用于操作对象数据的公共方法，也就是说，外界实际上并不清楚类的内部实现。

**继承**：通过继承联系在一起的类构成一种层次关系。通常根部叫做**基类**，直接或间接从基类继承而来叫**派生类**。

**动态绑定**：当我们使用基类的引用（或指针）调用一个虚函数时将发生动态绑定。动态绑定即是在运行时选择函数的版本，在一定程度上忽略相似类型的区别，而以统一的方式使用它们的对象。

#### 基类和派生类

基类通常应该定义一个虚析构函数，即使该函数不执行任何实际操作。

因为在派生类有与基类对应的部分，所以能把派生类的对象当作基类对象来使用，也能将基类指针或引用绑定到派生类对象中的基类部分上。

```c++
Quote item;// 基类
Bulk_quote bulk;// 派生类
Quote *p = &item;// p指向Quote对象
p = &bulk;// p指向bulk的Quote部分
Quote &r = bulk;// r绑定到bulk的Quote部分
```

派生类先初始化基类部分，然后按照声明顺序初始化派生类的成员。

不管从基类中派生出多少个派生类，对于每个**静态成员**来说都只存在**唯一**的实例。

静态成员遵循通用的访问控制规则

**防止继承**，即在类名后跟一个关键字final

我们可以将**基类的指针（内置或智能）或引用绑定到派生类对象**上。例如，可以用Quote&指向一个Bulk_quote对象，也可以把一个Bulk_quote对象的地址赋给一个Quote*

```c++
// 静态类型在编译时就已知，是变量声明时的类型或表达式生成的类型
// 动态类型则是变量或表达式表示的内存中的对象的类型，运行时才知道
double ret = item.net_price(n);
// item的静态类型是Quote&
// 它的动态类型依赖于item绑定的实参
// 如果传递一个Bulk_quote，则item动态类型则是Bulk_quote
// 如果表达式既不是引用也不是指针，动态类型和静态类型永远一致。
// 比如Quote类型变量永远是一个Quote对象
```

```c++
// 不存在基类向派生类的隐式类型转换，即使一个基类指针或引用绑定在一个派生了对象上
Quote base;
Bulk_quote* bulkP = &base;
Bulk_quote& bulkRef = base;
// 以上都是错误的，不能将基类转化为派生类
Bulk_quote bulk;
Quote *itemP = &bulk;// 正确，动态类型是Bulk_quote
Bulk_quote *bulkP = itemP;// 错误，不能将基类转化成派生类

// 可以用dynamic_cast,如果在基类中含有一个或多个虚函数
// 如果已知某个基类转化派生类是安全的，可以用static_cast
```

当我们用一个派生类对象为一个基类对象初始化或赋值时，只有该派生类对象中的基类部分会被拷贝、移动或赋值，派生类部分会被忽略，也就是被切掉

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507144244.png)

#### 虚函数

动态绑定**只会在我们通过指针或引用调用虚函数**时才会发生。如果通过一个普通类型（非引用非指针）的表达式调用虚函数，在编译时就会将表达式的把呢不能确定下来。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507152318.png)

基类中的虚函数在派生类中隐含地也是一个虚函数。当派生类覆盖了某个虚函数时，该函数在基类中的形参必须与派生类中的形参严格匹配。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507152800.png)

如果虚函数使用默认实参，则基类和派生类中定义的默认实参最好一致。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507153006.png)

```c++
class Base{
  virtual void foo(){}
};
class Drived : public Base{  
  void foo()
  {
    foo();//递归调用自己
    Base::foo();//明确告诉编译器，调用Base::foo而不是自己
  }
};
```

#### 抽象基类

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507154155.png)

含有纯虚函数的类是抽象基类，我们**不能创建一个抽象基类的对象**。可以定义它的派生类，前提是这些类覆盖了纯虚函数。

派生类只初始化它的直接基类

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507155227.png)

#### 访问控制与继承

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507161237.png)

上述表示，如果友元通过派生类来访问protected成员是可以的。但是友元直接访问protected成员就不可以

[C++派生类的成员或友元只能通过派生类对象来访问基类的受保护成员? - 邱昊宇的回答 - 知乎](
https://www.zhihu.com/question/37051531/answer/70216882)

在类中用using声明改变访问级别，当然派生类只能为访问到的名字提供using

struct 默认public继承 
class 默认private继承

#### 继承的类作用域

派生类的作用域位于基类作用域之内，如果一个名字在派生类中无法解析，则会在外层基类作用域中寻找该名字的定义。

在编译时进行**名字查找**，意味着能够使用哪些成员由静态类型决定。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507164433.png)

派生类会覆盖基类的同名成员，我们可以通过作用域运算符来使用基类成员。

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507164558.png)

**名字查找**,假设调用obj->foo():

- 首先确定obj的静态类型
- 然后在obj的静态类型对应的类中查找foo。找不到，就一直往继承链上找。如果一直找不到，就报错。
- 一旦找到foo，进行类型检查
- 如果合法，则会根据是否是虚函数进行调用：1.如果时虚函数，则依据obj的动态类型的版本;2.如果不是，直接调用

我们可以看到**名字查找先于类型检查,所以会有以下结果**

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507165048.png)

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507165828.png)

#### 虚析构函数

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507211827.png)

#### 合成拷贝控制与继承

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507212141.png)

**派生类中删除的拷贝控制与基类的关系**：

- 基类中的默认构造函数、拷贝构造函数、拷贝赋值运算符或析构函数是delete或private，则派生类对应的是delete的。原因是编译器不能使用基类成员来执行这些操作
- 如果基类中有一个**private或delete的析构函数**，则派生类合成的默认和拷贝构造函数是delete，因为编译器无法销毁派生类对象的基类部分
- 编译器不会合成一个delete移动操作。当我们使用=default，如果基类中对应是delete或private，则派生类中是delete，原因是派生类基类部分不可移动。同样，基类析构函数delete或private，则派生类移动构造函数也是delete

**派生类拷贝或移动构造函数**：

在默认情况下，基类默认构造函数初始化派生类对象的基类部分。如果想拷贝或移动基类部分，则必须在派生类的构造函数初始值列表中**显式地使用**基类的拷贝（或移动）构造函数

**派生类赋值运算符**：同理，复制运算符也要显式地为基类部分赋值

**派生类析构函数**：销毁顺序与创建顺序相反，先执行派生类析构函数，再执行基类的。

如果构造函数或析构函数调用了某个虚函数，则应该执行与类型相对应的虚函数版本。

#### 继承的构造函数

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230507213936.png)

using声明不会改变构造函数的访问级别。
using声明不能指定explicit或constexpr，继承的构造函数如果有这些属性，那么也有。
构造函数的默认实参不会被继承。相反，会获得多个继承。比如，基类有一个接受两个形参的构造函数，第二个含有默认实参，则派生类获得两个构造函数，一个接受两个形参，一个只接受一个形参，对应没有默认值的形参。

如果基类含有几个构造函数，大多数派生类会继承这些构造函数。有两个例外情况：

- 派生类继承一部分构造函数，为其他构造函数定义自己的版本。
- 默认、拷贝和移动构造函数不会被继承，会按照正常规则被合成。