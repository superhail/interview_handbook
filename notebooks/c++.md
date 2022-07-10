## varint

## concept

## STL

两级配置器(第一级用于一般情况，小于128bytes的时候就使用配置器维护16个自由链表)

一共有哪些部分组成: **迭代器, functor, 算法, 容器, 类型萃取, adapter**

## static的作用

1. static修饰的全局变量仅在该编译单元中可以被使用。静态局部变量具有全局的生命周期，但是作用域依然是局部的。(可以用于实现单例)
2. static修饰的类成员具有静态的生命周期，被存储在静态区

一般全局变量都使用static即可

## c++多态

静态多态用重载和模板来实现；动态多态用虚函数来实现

## 虚函数的底层实现机制

为每个类对象添加一个隐藏成员，隐藏成员中保存了一个指向函数地址数组的指针，称为虚表指针（vptr），这种数组成为虚函数表（virtual function table, vtbl），即，**每个类使用一个虚函数表，每个类对象用一个虚表指针**。

对象 A 实例的**头部**是一个 vtable 指针，紧接着是 **A 对象按照声明顺序排列的成员变量**。

虚函数表的结构其实是有一个头部的，叫做 vtable_prefix ，紧接着是按照声明顺序排列的虚函数。

typeinfo本质上也是一个类，存储着基类的信息。

<img src="https://jacktang816.github.io/img/cpp/virtualFunction/vptrLocation.png" alt="img" style="zoom: 67%;" />

代价：主要的代价体现在虚表指针占用的内存(每继承一个就会有4Nbyte)，运行速度的代价仅仅体现在无法inline这一点

应用事项

1. **使用基类指针或引用来调用虚函数，它都不能为内联函数(因为调用发生在运行时)**。
2. static成员不属于任何类对象或类实例，所以即使给此函数加上virutal也是没有任何意义的。
3. 构造函数不能是虚的。**虚函数的运行依赖于虚函数指针，而虚函数指针在构造函数中进程初始化，让它指向正确的虚函数表，而在对象构造期间，虚函数指针还未构造完成。**
4. **纯虚析构函数必须有定义体**

## char to unsigned int

char a = 255;

unsigned int b = a; // b == std::numeric_limits<unsigned int>::max();

255 => 2^8 - 1 => 2^32 - 1

`char` is signed by default.

## <<和>>运算符的重载

```c++
friend istream &operator>>( istream  &input, Distance &D )
{ 
    input >> D.feet >> D.inches;
    return input;            
}
```

