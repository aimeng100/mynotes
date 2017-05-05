# c++ class 基础

## 语法
```c++
class Name{
public:
  Name();
  ~Name();
  string get_name();
  void print_name();
private:
  string name;
}
```

基本构成部分：

- 构造函数

- 析构函数

- 其他函数与属性

## class中常量处理

- 在类定义时，只能给static const 成员属性赋初值，其它都不行。

- 对于 const：需要在构造函数初始化列表中初始化

- static const：必须在定义的时候初始化，可以看作为编译期间常量

- 可以使用无标记 enum 代替 static const。
```c++
class Bunch{
  enum{size=1000};
  int i[size];
}
```

## const 对象与成员函数

什么是`const`对象：
```c++
const Name name;//const对象，对象的数据成员在生命期内不会被改变
```
**只能调用`const`对象的const成员函数！！**

为什么呢？

因为编译器通过成员函数是否为`const`来得知此成员函数是否更改了对象的数据成员。

```c++
class X{
  int i; //class 默认为private
public:
  X(int ii);
  int f() const; //注意和返回值为常量的函数的区别。
}

X::X(int ii):i(ii){}
int X::f() const {return i}
```

## 内联函数
内联函数：能够像普通函数一样具有我们所有期望的任何行为，与普通函数不同之处在于，**内联函数在适当的地方像宏一样展开，所以不需要调用函数的开销。**

```c++
//函数声明和定义要写在一起！！
inline int plusOne(int x){
  return ++x;
}
//一定要把内联函数放在头文件里

//类内部定义的函数自动成为内联函数
class Name{
  string name;
public:
  Name(string nname):name(nname){}//内联
  ~Name(){}//内联
  void print(){cout<<name<<endl;}//内联
}
```