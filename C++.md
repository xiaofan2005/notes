<u>**中文在C++中由于编码方式很多，可能输出中文时可能会乱码**</u>

# 杂

1. #include   被称为预处理指令
2. iostream 为输入输出流（`istream`/`ostream`）
3. **using namespace是针对命名空间的指令**
4. `cin`>>?>>?;  `cin`函数用于输入数值
   `cout`<<"?"<<"?" ; `cout`函数可把紧随的“”之中的内容输出
5. \n是一个字符：换行符——`endl `是一个换行符（同时还能清清除缓存）
6. 强制类型转换：` float() `/` int()` /` double()`  括号内为想要转换的变量名
   隐含转换
7. `size(表达式)` `  sizeof（类型名）`

# 自定义数据类型

### typedef语句——为一个已有的数据类型另外命名 <!--起别名（笑）-->

​			语法形式：typedef 已有数据类型  新类型名表
​				例如：

```cpp						
typedef double area , volume;
area a;
volume b; 
```

### enum语句——枚举类型

声明形式： `enum` 枚举类型名 {枚举元素}；   <!--枚举元素是一个个的常量,不可对其赋值-->
	例如：

```cpp
enum weekday{sun,mon,tue,wed,thu,fri,sat};  // 枚举元素有默认值，他们对应为 0、1、 2.....
weekday a; a=mon;  // 定义一个weekday类型的变量a并赋值mon
a = weekday {4}; <=> a = thu;
//枚举值可以进行关系运算
enum weekday{sun = 4,mon=1,tue,wed,thu,fri,sat}; //枚举值可在声明时另行指定值，但最好保证枚举元素值不同;指定后，元素对应值为前一个已知值顺序增
//整数值不可直接赋值给枚举变量，需强制转换
```

### 结构体

同C

# 函数

函数可以嵌套调用，但不可以嵌套定义

## 参数传递机制

### 传递形参

- 只有在函数被**调用**的时候，才会分配形参的存储单元
- 实参可以是变量、常量、表达式·
- 实参类型同形参类型
- 单向传递

### 用引用做形参

- 引用（&）是标识符的别名
- 声明一个引用时，**必须同时**对它进行初始化，使它指向一个已存在变量
- 一旦一个引用被初始化后，就不可以改变指向其他对象
- 引用可做形参   //   void swap(int &a, int&b) 

```cpp
int i,j;
int &ri = i;//建立一个int型的引用ri，并将其初始化为变量i的一个别名
j = 10;
ri = j;//相当于i = j;
```

引用不是变量，并不会给分配存储

## 内联函数

- 用于不是很复杂但是调用的较为频繁的函数
- 声明时使用  关键字inline
- 内联函数体内不能有循环语句和switch
- 其定义在第一次调用之前

## 带默认形参值的函数

- 在**定义**时预先给出默认的形参值，调用时若给出实参，用实参值，否则用默认形参值.<!--不会在声明处给出默认值-->

- 在声明的默认形参值**右面**不能有普通的不带默认形参的参数

  ```cpp
  int add (int x=10,int y=5);
  int add (int c, int x=10,int y=5);
  int add (int x=10,int y=5,int c); //wrong
  int add (int x=10,int c,int y=5); //wrong
  ```

  ## 函数重载

  功能相近的函数在相同的作用域内以相同的函数名声明

  重载函数的形参必须不同：个数或类型不同		

  程序将依据实参和形参的类型及个数的最佳匹配来选择调用

  不可将不同功能的函数定义为重载
  
  1. 重载条件：函数名相同；参数列表不同
  2. 不可将不同返回值类型函数视作重载

## C++系统函数

使用系统函数必须包含头文件

# 类与对象

封装：将抽象出的数据成员、代码成员相结合成一个整体
实现封装：类声明中的{}

## 类

类是用户的一种自定义类型，声明形式：

```cpp
class clock//类名
{
    //函数或数据成员
    public:
    	void settime();
    	void showtime();
    private:
    	int hour,minute,second;
};
```

```cpp
class 类名称
{
	public: //公有类型成员（外部接口）
	private:// 私有成员;只允许类中的函数访问
    protected://保护型成员
};
```



- 所有的属性（类内变量）应当是 `private`，为了读取它们的值，你应当使用相应的 `GetXXX()` 方法（类内函数）。这通常叫做“封装”。
- 如果一个方法需要在外部被使用，则它应该是 `public` 的。一个类必须要有 `public` 的方法，否则这个类的存在毫无意义，因为它是一个完全封闭的个体。

### 成员函数

- 可以直接在类中给出成员函数的函数体
- 也可以先**在类中给出说明原型，类外给出函数体实现**(写出函数名，例：**`void clock::settime`**在前面加上所述的**类的名字**)
- 在成员函数中可直接调用成员数据也可以调用其他成员函数
- 允许声明重载函数、带默认形参值的函数

#### 内联成员函数

- 对于较简单的成员函数可声明为内联函数
- 不可有较复杂结构（循环、switch等）

### 类中成员访问方式

- 类内互访
- 类外访问：使用`对象名.成员名`  <!--是对象名--> //成员名可数据可函数

## 对象

类的对象就是类类型的变量

声明形式：`类名  对象名;` 

## 构造函数与析构函数

### 构造函数

- 其将对象初始化为一个特定的状态;在对象创建时由系统自动调用
- **构造函数名为类名**,并且没有返回类型
- 无参数的构造函数为默认构造函数（若未声明，则自动产生默认形式的构造函数;在创建对象时，会自动调用默认的构造函数）
- 如果定义了带参数的构造函数，则编译器不会再提供默认的无参构造函数。
- 带参数的默认值的构造函数中**默认参数应该在函数声明中指定，而不是在定义中**

```cpp
class Clock 
{
	Clock(){}//不带参数的默认函数    
    Clock(){Hour = 12; Min = 3; Sec = 12;}    
    Clock(int NewH,int NewM,int NewS){Hour = NewH; Min = NewM; Sec = NewS;}//带参数的构造函数
    Clock(int NewH,int NewM,int NewS);//定义默认参数的构造函数。！！会有问题！！
};
```

```cpp
class Example {
public:
    // 构造函数
    Example()
    {
        x = 0;
        y = 0;
    }
    // 其他成员函数
private:
    int x, y;
};

```

```cpp
Clock::Clock(int NewH,int NewM,int NewS) : Hour(NewH),Min(NewM),Sec(NewS)//写需要初始化的数据成员，等价于赋值行为
{}
```

#### 拷贝构造函数

C++中的拷贝构造函数是一种特殊类型的构造函数，用于从一个已有对象创建一个新的对象。当使用赋值操作符或将一个对象作为函数参数传递时，拷贝构造函数会被自动调用。它的语法形式如下：

```cpp
class Example {
public:
    // 拷贝构造函数
    Example(const Example& other)
    7{
        x = other.x;
        y = other.y;
    }
    // 其他成员函数
private:
    int x, y;
};
```

在这个例子中，Example类定义了一个拷贝构造函数，它将创建一个新对象，并将其初始化为另一个Example对象的值。拷贝构造函数的参数是一个常量引用，指向将要被拷贝的对象。在拷贝构造函数的函数体中，我们将另一个对象的x和y成员变量的值分别拷贝到新对象的x和y成员变量中。

需要注意的是，拷贝构造函数应该接受一个const引用参数，而不是一个值参数。这是因为如果使用值参数，将会递归地调用拷贝构造函数，从而导致无限循环。此外，拷贝构造函数应该将参数声明为const

##### 调用拷贝构造函数的不同情况

1. 当用一个对象去初始化同类型的另一个对象时，拷贝构造函数会被调用。例如：

   ```cpp
   MyClass obj1; // 创建一个MyClass对象
   MyClass obj2(obj1); // 用obj1初始化obj2，调用拷贝构造函数
   ```

2. 当将一个对象作为函数参数传递给函数时，拷贝构造函数会被调用。例如：

```cpp
void func(MyClass obj); // 函数定义
MyClass obj1; // 创建一个MyClass对象
func(obj1); // 将obj1作为参数传递给func函数，调用拷贝构造函数   
```

3.当函数返回一个对象时，拷贝构造函数会被调用。例如：

```cpp
MyClass func(); // 函数定义
MyClass obj1 = func(); // 调用func函数返回一个MyClass对象，调用拷贝构造函数
```

4.当创建一个对象数组时，拷贝构造函数会被调用。例如：

```cpp
MyClass obj1; // 创建一个MyClass对象
MyClass objArr[3] = { obj1, obj1, obj1 }; // 创建一个MyClass对象数组，调用拷贝构造函数
```

##### 浅拷贝与深拷贝

1. 浅拷贝：**实现对象间数据元素的一一对应复制**

浅拷贝是指将一个对象的值复制到另一个对象中，但是**两个对象共享相同的内存地址**。在浅拷贝中，如果原对象被销毁或修改，则会影响到拷贝对象。C++默认提供的拷贝构造函数是浅拷贝的。例如，下面是一个浅拷贝的例子：

```c++
#include <iostream>
using namespace std;

class MyClass 
{
public:
  int* data;//!!!!!!
  MyClass(int d) {
    data = new int(d);//!!!
  }
  ~MyClass() {
    delete data;
  }
  void display() {
    cout << "Data is: " << *data << endl;
  }
};

int main() {
  MyClass obj1(10);
  MyClass obj2(obj1);

  obj1.display(); // Output: Data is: 10
  obj2.display(); // Output: Data is: 10

  // Modify obj1's data
  *obj1.data = 20;

  obj1.display(); // Output: Data is: 20
  obj2.display(); // Output: Data is: 20

  return 0;
}
```

在这个例子中，我们定义了一个名为`MyClass`的类，它有一个`int`型成员data。我们使用`new`运算符在堆内存中分配了一个int型变量，并将其地址存储在data中。在我们的主函数中，我们使用obj1创建了一个`MyClass`对象，并将其data成员设置为10。然后我们使用obj2创建了另一个`MyClass`对象，并将其初始化为obj1的副本。由于默认拷贝构造函数是浅拷贝的，因此obj1和obj2共享相同的data成员。

当我们修改obj1的data成员时，obj2的data成员也会被修改。这是因为它们共享相同的内存地址。因此，浅拷贝可能会导致不可预期的行为，因此需要使用深拷贝。

1. 深拷贝

深拷贝是指将一个对象的值复制到另一个对象中，但是两个对象不共享相同的内存地址。在深拷贝中，如果原对象被销毁或修改，不会影响到拷贝对象。为了实现深拷贝，我们需要手动编写拷贝构造函数，以确保对象的所有成员都被正确地复制。例如，下面是一个深拷贝的例子：

```c++
#include <iostream>
using namespace std;

class MyClass {
public:
  int* data;
  MyClass(int d) {
    data = new int(d);
  }
  MyClass(const MyClass& other) {
    data = new int(*other.data);
  }
  ~MyClass() {
    delete data;
  }
  void display() {
    cout << "Data is: " << *data << endl;
  }
};

int main() {
  MyClass obj1(10);
  MyClass obj2(obj1);

  obj1.display(); // Output: Data is: 10
  obj2.display(); // Output: Data is: 10

  // Modify obj1's data
  *obj1.data = 20;

  obj1.display(); // Output: Data is: 20
  obj2.display(); // Output: Data is: 10

  return 0;
}
```

在这个例子中，我们手动编写了拷贝构造函数，以确保对象的data成员被正确地复制。当我们修改obj1的data成员时，obj2的data成员不会被修改，因为它们不共享相同的内存地址。

### 析构函数

除了构造函数，C++中还有另一种特殊类型的成员函数，称为析构函数。析构函数与构造函数相反，它们在对象被销毁时自动调用，用于清理对象所使用的资源。例如，如果一个对象分配了内存或打开了文件，那么在该对象被销毁时，析构函数可以释放内存或关闭文件。析构函数的语法与构造函数非常相似，只是在名称前加上了一个波浪号(~)



```cpp
class Example {
public:
    Example() {
        x = 0;
        y = 0;
    }
    ~Example() {
        // 在此清理资源
    }
private:
    int x, y;
};
```

## 类的组合

类中的成员数据包含另外一个类的对象

```cpp
class line
{
    private:
    point p1, p2;//两端点
    char color;
    public:
    line(point i, point j, char c);
    line(line &l);
    void draw(void);//画出线段
    float length(point p1, p2);
    
};
```

定义形式：

```cpp
class ClassA
{
private:
    ClassB classb;
};

class ClassB
{
};
//先定义A，再定义B
```

在上述示例中，类`ClassA`中定义了一个`ClassB`的实例变量`classb`，从而实现了`ClassA`和`ClassB`之间的关联。可以通过以下方式来访问`ClassB`的成员函数和成员变量：

```cpp
ClassA a;
a.classb.method();  // 调用ClassB的成员函数
a.classb.attribute; // 访问ClassB的成员变量

```

### 类的组合的构造函数

- 调用顺序是按照成员变量在类中的定义顺序进行的。注意：内嵌对象在构造函数的初始化列表中出现的顺序与内嵌对象构造函数的调用顺序无关
- 在组合中，先调用被组合类的构造函数，然后才调用包含该类的构造函数。
- 注意：若B没有默认构造函数，那么在A的构造函数中必须显式地调用B的构造函数来初始化b

必须在初始化列表中进行初始化的数据成员

1. 没有默认构造函数的内嵌对象：必须为该对象提供参数
2. 内嵌对象有默认构造函数
3. 引用类型的数据成员：必须在初始化时绑定引用的成员

### 拷贝构造函数

### 补

在C++中，**匿名对象**是没有命名的临时对象，**可以在不使用变量名的情况下直接创建和使用**。它们通常用于一次性的操作，例如将它们传递给函数或方法中，而不必在程序中创建变量来持有它们。匿名对象可以在语句中创建，例如：

```c++
myFunc(MyClass()); // 创建一个匿名的MyClass对象并传递给myFunc函数
```

在这个例子中，我们创建了一个匿名的MyClass对象，并将它作为参数传递给myFunc函数。**一旦myFunc函数返回，这个匿名对象就会被销毁**，因为它没有被分配给任何变量来持有它。

需要注意的是，匿名对象可以引起一些问题，因为它们没有名称，所以你不能在程序中引用它们。此外，如果你尝试将匿名对象作为参数传递给一个函数或方法，你必须保证该函数或方法不会尝试持有该对象的指针或引用，因为一旦函数或方法返回，该匿名对象就会被销毁。



# 数据共享与保护

## 标识符的作用域与可见性

### 作用域

1. 函数原型的作用域：声明时形参的作用范围就是函数原型的作用域(仅在括号内)
2. 全局作用域：在所有函数和代码块之外声明的变量具有全局作用域，它们可以被程序中的任何函数访问。全局变量在程序开始时被创建，在程序结束时被销毁。全局变量的生命周期与程序生命周期相同。
3. 局部作用域：在函数内部声明的变量具有局部作用域，它们只能在函数内部访问。局部变量在函数每次被调用时被创建，在函数执行完后被销毁。局部变量的生命周期与函数调用次数有关。
4. 块作用域（一对大括号内的就是'块'）：在代码块内部声明的变量具有块作用域，它们只能在代码块内部访问。块作用域变量在代码块每次被执行时被创建，在代码块执行完后被销毁。
5. 类作用域：
   若在类X中的成员m且成员函数中没有声明同名变量，则可以在这个函数内访问成员m(通过`X.m`或者`X::m`或者`ptr->m`访问成员m)
6. 命名空间作用域：在命名空间内部声明的变量具有命名空间作用域，它们只能在命名空间内部访问。命名空间作用域变量在命名空间被定义时被创建，在命名空间被销毁时被销毁。具有命名空间作用域的变量也称为全局变量
7. 文件作用域：在文件内部声明的变量具有文件作用域，它们可以被文件内的所有函数访问。文件作用域变量在文件被打开时被创建，在文件被关闭时被销毁

### 可见性

- 可见性是指在程序的某个地方是否是有效的，是否能够被引用被访问。
- 在大多数时候，变量作用域与可见性是一致。但是两者的主要区别就在于能否被直接引用。一个变量可以有不同的作用域，但是在不同的作用域中可能有不同的可见性，比如在C++的基类和派生类中，派生类并不能直接访问基类的私有成员，这时候私有成员在派生类中是不可见的。但是，派生类可以通过共有成员函数访问基类的私有成员，所以基类的私有成员的作用域同时包括了基类和其派生类。

#### 常见的三种可见性类型

- public表示这个类的成员变量和成员函数都可以被任何人访问
- private
- protected的开放程度要略高于private，但是略低于public，它表示这个类本身和它的子类，都可以访问和使用protected，但是除了这个类自己和它的子类，其他都不可以。

#### 作用域可见性的一般规则

1. 标识符要声明在前，引用在后
2. 同一作用域中，不能声明同名的标识符
3. 在没有互相包含关系的不同的作用域中声明的同名标识符，互不影响
4. 若在两个或多个具有包含关系的作用域中声明了同名标识符，则外层标识符在内层不可见

## 对象的生存期

### 静态生存期

- 静态生存期：对象的生存期和程序的运行期相同。

- 具有静态生存期的对象包括
             在命名空间作用域中声明的对象和在局部作用域中使用关键字static声明的对象。
- **当函数（局部作用域）中的变量采用static修饰时，该变量不会在每次调用后被销毁，也就是下一次调用该函数时依旧保存上一次调用的状态，同时该变量也不会在每次调用都被初始化**
- 当函数（局部作用域）中的变量采用static修饰时，该变量不会在每次调用后被销毁，也就是下一次调用该函数时依旧保存上一次调用的状态，同时该变量也不会在每次调用都被初始化

```c++
#include <iostream.h>
void fun();
int main()
{
    fun();
    fun();
}
void fun()
{
    static int a = 1;//a是动态生存期
    int i = 5;
    a++;
    i++;
    cout <<"i=" <<i <<"a=" <<a;
    //输出结果为：i=6 a=2  i=6 a=3
}
```



### 动态生存期

当函数（局部作用域）中的变量采用static修饰时，该变量不会在每次调用后被销毁，也就是下一次调用该函数时依旧保存上一次调用的状态，同时该变量也不会在每次调用都被初始化

## 静态成员

### 静态数据成员

静态数据成员在**类内声明，在类外定义**，与类的其他成员函数一样，可以是public、private或protected。静态数据成员是属于类的，不是属于对象的，也就是说，无论创建多少个对象，静态数据成员只有一个副本，**被所有的对象共享**。静态数据成员的初始化必须在类外进行。

```c++
#include <iostream>
using namespace std;
class Person
{
public:
    static int age;
    Person()
    {
        count++;
    }
    static void getCount()
    {
        cout<<"Person count:"<<count<<endl;
    }
private:
    static int count;
};
//静态数据成员可以被所有的对象共享，因此静态数据成员的值可以被所有的对象访问和修改。同时，静态数据成员也可以被类的成员函数访问和修改。
int Person::age = 0;
int Person::count = 0;
//需要注意的是，在类中声明静态数据成员只是声明，而不是定义。因此，在类外必须对静态数据成员进行定义，并且不需要使用static关键字。
int main()
{
    cout<<Person::age<<endl;
    Person p1;
    Person::getCount();
    Person p2;
    Person::getCount();
    //getCount函数就是一个静态成员函数，它可以访问静态成员变量count。静态成员函数没有this指针，因此不能访问非静态成员。需要使用类名和作用域解析符号::来访问静态数据成员和静态成员函数。
    return 0;
}
//age是Person类的静态数据成员，count是Person类的静态成员变量，它们都被初始化为0。由于age是静态数据成员，所以可以使用Person::age来访问它。在main函数中，先输出了age的值，然后创建了两个Person对象，每创建一个对象，count就加1，最后调用了getCount函数来输出对象的数量。
```

### 静态函数成员

- 静态函数成员是属于类的，而不是属于对象的函数成员。静态函数成员可以通过**类名**和作用域解析符号::来调用，**不需要创建类的对象。**
- 静态函数成员，可以直接访问静态成员变量和静态成员函数。而访问非静态成员，必须通过对象名。
- 静态函数成员通常用来处理和类有关的任务，而不是对象的任务

```c++
#include <iostream>
using namespace std;
class Person{
public:
    static int age;
    Person(){
        count++;
    }
    static void getCount(){
        cout<<"Person count:"<<count<<endl;
    }
private:
    static int count;
};
int Person::age = 0;
int Person::count = 0;
int main(){
    Person::getCount();
    Person p1;
    Person::getCount();
    Person p2;
    Person::getCount();
    return 0;
}
```

需要注意的是，静态函数成员不能被声明为`const、volatile和virtual`，因为静态函数成员没有`this`指针，而`const、volatile和virtual`都需要`this`指针。另外，静态函数成员也不能被声明为`friend`，因为`friend`关键字只能用于非静态成员函数。

## 类的友元

友元关系提供了不同类或对象的成员函数之间、类的成员函数之间与一般函数之间进行数据共享的机制

### 友元函数

- 友元函数可以是非成员函数，也可以是其他类的成员函数。
- 但可以访问类的私有成员。友元函数可以在类定义内部或外部进行声明，但**必须在类外部进行定义**。
- **友元函数可以访问类的私有成员**

```c++
#include <iostream>
using namespace std;
class Person
{
public:
    Person(int age)
    {
        this->age = age;
    }
    friend void getAge(Person p);//友元函数在声明时必须在函数名前加上关键字friend
private:
    int age;
};
void getAge(Person p)
{
    cout<<"Person age:"<<p.age<<endl;
}
int main()
{
    Person p(18);
    getAge(p);
    return 0;
}
```

### 友元类

- 实现类之间的数据共享。
- 若A类为B类的友元类，则A的所有成员函数都是B的友元函数，都可以访问B的私有和保护成员
- 友元关系是**单向的且不能传递**、不能继承

```C++
class A
{
    public:
    	void display()
        {
            cout << x << endl;
        }
    	int getX()
        {
            return x;
        }
    	friend class B;  // B是A的友元类
    //其他成员略
    private:
    	int x;
};
class B
{
    public:
    	void set(int i); 
        void display();
    private:
    	A a;
};
void B::set(int i)
{
    a.x = i;  // 由于B是A的友元，所以在B中可以访问A类对象的私有成员
}
```



## 常类型

### 常对象

1. 常对象必须进行初始化，而且不能被更新
2. 语法形式： `const 类型说明符 对象名`
3. 不能通过常对象调用普通的成员函数

```c++
class MyClass {
    // class definition
};

const MyClass obj; // 常对象
```



指针类型的常对象可以有两种声明方式：指针本身不是常量，但指向的对象是常量。这意味着指针可以被重新赋值，但不能用来修改指向的常量对象。

```c++
const int *ptr1;   // ptr1是指向常量整数的指针
int const *ptr2;   // ptr2是指向常量整数的指针，与ptr1等效
```

### 用`const`修饰的类成员

#### 类成员函数

`类型说明符 函数名（参数表）const ;`  /   `类型说明符 函数名（参数表）const {}`

<u>**在`main`中调用函数时不需要再标出`const`**</u>

1. `const`是函数类型的一个组成部分，函数的定义部分也应有`const`关键字
2. 通过一个常对象，只能常成员函数
3. 常成员函数不能更新目的对象的数据成员
4. `const`关键字可用于区分重载函数

```c++
//例如：
void print();
void print() const;
```

#### 常数据成员

构造函数时对该数据成员进行初始化，**<u>只能通过初始化列表</u>**

```c++
class MyClass {
public:
    MyClass(int x, int y) : const_member(x), nonconst_member(y) {}
private:
    const int const_member;     // 常数据成员
    int nonconst_member;        // 非常数据成员
};
```



```c++
class MyClass {
public:
    MyClass(int value) : const_member(value) {}
    int get_const_member() const 
    { 
        return const_member; 
    } // 常成员函数
private:
    const int const_member; // const成员变量
};
```

#### 常引用

1. 非常引用只能绑定普通对象
2. 常引用能绑定普通对象，也能绑定常对象
3. 常引用**引用的对象**不能被更新
   `const 类型说明符 &引用名`

#### 常数组

`类型说明符 const 数组名[大小]`

## 多文件结构和编译预处理命令

### 编译预处理命令

C++编译预处理命令是在源代码被编译之前对源代码进行预处理的一组命令。

1. \#include：用于包含头文件。

   `#include <文件名>`：标准方式搜索   /   `#iinclude "文件名"`：首先在文件目录中搜索，若没有，再按照标准方式寻找
   例如：

```c++
#include <iostream>  // 这个命令会将iostream头文件包含到源代码中。
```

   2.\#define：用于定义宏。例如：

```3c++
#define PI 3.14159  //这个命令将宏PI定义为3.14159。
```

   3.`#undef`  删除先前定义的宏

   4.`#if / #else / #elif / #endif`：用于条件编译。例如：

```c++
#if defined(_WIN32)
    // Windows-specific code here
#elif defined(__linux__)
    // Linux-specific code here
#else
    // Other operating systems code here
#endif
```

这个命令根据不同的条件选择不同的代码块进行编译。

​     5.\#pragma：用于向编译器传递特定的指令。例如：

```c++
#pragma warning(disable : 4996)
```

这个命令用于禁用编译器对指定警告的显示。

这些预处理命令可以在源代码中灵活使用，帮助程序员进行代码的组织和调试，提高代码的可读性和可维护性。

### 多文件结构

通常，一个C++程序可以被拆分为多个文件，例如：

1. 头文件（.h或.hpp文件）：包含类的声明、常量、函数原型等。
2. 源文件（.cpp文件）：包含类的实现、函数的定义等。
3. 主函数文件（.cpp文件）：包含程序入口函数main的定义。

一个头文件可以被多个源文件包含，这样就可以实现**多个源文件共享同一个类或函数的定义**。在源文件中，需要使用#include命令将需要的头文件包含进来。例如，如果有一个头文件MyClass.h，包含了MyClass类的声明，那么在源文件中需要这样包含它：

```c++
#include "MyClass.h"
```

**注意，在包含头文件时使用双引号" "而不是尖括号< >，这样可以告诉编译器在当前目录下查找头文件。**

**当多个源文件中包含同一个头文件时，会导致头文件被多次包含。这种情况下，可以使用头文件保护宏（header guard）来防止重复包含**，例如：

```c++
#ifndef MYCLASS_H
#define MYCLASS_H
// header file contents here
#endif
```

这样，当第一个源文件包含MyClass.h时，MYCLASS_H会被定义，当第二个源文件再次包含MyClass.h时，MYCLASS_H已经被定义，就不会再次包含MyClass.h了。

# 数组、指针与字符串

## 指针

### 初始化

`存储类型 数据类型 * 指针名 = 初始地址` **一定是地址值**

```c++
int i = 0;
int * ptr = &i;
```

- 可以把0赋值给指针变量，表示空指针
- 指针的类型是它所指向的变量的类型
- 允许声明指向void类型的指针，它后续可以被赋予任何类型

### 指向常量的指针

不可通过指针来改变所指对象的值；但指针本身可变，可以指向其他的对象

```c++
const char * name = "john";
char s[] = "my";
*name = "my";  // wrong
name = s; //right
```

### 指针常量

指针本身的值不可被改变，但是可以改变其所指向的值

```c++
```

### 指向数组元素的指针

```c++
int a[10];
int * pa = NULL;
pa = a; // 或 pa = &a[0]
//a[i] / *(pa+i) / *(a+i) / pa[i]   均为等价
```

**不能写`a++` 因为a是数组首地址，是常量**

### 指针数组

```c++
int * ptr[10]; //数组的元素是指针
```

### 对象指针

`类名 * 对象指针名 `

访问成员：`对象指针名 -> 成员名`

### this指针

1. 隐含于每一个类中的**非静态成员函数**中的特殊指针，指向正在被成员函数操作的对象，是**指针常量**
2. 可以用来区分同名的局部变量和成员变量
3. 当调用成员函数时，编译器**会自动向该函数传递当前对象的地址作为参数**，而这个地址就是this指针所指向的地址。

```c++
#include <iostream>
using namespace std
class Point {
public:
    Point(int x, int y) {
        this->x = x;
        this->y = y;
    }
    int getX() {
        return this->x;
    }
    int getY() {
        return this->y;
    }
    void setX(int x) {
        this->x = x;
    }
    void setY(int y) {
        this->y = y;
    }
private:
    int x;
    int y;
};
//
int main() {
    Point p(1, 2);
    p.setX(3);
    cout << p.getX() << "," << p.getY() << endl;
    return 0;
}
```

```c++
Point& setX(int x) {
    this->x = x;
    return *this;
}
//this指针也可以用于返回当前对象本身
```

## 动态存储分配

### 动态申请内存

动态申请内存是在程序运行时**动态地分配内存空间**。在C++中，动态申请内存需要**使用`new`运算符**来完成，其基本语法为：

```c++
指针变量 = new 数据类型;
```

其中，指针变量是指向数据类型的指针，`new`运算符用于在堆内存中动态分配一块空间，**返回分配空间的首地址**，将其赋值给指针变量。
若分配失败，则返回的地址是`NULL` 

例如，动态申请一个整型变量的内存空间可以这样实现：

```c++
int* p = new int;
int* p = new int (初始值); // ()内内容可以给*p 赋初始值
```

如果需要动态申请一个数组，则可以这样实现：

```c++
int* p = new int[数组大小]; //[]内一定有数值
//可在[]后加()，但不能带参数
//若不加（），对每个数组元素的初始化与执行new T 时初始化的方式相同
//若加（），对每个数组元素的初始化与执行new T() 时初始化的方式相同
int* p = new int[数组大小] ();
```

```c++
class Point {};
Point *q = new Point[2] ();
```



在使用完动态申请的内存后，需**要使用`delete`运算符释放**所申请的空间，避免内存泄漏，其基本语法为：

```c++
delete 指针变量;
delete[] 指针变量; //释放动态申请的数组
```

需要注意的是，在释放动态申请的内存空间后，应该将指针变量置为空指针，避免产生悬挂指针的问题：

```c++
int* p = new int;
// 使用p指向的内存空间
delete p;
p = NULL; // 将指针变量置为空指针
```

```c++
// 动态创建对象！
#include <iostream>
using namespace std;

class MyClass {
  int data;
public:
  MyClass(int d) : data(d) {}
  void display() {
    cout << "Data is: " << data << endl;
  }
};

int main() {
  // Dynamically allocating memory using new
  MyClass* obj = new MyClass(10);

  // Calling member function using pointer
  obj->display();

  // Deleting object created using new
  delete obj;

  return 0;
}

```

### 动态存储函数

```c++
void free()
```

### 动态数组类

```c++
#ifndef DYNINTS_H
#define DYNINTS_H

class DynInts {
private:
    const int capacity;//数组最大容量
    int count;//数组中实际有几个元素
    int *items;//指向动态分配的数组
    //bool modified;//数组是否改变,这个成员我感觉意义不大，不管了。
public:
    DynInts(int _cap): capacity(_cap), count(0), items(NULL) {}//构造函数，带一个参数，指定最大容量

    DynInts(const DynInts &a); //复制构造函数

    DynInts(int _cap, int *a, int n);
    //带三个参数的构造函数，第一个参数指定最大容量，
    //把第二个参数代表的数组（第三个参数是第二个参数数组的元素个数）复制进来，超出指定容量的话报错

    DynInts & operator =(const DynInts &a); //重载赋值运算符，不改动自身最大容量，赋值过来的数组若元素个数超出则报错。

    void push_back(int v);//在数组末尾添加一个元素

    ~DynInts() //析构
    {
        printf("析构函数调用\n");
        if (items) delete [] items;
    }

    int length() { return count;  }//返回元素个数

    int & operator [](int i) { return items[i]; }//根据下标访问元素

    void travel_by(void (*func)(int * data)); //遍历数组
};

#endif
```

# 继承与派生

## 类的继承与派生

C++中的类的继承与派生是面向对象编程的重要概念之一，它允许你创建一个新的类，该类可以继承一个或多个已有的类的特性和行为。继承与派生使得代码重用和扩展变得更加方便。

在C++中，使用关键字`class`来定义一个类的派生类（子类），语法如下：

```c++
class 派生类名 : 继承方式1 基类名1, 继承方式2 基类名2
{
    // 派生类的成员声明
};
```

派生类继承了基类的成员变量和成员函数，并可以在派生类中添加自己的成员变量和成员函数。访问修饰符指定了派生类对基类成员的访问权限，可以是`public`、`protected`或`private`。不同的访问修饰符决定了派生类对基类成员的可访问性。

派生类可以通过以下几种方式继承基类的成员：

1. **公有继承（public inheritance）**：派生类继承了基类的公有成员和保护成员，但不继承基类的私有成员。在公有继承中，基类的公有成员在派生类中仍然是公有的，保护成员在派生类中变为保护的。
2. **保护继承（protected inheritance）**：派生类继承了基类的公有成员和保护成员，但不继承基类的私有成员。在保护继承中，基类的公有成员和保护成员在派生类中都变为保护的。
3. **私有继承（private inheritance）**：派生类继承了基类的公有成员和保护成员，但不继承基类的私有成员。在私有继承中，基类的公有成员和保护成员在派生类中都变为私有的。

派生类可以覆盖（重写）基类的成员函数，即在派生类中重新定义一个与基类成员函数具有相同名称和参数列表的成员函数。使用`override`关键字可以显式地表示这是一个覆盖函数。派生类中的成员函数可以通过基类名和作用域解析运算符来访问基类的成员函数。

派生类还可以添加自己的成员函数和成员变量，以及重载基类的成员函数。

下面是一个示例代码，展示了一个基类`Shape`和两个派生类`Circle`和`Rectangle`的例子：

```c++
class Shape
{
public:
    void setColor(const string& color) {
        this->color = color;
    }

    string getColor() const {
        return color;
    }

    virtual double getArea() const = 0; // 纯虚函数，需要在派生类中实现

private:
    string color;
};

class Circle : public Shape //单继承
{
    //在Circle 类中实际上就有了Shape类中的除了构造和析构函数的所有成员，即为继承
public:
    Circle(double radius) : radius(radius) {}

    double getArea() const override {
        return 3.14 * radius * radius;
    }
    //getArea（）即为新增部分

private:
    double radius;
};

class Rectangle : public Shape //单继承
{
public:
    Rectangle(double width, double height) : width(width), height(height) {}

    double getArea() const override {
        return width * height;
    }

private:
    double width;
    double height;
};

```

在上面的示例中，`Shape`是基类，`Circle`和`Rectangle`是派生类。`Shape`类定义了一个公有函数`setColor`和`getColor`，以及一个纯虚函数`getArea`，需要在派生类中实现。

`Circle`类和`Rectangle`类分别继承了`Shape`类，并实现了纯虚函数`getArea`来计算圆和矩形的面积。派生类可以访问基类的公有成员函数`setColor`和`getColor`。

在使用继承与派生时，可以通过基类的指针或引用来操作派生类的对象，实现多态性，即在编译时不确定调用的是基类还是派生类的成员函数。例如：

```c++
int main() {
    Circle c(5);
    Rectangle r(4, 6);

    Shape* shape1 = &c;
    Shape* shape2 = &r;

    cout << "Circle area: " << shape1->getArea() << endl; // 输出圆的面积
    cout << "Rectangle area: " << shape2->getArea() << endl; // 输出矩形的面积

    return 0;
}
```

在上面的示例中，通过基类指针`shape1`和`shape2`来操作派生类`Circle`和`Rectangle`的对象，实现了多态性。

## 访问与继承

下面详细介绍派生类对基类成员的访问权限：

1. **公有继承（public inheritance）**：在公有继承中，基类的公有成员和保护成员在派生类中仍然是公有或保护的，派生类可以直接访问基类的公有成员和保护成员。**私有成员在派生类中不可直接访问**。
2. **保护继承（protected inheritance）**：在保护继承中，基类的公有成员和保护成员在派生类中变为保护的，派生类可以直接访问基类的保护成员，但对外部用户不可见。私有成员在派生类中不可直接访问。
3. **私有继承（private inheritance）**：在私有继承中，**基类的公有成员和保护成员在派生类中变为私有的**，派生类可以直接访问基类的私有成员，但对外部用户不可见 ( 变为不可直接访问的 ) 。

### 公有继承

```c++
#include <iostream>
#include <string>
using namespace std;

class Shape 
{
public:
    void setColor(const string& color) {
        this->color = color;
    }

    string getColor() const {
        return color;
    }

protected:
    double area; // 基类的保护成员

private:
    string color; // 基类的私有成员
};

class Circle : public Shape 
{
public:
    void setRadius(double radius) {
        this->radius = radius;
    }

    double getArea() const {
        return 3.14 * radius * radius;
    }

private:
    double radius;
};

int main() {
    Circle c;
    c.setColor("Red");  //!!!
    c.setRadius(5.0); //!!!

    cout << "Circle color: " << c.getColor() << endl;
    cout << "Circle area: " << c.getArea() << endl;

    return 0;
}
```

### 私有继承

```c++
//课本上的示例更好'
#include <iostream>
#include <string>
using namespace std;

class Shape {
public:
    void setColor(const string& color) {
        this->color = color;
    }

    string getColor() const {
        return color;
    }

protected:
    double area; // 基类的保护成员

private:
    string color; // 基类的私有成员
};

class Circle : private Shape {
public:
    void setRadius(double radius) {
        this->radius = radius;
    }

    double getArea() const {
        return 3.14 * radius * radius;
    }

    using Shape::setColor; // 通过 using 声明使基类的 setColor() 在派生类中可见

private:
    double radius;
};

int main() {
    Circle c;
    c.setColor("Red"); // 通过 using 声明后，可以在派生类中访问基类的公有成员函数
    c.setRadius(5.0);

    cout << "Circle color: " << c.getColor() << endl;
    cout << "Circle area: " << c.getArea() << endl;

    return 0;
}
```

在上面的示例中，`Circle` 类使用私有继承 `private Shape`，这意味着基类 `Shape` 的公有和保护成员在派生类中都变为私有成员。为了在派生类中仍然可以访问基类的公有成员函数 `setColor`，使用 `using` 声明使其可见。

私有继承意味着派生类对象可以访问基类的公有和保护成员，但不能直接访问基类的私有成员。在私有继承的情况下，从基类继承的公有和保护成员将成为派生类的私有成员，因此只能通过派生类对象的成员函数或友元函数来访问这些成员。
以下是一个示例程序，演示了如何从派生类中访问从基类继承的成员：

```c++
#include <iostream>
using namespace std;

class Base {
public:
    int public_data;
protected:
    int protected_data;
private:
    int private_data;
};

class Derived : private Base {
public:
    void func() {
        // 可以访问从基类继承的公有成员
        public_data = 1;

        // 可以访问从基类继承的保护成员
        protected_data = 2;

        // 不能直接访问从基类继承的私有成员
        // private_data = 3;

        // 可以通过基类的公有成员函数来访问私有成员
        // private_data = get_private_data();
    }

    // 可以定义公有成员函数来访问基类的私有成员
    int get_private_data() {
        return Base::private_data;
    }
};

int main() {
    Derived obj;
    obj.func();
    return 0;
}
```

### 构造函数

```c++
派生类名::派生类名（基类所需的形参,本类成员所需的形参）: 基类名(参数表)
{
    本类成员的初始化赋值语句
}
```

继承中的构造和析构顺序：**先调用父类构造函数，再调用子类构造函数；析构顺序与构造顺相反**

### 继承中同名成员的处理方式

#### 非静态同名成员的处理

1. 子类中的成员可以直接进行调用；想通过子类对象访问父类中同名成员，需要加上父类的作用域  `子类对象名.父类名::成员`
2. 函数处理：直接调用，调用的是子类中的；父类**`子类对象名.父类名::成员函数`**
3. 成员函数如果子类中出现与父类同名的成员函数，子类的同名成员会隐藏掉父类中所有的同名。如果想要访问到父类中被隐藏的同名成员函数，需要加作用域

#### 静态同名成员的处理

1. 静态成员属性
   1. 通过对象访问：与非静态成员的处理方法相同
   2. 通过类名访问：访问父类`子类名::父类名::成员名` 
2. 静态成员函数
   1. 通过对象访问：`子类对象名.父类名::成员函数`
   2. 通过类名访问：访问父类`子类名::父类名::成员函数`

当父类中出现同名成员，需要加作用域进行区分

### 菱形继承

在C++的菱形继承中，子类得到的数值来源于最远的基类。假设有一个类A，它是类B和类C的基类，而类D是类B和类C的派生类。如果类B和类C都定义了一个名为"num"的成员变量，并且类D没有重新定义它，**那么在类D中访问"num"时，它将使用类A中的成员变量。**这是因为**类A是最远的基类**，而类B和类C都从类A继承了它们的"num"成员变量。**如果类D重新定义了"num"，则它将使用类D中的成员变量。**

定义：两个派生类继承同一个基类，又有某个类同时继承两个派生类

问题：

1. 父类具有相同的数据，容易对最后的类造成二义性
2. 有一份数据即可，但是会导致有两份

```c++
class animal{};
class sheep : virtual public animal {};
class tuo : virtual public animal {};
class sheeptuo : public sheep , public tuo {};
//利用虚继承，解决第二个问题:继承之前加上virtual
```

```c++
class Base {
public:
    int x;
};

class Derived1 : virtual public Base {
public:
    // ...
};

class Derived2 : virtual public Base {
public:
    // ...
};

class Derived3 : public Derived1, public Derived2 {
public:
    // ...
};
```

### 类型兼容规则：

1. 派生类对象可以隐式地转换为基类对象：可以将派生类的对象赋值给基类对象，这是一种向上转型（upcasting）的操作。例如，如果有一个派生类`Derived`和一个基类`Base`，可以将`Derived`对象赋值给`Base`对象。

2. 派生类的指针可以隐式地转换为基类的指针：可以将派生类的指针赋值给指向基类的指针，这同样是一种向上转型的操作。例如，如果有一个指向派生类对象的指针`Derived* derivedPtr`，可以将其赋值给指向基类的指针`Base* basePtr`。

3. 派生类的引用可以隐式地转换为基类的引用：可以将派生类的引用绑定到基类的引用，同样是一种向上转型的操作。例如，如果有一个派生类对象的引用`Derived& derivedRef`，可以将其绑定到基类的引用`Base& baseRef`。

4. 可以通过基类指针或引用调用派生类的虚函数：如果基类中定义了虚函数，并且派生类进行了函数重写（override），那么可以通过基类的指针或引用调用派生类的虚函数。在运行时，将根据指针或引用所指向的对象的实际类型来调用相应的函数。

需要注意的是，通过基类指针或引用调用派生类特有的成员或函数是不允许的，因为基类指针或引用只能访问基类中定义的成员和函数。

这些类型兼容规则使得在继承与派生的体系中可以进行多态性的操作，实现了对象的抽象和通用性。

### 代码中的小问题

```c++
//知识点：在构造类时，会先调用基类的构造函数，然后调用派生类的构造函数

// chatgpt 的修正意见
// 这段代码在语法上没有明显的错误，但存在一些设计上的问题：

// 1. 构造函数没有使用成员初始化列表：在类的构造函数中，最好使用成员初始化列表来初始化成员变量，而不是在构造函数体内进行赋值操作。这样可以提高效率并避免不必要的赋值操作。

// 2. 没有使用虚析构函数：基类`vehicle`应该定义一个虚析构函数，以便在通过基类指针删除派生类对象时，能够正确调用派生类的析构函数。


// 4. 缺少访问控制修饰符：基类`vehicle`中的成员变量和成员函数都没有指定访问控制修饰符（如`public`、`private`和`protected`）。默认情况下，类中的成员是私有的，应根据需要添加适当的访问控制修饰符。

// 这些问题不一定导致代码无法编译或运行，但可能影响代码的可读性、维护性和扩展性。在设计和实现类的继承关系时，需要仔细考虑这些因素，并遵循良好的面向对象设计原则。


// 多次构造输出：
// 在派生类的构造函数中，会隐式调用基类的默认构造函数，所以在输出语句中会显示多次"The vehicle has been constructed"
//。为避免重复输出，您可以在派生类的构造函数中使用成员初始化列表来调用基类的特定构造函数。
```



# 多态

- 静态多态：编译阶段确定函数地址：函数重载或者运算符重载
- 动态多态：运行阶段确定函数地址：派生类和虚函数实现运行时多态

动态多态的条件：

1. 有继承关系
2. 子类要重写父类中的虚函数(函数返回值类型、函数名、参数列表完全相同)

动态多态的使用：父类的引用或者指针指向子类对象

## 运算符重载

1. 重载为类成员函数时，参数个数=原操作数-1（后置++及--除外）
2. 重载为友元函数时，参数个数=原操作数个数，且至少应有一个自定义类型的形参

运算符重载通过定义特定的**成员函数或全局函数**来实现。重载运算符的函数名称以**关键字 `operator` 开头**，**后跟要重载的运算符符号**。

以下是一些常见的运算符及其对应的重载形式：

1. 一元运算符重载：可以重载一元运算符，例如取反运算符 `!`、递增运算符 `++`、递减运算符 `--` 等。

```c++
返回类型 operator运算符 (参数列表); // 成员函数形式
返回类型 operator运算符 (参数列表); // 全局函数形式
```

1. 二元运算符重载：可以重载二元运算符，例如算术运算符 `+`、`-`、`*`、`/`、比较运算符 `==`、`!=`、`<`、`>` 等。

```c++
返回类型 operator运算符 (参数列表); // 成员函数形式
返回类型 operator运算符 (参数列表); // 全局函数形式
```

1. 赋值运算符重载：可以重载赋值运算符 `=`，用于自定义类型对象的赋值操作。

```c++
返回类型 operator= (参数列表); // 成员函数形式
```

1. 下标运算符重载：可以重载下标运算符 `[]`，用于类对象的索引访问操作。

```c++
返回类型 operator[] (参数列表); // 成员函数形式
```

1. 函数调用运算符重载：可以重载函数调用运算符 `()`，使对象可以像函数一样被调用。

```c++
返回类型 operator() (参数列表); // 成员函数形式
```

1. 输入/输出运算符重载：可以重载输入输出运算符 `<<` 和 `>>`，使对象可以使用流插入运算符 `<<` 和流提取运算符 `>>` 进行输入输出操作。

```c++
返回类型 operator<< (参数列表); // 全局函数形式，输出运算符重载
返回类型 operator>> (参数列表); // 全局函数形式，输入运算符重载
```

通过重载运算符，您可以为自定义类型提供与内置类型相似的行为，使其更直观和易于使用。但是请注意，运算符重载应该遵循适当的语义规则，以保持代码的可读性和一致性。

**运算符重载也可以实现函数重载**

在C++中，成员函数重载和全局函数重载有几个主要的区别：

1. 成员函数重载是在类中定义的，只能通过该类的对象或指针调用。而全局函数重载是在命名空间中定义的，可以直接调用或通过命名空间限定符调用。
2. 成员函数重载可以访问该类的私有成员，而全局函数重载不能访问类的私有成员。如果需要访问类的私有成员，可以通过友元函数或访问器函数来实现。
3. 成员函数重载可以被继承，而全局函数重载不能被继承。如果需要在派生类中重载一个全局函数，需要重新定义该函数。
4. 成员函数重载可以有虚函数，而全局函数重载不能有虚函数。虚函数可以实现多态性，允许通过基类指针或引用调用派生类的实现。

### 加号运算

- 通过成员函数重载
- 通过全局函数重载

加号运算符可以重载为执行不同类型的操作，取决于您要对自定义类型执行何种操作。以下是加号运算符重载的示例：

1. 对于两个自定义类型对象相加，可以将加号运算符重载为执行对象之间的加法操作。假设有一个名为 `MyClass` 的类：

```c++
class MyClass {
private:
    int value;
public:
    MyClass(int val) : value(val) {}
    MyClass operator+(const MyClass& other) //!!!
    {
        int sum = value + other.value;
        return MyClass(sum);
    }
};
```

通过重载 `+` 运算符，我们可以将两个 `MyClass` 对象相加：

```c++
MyClass obj1(5);
MyClass obj2(10);
MyClass result = obj1 + obj2;  // 调用重载的加号运算符(为调用的简化形式)
```

1. 对于自定义类型对象和内置类型数据相加，可以将加号运算符重载为执行对象和内置类型之间的加法操作。假设有一个名为 `MyClass` 的类：

```c++
class MyClass {
private:
    int value;
public:
    MyClass(int val) : value(val) {}
    MyClass operator+(int num) {
        int sum = value + num;
        return MyClass(sum);
    }
};
```

通过重载 `+` 运算符，我们可以将 `MyClass` 对象与整数相加：

```c++
MyClass obj(5);
MyClass result = obj + 10;  // 调用重载的加号运算符
```

注意：运算符重载可以**作为成员函数或全局函数**进行定义。以上示例是将重载函数定义为**成员函数，因此运算符左侧的对象将自动成为调用者**。如果您选择使用全局函数形式，则需要在函数声明中将对象作为参数传递。



### 左移运算符

左移运算符（<<）可以重载为执行自定义类型对象的输出操作。重载左移运算符**允许我们以自定义的方式将对象的数据输出到流中**。

**一般不会用成员函数来重载，只能用全局函数来重载左移运算符**，因为无法保证`cout << p`格式

```c++
#include <iostream>
using namespace std;

class MyClass {
    int x, y;
public:
    MyClass(int a, int b) {
        x = a;
        y = b;
    }
    friend ostream& operator<<(ostream& os, const MyClass& obj);
};

ostream& operator<<(ostream& os, const MyClass& obj) {
    os << "x: " << obj.x << " y: " << obj.y;
    return os;
}

int main() {
    MyClass obj(10, 20);
    cout << obj << endl;
    return 0;
}
```

### 递增运算符

递增运算符可以重载为执行自定义类型对象的递增操作。有两种方式可以重载递增运算符：前置递增和后置递增。

1. 前置递增运算符（++i）：

```c++
返回类型 operator++() {
    // 执行递增操作
    // 返回递增后的对象
}
```

```c++
class Counter {
    private:
        int count;
    public:
        Counter() : count(0) {}
        Counter(int c) : count(c) {}
        int getCount() { return count; }
        Counter& operator++() 
        {
            ++count;
            return *this;
        }
};
```



在这种情况下，递增操作在对象被使用之前发生。

   2.后置递增运算符（i++）：

```c++
返回类型 operator++(int) {
    // 保存当前对象的副本
    // 执行递增操作
    // 返回保存的副本
}
//int代表占位参数，用来区分前置与后置
```

在这种情况下，递增操作在对象被使用之后发生。

以下是递增运算符重载的示例：

```c++
class Counter {
private:
    int count;
public:
    Counter(int initialCount) : count(initialCount) {}
    
    // 前置递增运算符重载
    //返回一个引用，是为了一直对一个数据进行运算
    Counter& operator++() {
        ++count;
        return *this;
    }
    
    // 后置递增运算符重载
    Counter operator++(int) {
        Counter temp(count);
        ++count;
        return temp;
    }
    
    int getCount() const {
        return count;
    }
};

int main() {
    Counter c(5);
    
    // 前置递增运算符
    ++c;
    cout << c.getCount() << endl;  // 输出：6
    
    // 后置递增运算符
    Counter d = c++;
    cout << c.getCount() << endl;  // 输出：7
    cout << d.getCount() << endl;  // 输出：6
    
    return 0;
}
```

在上述示例中，`Counter` 类重载了前置递增运算符和后置递增运算符。通过重载，我们可以对 `Counter` 对象执行递增操作，并返回递增后的对象或递增前的对象（根据运算符的类型）。

### 关系运算符

在 C++ 中，可以通过函数重载来改变关系运算符的行为。下面是一些常见的关系运算符和它们的对应函数：

- `==` 重载为 `bool operator==(const MyClass& other)`
- `!=` 重载为 `bool operator!=(const MyClass& other)`
- `<` 重载为 `bool operator<(const MyClass& other)`
- `>` 重载为 `bool operator>(const MyClass& other)`
- `<=` 重载为 `bool operator<=(const MyClass& other)`
- `>=` 重载为 `bool operator>=(const MyClass& other)`

其中 `MyClass` 是你定义的类名，`other` 是另外一个对象。

下面是一个示例代码，演示如何重载 `<` 运算符：

```c++
class MyClass {
public:
    int value;
    MyClass(int value) : value(value) {}

    // 重载 < 运算符
    bool operator<(const MyClass& other) const 
    {
        return value < other.value;
    }
};

int main() {
    MyClass a(5);
    MyClass b(10);

    if (a < b) {
        cout << "a 小于 b" << endl;
    } else {
        cout << "a 大于等于 b" << endl;
    }

    return 0;
}
```

### 赋值运算符

```c++
class MyClass {
private:
    int value;
public:
    MyClass(int val) : value(val) {}
    int getValue() const { return value; }
    void setValue(int val) { value = val; }
    MyClass& operator=(const MyClass& other) {
        if (this != &other) {
            value = other.value;
        }
        return *this;
    }
};
//重载运算符需要返回一个引用，以便能够进行链式赋值操作。在这个示例中，我们检查了<自我赋值>的情况，并将值从另一个对象复制到当前对象。
```

### 函数调用运算符  ()

C++中，函数调用运算符可以被重载。这**使得一个类实例可以像函数一样被调用**。要重载函数调用运算符，可以在类中声明一个名为"operator()"的函数重载。

```c++
class MyClass 
{
public:
    int operator()(int arg1, int arg2) 
    {
        return arg1 + arg2;
    }
};

int main() 
{
    MyClass obj;
    int result = obj(1, 2); // 调用函数调用运算符重载
    return 0;
}
```

```c++
#include <iostream>
#include <string>
using namespace std;
class Point 
{
private:
    int x;
    int y;
public:
    //构造+析构
    Point()
    {
        cout << "Point has been created" << endl;
    }
    Point(int _x, int _y) : x(_x), y(_y)
    {
        cout << "Point has been created" << endl;
    }
    ~Point()
    {
        cout << "Point has been cleared" << endl;
    }
    //重载
    //重载<<
    friend ostream& operator<<(ostream& os, const Point & obj);
    //重载+
    Point operator + (Point &obj)
    {
        int sum_x = x + obj.x;
        int sum_y = y + obj.y;
        return Point(sum_x, sum_y);
    }
    //重载-
    Point operator - (Point &obj)
    {
        int sum_x = x - obj.x;
        int sum_y = y - obj.y;
        return Point(sum_x, sum_y);
    }
    //重载前置++
    Point operator ++ ()
    {
        (this->x)++;
        (this->y)++;
        return *this;
    }
    //重载后置++
    Point operator ++ (int)
    {
        Point temp = *this;
        x++;
        y++;
        return temp;
    }
    //重载前置--
    Point operator -- ()
    {
        (this->x)--;
        (this->y)--;
        return *this;
    }
    //重载后置--
    Point operator -- (int)
    {
        Point temp = *this;
        x--;
        y--;
        return temp;
    }

};
//
ostream& operator<<(ostream& os, const Point & obj) 
{
    os << "x: " << obj.x << " y: " << obj.y;
    return os;
}
//
int main()
{
    Point P1(1 , 2);
    Point P2(2 , 4);
    cout << "P1+P2 : " << endl << P1 + P2 << endl;
    cout << "P1-P2 : " << endl << P1 - P2 << endl;
    cout << "++P1: " << endl << ++P1 << endl;
    cout << "P1++: " << endl << P1++ << endl;
    cout << "--P1: " << endl << --P1 << endl;
    cout << "P1--: " << endl << P1-- << endl;
    return 0;
}
```



## 纯虚函数和抽象类

### 一般虚函数

在C++中，虚函数是一种特殊的函数，**它可以被子类重写**，并且可以通过**基类指针或引用调用它们**。一般来说，虚函数用于实现多态性，这是面向对象编程中的一个重要概念。

一般的虚函数声明如下：

```c++
virtual return_type function_name(parameter_list);
```

其中，关键字`virtual`表示这是一个虚函数。子类可以通过重写虚函数来提供自己的实现。

虚函数可以在基类中定义，但也可以在派生类中重新定义。当通过基类指针或引用调用虚函数时，将根据指针或引用所指对象的实际类型来选择相应的函数实现。这种行为被称为动态绑定或后期绑定。

### 虚析构函数

虚析构函数（virtual destructor）是 C++ 中特殊的函数。它在基类中使用 virtual 关键字声明，在派生类中也可以重载。与普通的析构函数不同的是，虚析构函数可以在通过基类指针或引用删除派生类对象时，正确地调用派生类的析构函数来释放内存。**如果没有使用虚析构函数，删除派生类对象时只会调用基类的析构函数**，导致派生类所占用的内存无法释放，从而可能导致内存泄漏。因此，当基类中有虚函数时，应该将析构函数也声明为虚函数。

虚析构函数的作用：

1. 正确释放资源：当基类指针指向派生类对象并调用delete操作时，如果基类的析构函数不是虚函数，将只会调用基类的析构函数而不会调用派生类的析构函数。这可能导致派生类中申请的资源没有正确释放，造成资源泄漏。通过在基类的析构函数前面添加virtual关键字，可以确保析构函数的动态绑定，从而正确地调用派生类的析构函数，确保释放所有相关资源。
2. 支持多态性：虚析构函数是实现多态性的基础之一。当基类指针指向派生类对象时，通过虚析构函数可以实现动态绑定，即在运行时根据指针所指向的对象的实际类型调用相应的析构函数。这样可以实现基类指针的多态性，提高代码的灵活性和可扩展性。

需要注意的是，虚析构函数应该与虚函数一起使用，**即基类中至少有一个虚函数**，以便通过基类指针或引用实现动态绑定。如果一个类中包含虚函数，通常建议将析构函数声明为虚函数，以确保正确的析构行为。如果一个类不会被继承，或者不会作为基类使用，可以不将析构函数声明为虚函数。

### 纯虚函数与抽象类

在C++中，纯虚函数是一种特殊的虚函数，它在基类中声明但没有提供实现。纯虚函数用**关键字 `virtual` 和 `= 0`** 来声明，在基类中没有具体的函数体。

纯虚函数的声明示例：

```c++
class Base {
public:
    virtual void pureVirtualFunction() = 0;
};
```

**一个含有纯虚函数的类称为抽象类**。**抽象类不能被实例化**（**不能定义一个抽象类的对象，但是可以定义一个抽象类的指针或引用，通过指针或引用就可以指向并访问派生类的对象**），只能用作其他类的基类。抽象类中的纯虚函数**必须**在派生类中重写（提供实现），否则派生类也将变为抽象类。

派生类中重写纯虚函数的示例：

```c++
class Derived : public Base {
public:
    void pureVirtualFunction() override 
    {
        // 提供具体的函数实现
        // ...
    }
};
```

抽象类可以包含普通的成员函数和数据成员，与普通的类一样，但只要包含了至少一个纯虚函数，该类就成为抽象类。

抽象类的主要作用是定义一组接口和规范，派生类必须实现这些接口才能被实例化。抽象类提供了一种强制约束派生类实现特定功能的机制。

需要注意的是，**抽象类不能直接实例化，只能通过指针或引用来操作**。例如：

```c++
Base* ptr = new Derived();  // 使用抽象类的指针来指向派生类对象
ptr->pureVirtualFunction(); // 调用派生类中的纯虚函数
delete ptr;                 // 释放内存
```

纯虚函数和抽象类为C++中的多态提供了基础，使得基类可以定义一组接口，而派生类可以根据具体需求提供自己的实现。这种特性提高了代码的灵活性和可扩展性。

# 群体类和群体数据的组织

## 模板

### 函数模板

函数模板定义了一个通用的函数，其中包含一个或多个类型参数。**这些类型参数在使用函数模板时由具体的类型替换**。这样，我们就可以使用相同的代码来处理不同类型的数据，而不必为每种类型编写不同的函数。函数模板的语法使用关键字`template`和`typename`（或`class`）来定义类型参数。

```c++
template <typename T> //T是通用的数据类型，名称可更换
void swap(T& a, T& b) 
{
    T temp = a;
    a = b;
    b = temp;
}
```

在这个例子中，T是一个类型参数，它用于定义a和b的类型。当我们使用该函数模板时，我们将具体的类型作为参数传递给T，例如：

```c++
int x = 1, y = 2;
swap(x, y); // x = 2, y = 1
```

使用函数模板有两种方式：

1. 自动类型推导：编译器对传入函数体的参数进行识别
2. 显示指定类型：`函数名<类型> (参数....)`

#### 使用函数模板注意事项

1. 模板参数的类型**必须在函数体内使用**，否则编译器会报错。
2. **函数体中的参数必须是同一类型的(即可以推断出同一个T)**，否则会出现错误
3. 函数模板可以有默认的类型参数，这些默认参数应该放在参数列表的最右边。
4. 函数模板的定义和声明通常要放在头文件中，以便在多个源文件中使用。
5. 在使用函数模板时，需要显式地指定模板参数的类型，或者编译器可以根据函数参数的类型进行推导。
6. 如果在函数模板中使用了类类型作为模板参数，需要确保该类有合适的构造函数和拷贝构造函数。

```c++
// 普通函数
int add(int a, int b) {
    return a + b;
}

// 函数模板
template <typename T>
T add(T a, T b) 
{
    return a + b;
}//返回的也该是T
```

#### 普通函数与函数模板区别

1. 普通函数使用时可以发生隐形的类型转换
2. 函数模板 用自动类型推导 ，不可以发生隐形类型转换(没法推导出一致的T类型)
3. 函数模板 用显示指定类型 ， 可以发生隐形的类型转换

#### 普通函数与函数模板调用规则

1. 若普通函数与函数模板都可以实现，**优先**调用**普通**函数
2. 可以通过**空模板参数列表**`函数名<>(参数...);`来强制调用函数模板
3. 函数模板也可以**重载**
4. 若函数模板可以产生更好的匹配，优先调用函数模板

#### 模板的局限性

模板的通用性不是万能的

以下是一些函数模板通用性受限的情况：

1. 需要特定的类型支持：某些操作可能依赖于特定类型的特性或操作符重载。如果使用的类型不支持所需的操作或特性，函数模板可能无法正常工作。
2. 需要类型信息：某些情况下，函数模板需要访问类型的具体信息，如类型的大小、成员函数、成员变量等。然而，函数模板只能根据传入的参数类型进行通用编码，无法直接访问类型的具体信息。
3. 对类型的限制：函数模板可以使用类型的通用特征，如拷贝构造函数、赋值运算符等。但是，有些类型可能不符合这些要求，或者需要特定的类型约束，此时函数模板的通用性就会受到限制。

```c++
//例如，考虑以下函数模板 Max() 用于返回两个值中的较大值：
template <typename T>
T Max(T a, T b)
{
    return (a > b) ? a : b;
}
//这个函数模板可以用于比较各种类型的值，如整数、浮点数、字符等。然而，如果我们想要比较两个自定义类型的对象，而这些对象没有定义大于运算符 > 的重载，那么编译时将会错误

int maxInt = Max(intValue1, intValue2);                // 正常工作
float maxFloat = Max(floatValue1, floatValue2);        // 正常工作
char maxChar = Max(charValue1, charValue2);             // 正常工作
MyClass maxMyClass = Max(myClassValue1, myClassValue2); // 编译时错误，MyClass类型没有定义大于运算符
```

为了解决函数模板通用性受限的问题，可以采取以下几种方法：

1. 重载函数模板：针对特定类型编写重载的函数模板或非模板函数，以提供特定类型的操作。这样可以在需要特定操作的情况下调用适当的重载函数，而不是使用通用的模板函数。
2. 提供类型限定：在函数模板中添加对特定类型的限定，以确保只有支持特定操作的类型才能使用该模板。可以使用类型特征或概念来限定模板参数，以保证特定操作的可用性。这样可以在编译时检查类型的支持情况。例如，使用类型特征 `std::is_arithmetic` 限定模板参数为算术类型：

### 类模板

类模板允许我们定义一个通用的类，可以在实例化时使用不同的数据类型。与函数模板类似，类模板也使用模板参数来指定类型。

类模板的基本语法如下：

```c++
template <typename T> // 也可以使用class关键字
class ClassName {
  // class definition here
};
```

其中，`template`关键字用于指示这是一个类模板，`typename`关键字用于指示模板参数类型。`T`是模板参数的名称，可以替换为任何有效的标识符。在类定义中，可以使用`T`来代表模板参数类型。使用类模板时，需要通过指定模板参数的类型来实例化类。

```c++
#include <iostream>
#include <string>
using namespace std;
template <class NameType, class AgeType>
class Person
{
public:
    Person(NameType name, AgeType age)
    {
        this -> m_Name = name;
        this -> m_Age = age;
    }
    void showPerson()
    {
        cout << "name:" << this->m_Name << "age:" << this -> m_Age << endl;
    }
    
    NameType m_Name;
    AgeType m_Age;
};
//
int main()
{
    Person<string, int> p("孙悟空", 999);
    p.showPerson();
}
```

#### 类模板与函数模板区别

- 类模板没有自动类型推导的使用方式，必须使用`类名<传递的参数对应类型>对象名(传递参数...);` 
- 类模板在模板的参数列表中可以有默认参数：传递的参数中有固定的类型

#### 类模板对象作函数参数

三种传入方式:

1. 

- 指定传入类型。直接显示对象的数据类型（最常用)

  ```c++
  void printPerson1(Person<string, int>&p)  //把p传入，指定参数类型
  {
      p.showPerson();
  }
  void test01()
  {
      Person<string, int> p("孙悟空"，999);
      printPerson1(p);
  }
  ```

  

- 参数模板化

  ```c++
  template <class T1, class T2> 
  void printPerson2(Person<T1, T2>&p)  //把p传入，参数模板化
  {
      p.showPerson();
  }
  void test02()
  {
      Person<string, int> p("猪八戒"，999);
      printPerson2(p);
  }
  ```

  

- 整个类模板化

  ```c++
  template <class T> 
  void printPerson3(T &p)  //把p传入，参数模板化
  {
      p.showPerson();
  }
  void test03()
  {
      Person<string, int> p("唐僧"，30);
      printPerson2(p);
  }
  ```

#### 类模板与继承

- 当子类继承的父类是一个类模板时，子类在声明时，要指出父类中的T的类型
- 如果想灵活的指出父类中T的类型，子类也需要变为类模板

```c++
template <class T> 
class Base
{
    T m;
};
class Son : public Base<父类中T的类型>  //指出父类中的T的类型
{
    
};
```

```c++
template <class T> //子类也需要变为类模板
class Base
{
    T m;
};
template <class T1, class T2> //  
class Son : public Base<T2>  //
{
    T1 obj;
};
void test()
{
    Son2<int , char>S2; //int 给了T1，char给了T2（即Base为char类型）
}
```

#### 类模板成员函数的类外实现

```c++
#include <iostream>
#include <string>
using namespace std
template <class NameType, class AgeType>
class Person
{
public:
    Person(NameType name, AgeType age);
    //{
    //    this -> m_Name = name;
    //    this -> m_Age = age;
    //}
    void showPerson();
    //{
    //    cout << "name:" << this->m_Name << "age:" << this -> m_Age << endl;
    //}
    NameType m_Name;
    AgeType m_Age;
};
//类外实现
template <class NameType, class AgeType>	//一定要加上这句
Person<NameType, AgeType>::Person(NameType name, AgeType age)	//需要加模板的参数列表
{
	this -> m_Name = name;
	this -> m_Age = age;
}
//
template <class NameType, class AgeType>
void Person<NameType, AgeType>::showPerson()//需要加模板的参数列表
{
    cout << "name:" << this->m_Name << "age:" << this -> m_Age << endl;
}
```

#### 类模板分文件编写

**MyClass.h** 文件：

```c++
#ifndef MYCLASS_H
#define MYCLASS_H

template <typename T>
class MyClass
{
private:
    T data;

public:
    MyClass(T value);
    void Print();
};

#include "MyClass.cpp"

#endif
```

**MyClass.cpp** 文件：

```c++
#include <iostream>
#include "MyClass.h"

template <typename T>
MyClass<T>::MyClass(T value) : data(value)
{
}

template <typename T>
void MyClass<T>::Print()
{
    std::cout << "Data: " << data << std::endl;
}
```

**main.cpp** 文件：

```c++
#include "MyClass.h"

int main()
{
    MyClass<int> myInt(10);
    myInt.Print();

    MyClass<double> myDouble(3.14);
    myDouble.Print();

    return 0;
}
```

在上述示例中，`MyClass.h` 文件包含了类模板的声明，并在文件末尾通过 `#include "MyClass.cpp"` 将类模板的定义包含进来。

`MyClass.cpp` 文件包含了类模板的定义，注意在定义之前要包含对应的头文件 `MyClass.h`。

在 `main.cpp` 文件中，通过包含 `MyClass.h` 头文件，就可以使用 `MyClass` 类模板创建对象并调用其成员函数。

#### 类模板与友元

```c++
template <typename T>
class MyClass
{
private:
    T data;
//
public:
    MyClass(T value) : data(value) {}

    template <typename U>//!!!
    friend void FriendFunction(const MyClass<U>& obj); //全局函数的类外实现

    template <typename U>
    friend class FriendClass;
};
//全局函数的类外实现。
template <typename U> //!!!
void FriendFunction(const MyClass<U>& obj)
{
    std::cout << "FriendFunction: " << obj.data << std::endl;
}
//实际是全局函数，所以不用加作用域

template <typename U>
class FriendClass
{
public:
    //类内实现
    void PrintData(const MyClass<U>& obj)
    {
        std::cout << "FriendClass: " << obj.data << std::endl;
    }
};

int main()
{
    MyClass<int> myInt(10);
    FriendFunction(myInt);

    FriendClass<int> friendObj;
    friendObj.PrintData(myInt);

    return 0;
}
```

在上述示例中，`FriendFunction` 是一个友元函数，它被声明为 `MyClass` 类模板的友元函数。它可以访问 `MyClass` 类模板中的私有成员 `data`。

`FriendClass` 是一个友元类，它被声明为 `MyClass` 类模板的友元类。它可以访问 `MyClass` 类模板中的私有成员 `data`。

在 `main` 函数中，我们创建了一个 `MyClass<int>` 对象 `myInt`，并通过调用友元函数 `FriendFunction` 和友元类 `FriendClass` 的成员函数来访问 `myInt` 的私有成员 `data`。

## 线性群体

### 基本概念

1. 线性群体的元素次序与其位置关系是对应的
2. 访问元素的不同方法有：直接访问、顺序访问（只能依次访问）和索引访问 (eg:数组)

#### 栈

栈（Stack）是一种**后进先出**（Last-In-First-Out，LIFO）的数据结构。类比于现实生活中的堆叠物品，最后放入的物品最先被取出。栈具有以下特点和操作：

1. 元素的插入操作称为压栈（Push），将元素放入栈顶。
2. 元素的删除操作称为弹栈（Pop），从栈顶移除元素。
3. 栈顶元素是最近插入的元素，也是唯一可访问的元素。
4. 可以使用栈来实现逆序操作，如逆序输出字符串或表达式求值等。

C++中的栈可以使用STL提供的`std::stack`模板类来实现，也可以自行实现基于数组或链表的栈结构。

#### 队列

队列（Queue）是一种**先进先出**（First-In-First-Out，FIFO）的数据结构。类比于现实生活中排队等候的情况，最先到达的元素最先被处理。队列具有以下特点和操作：

1. 元素的插入操作称为入队（Enqueue），将元素放入队列尾部。
2. 元素的删除操作称为出队（Dequeue），从队列头部移除元素。
3. 队列头部元素是最先插入的元素，也是唯一可访问的元素。
4. 可以使用队列来实现排队和调度等场景，如任务调度、消息传递等。

C++中的队列可以使用STL提供的`std::queue`模板类来实现，也可以自行实现基于数组或链表的队列结构。

### 数组类

```c++
#include <iostream>
using namespace std;

template <typename T>
class Array 
{
private:
    T* data;
    int size;

public:
    //构造函数
    Array(int size) 
    {
        this->size = size;
        data = new T[size];
    }
    //复制构造函数
    Array(const Array<T>&a)
    {
        //一定是进行深复制，为新的对象也申请属于自己的内存空间。而不是浅复制：简单的把原数组类中的首地址赋值给新数组类
        this->size = a.size;
        data = new T[size];
        for(int i = 0; i < size; i++)
        {
            data[i] = a.data[i];
        }
    }
    //析构函数
    ~Array() 
    {
        delete[] data;
    }
    //重载[]
    T& operator[](int index) 
    {
        return data[index];
    }

    Array<T>& operator=(const Array<T>& other) 
    {
        if (this != &other) 
        {
            delete[] data;
            size = other.size;
            data = new T[size];
            for (int i = 0; i < size; i++) 
            {
                data[i] = other.data[i];
            }
        }
        return *this;
    }

    Array<T> operator+(const Array<T>& other) 
    {
        if (size != other.size) 
        {
            throw runtime_error("Arrays must have the same size for addition.");
        }

        Array<T> result(size);
        for (int i = 0; i < size; i++) 
        {
            result.data[i] = data[i] + other.data[i];
        }
        return result;
    }

    Array<T> operator-(const Array<T>& other) 
    {
        if (size != other.size) 
        {
            throw runtime_error("Arrays must have the same size for subtraction.");
        }

        Array<T> result(size);
        for (int i = 0; i < size; i++) 
        {
            result.data[i] = data[i] - other.data[i];
        }
        return result;
    }

    friend ostream& operator<<(ostream& os, const Array<T>& arr) 
    {
        for (int i = 0; i < arr.size; i++) 
        {
            os << arr.data[i] << " ";
        }
        return os;
    }
};

int main() 
{
    Array<int> arr1(5);
    Array<int> arr2(5);

    for (int i = 0; i < 5; i++) 
    {
        arr1[i] = i + 1;
        arr2[i] = i * 2;
    }

    Array<int> arr3 = arr1 + arr2;
    Array<int> arr4 = arr1 - arr2;

    cout << "arr1: " << arr1 << endl;
    cout << "arr2: " << arr2 << endl;
    cout << "arr1 + arr2: " << arr3 << endl;
    cout << "arr1 - arr2: " << arr4 << endl;

    return 0;
}
```

#### 数组类中重载指针转换运算符

```c++
// 重载指针转换运算符
    operator int*() const 
    {
        return data;//返回当前对象中私有数组的首地址
    }

int main() 
{
    Array arr(5);

    for (int i = 0; i < 5; i++) 
    {
        arr[i] = i + 1;
    }

    // 使用指针转换运算符将数组对象转换为指针
    int* ptr = arr;

    // 通过指针访问数组元素
    for (int i = 0; i < 5; i++) {
        std::cout << ptr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 链表类

单链表 / 双向链表（每个节点中有两个指针，一个指向前驱结点，另一个指向后继结点）

#### 结点类模板

```c++
template<typename T>
class Node {
public:
    T data;           // 节点存储的数据
    Node<T>* next;    // 指向下一个节点的指针

    // 构造函数
    Node(const T& value) : data(value), next(nullptr) {
        // 初始化节点的数据为给定值，next指针为空
    }

    // 在本节点后插入一个新节点
    void insertAfter(const T& value) {
        Node<T>* newNode = new Node<T>(value);  // 创建新节点
        newNode->next = this->next;             // 新节点指向本节点的后继节点
        this->next = newNode;                    // 本节点指向新节点
    }

    // 删除本节点的后继节点并返回其地址
    Node<T>* removeNext() {
        if (this->next) {
            Node<T>* toDelete = this->next;        // 记录要删除的节点地址
            this->next = this->next->next;        // 本节点指向要删除节点的后继节点
            toDelete->next = nullptr;              // 将要删除节点的next指针置为空
            return toDelete;                       // 返回要删除的节点地址
        }
        return nullptr;
    }

    // 获取后继节点的地址
    Node<T>* getNext() const {
        return this->next;
    }
};
```

在这个示例中，我们扩展了节点类模板，并添加了三个成员函数：

- `insertAfter(const T& value)`：该函数在当前节点后插入一个新节点。它接受一个参数`value`，用于设置新节点的数据。函数首先创建一个新节点，并将其`next`指针指向当前节点的后继节点，然后将当前节点的`next`指针指向新节点，以完成插入操作。
- `removeNext()`：该函数删除当前节点的后继节点并返回其地址。如果当前节点存在后继节点，则函数将记录要删除的节点地址，将当前节点的`next`指针指向后继节点的后继节点，并将要删除节点的`next`指针置为空。最后，函数返回要删除的节点地址。如果当前节点没有后继节点，则函数返回`nullptr`。
- `getNext() const`：该函数用于获取当前节点的后继节点地址。它返回当前节点的`next`指针。

#### 链表类

```c++
template<typename T>
class LinkedList {
private:
    struct Node {
        T data;
        Node* next;

        Node(const T& value) : data(value), next(nullptr) {}
        // 构造函数：创建一个节点，初始化节点的数据为给定值，next指针为空
    };

    Node* head;  // 链表的头节点

public:
    LinkedList() : head(nullptr) {}
    // 构造函数：创建一个空链表，头节点指针初始化为空

    ~LinkedList() {
        clear();
    }
    // 析构函数：销毁链表，调用clear()函数删除所有节点

    void append(const T& value) {
        Node* newNode = new Node(value);
        // 创建一个新节点，其数据为给定值

        if (head == nullptr) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = newNode;
        }
        // 如果链表为空，则将头节点指针指向新节点
        // 否则，找到链表的最后一个节点，将其next指针指向新节点
    }

    void insert(int position, const T& value) {
        if (position < 0 || position > size()) {
            throw std::out_of_range("Invalid position");
        }
        // 检查位置是否合法，如果不合法抛出异常

        Node* newNode = new Node(value);
        // 创建一个新节点，其数据为给定值

        if (position == 0) {
            newNode->next = head;
            head = newNode;
        } else {
            Node* current = head;
            int count = 0;
            while (count < position - 1) {
                current = current->next;
                count++;
            }
            newNode->next = current->next;
            current->next = newNode;
        }
        // 如果位置为0，将新节点插入到头节点之前
        // 否则，找到插入位置的前一个节点，将新节点插入到其后面
    }

    void remove(int position) {
        if (position < 0 || position >= size()) {
            throw std::out_of_range("Invalid position");
        }
        // 检查位置是否合法，如果不合法抛出异常

        if (position == 0) {
            Node* temp = head;
            head = head->next;
            delete temp;
        } else {
            Node* current = head;
            int count = 0;
            while (count < position - 1) {
                current = current->next;
                count++;
            }
            Node* temp = current->next;
            current->next = temp->next;
            delete temp;
        }
        // 如果位置为0，删除头节点，并将头节点指针指向下一个节点
        // 否则，找到待删除节点的前一个节点，将其next指针跳过待删除节点，指向下一个节点
        // 删除待删除节点
    }

    T& get(int position) const {
        if (position < 0 || position >= size()) {
            throw std::out_of_range("Invalid position");
        }
        // 检查位置是否合法，如果不合法抛出异常

        Node* current = head;
        int count = 0;
        while (count < position) {
            current = current->next;
            count++;
        }
        return current->data;
        // 找到指定位置的节点，并返回其数据
    }

    void set(int position, const T& value) {
        if (position < 0 || position >= size()) {
            throw std::out_of_range("Invalid position");
        }
        // 检查位置是否合法，如果不合法抛出异常

        Node* current = head;
        int count = 0;
        while (count < position) {
            current = current->next;
            count++;
        }
        current->data = value;
        // 找到指定位置的节点，并将其数据修改为给定值
    }

    void clear() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
        // 从头节点开始，依次删除所有节点，直到链表为空
    }

    int size() const {
        Node* current = head;
        int count = 0;
        while (current != nullptr) {
            current = current->next;
            count++;
        }
        return count;
        // 遍历链表，计算节点的数量，并返回结果
    }

    void traverse(void (*function)(const T&)) const {
        Node* current = head;
        while (current != nullptr) {
            function(current->data);
            current = current->next;
        }
        // 遍历链表，对每个节点执行指定的函数操作
    }
};
```

### 栈类

有三种状态：栈满、栈空、一般状态

```c++
#include <iostream>
#include <map>
#include <exception>
#include <string>
#include <vector>
#include <cassert>
//
class StackException : public exception 
{
public:
    const char* what() const throw() // throw() stands for no exception
    {
        return "Stack is full or empty!";
    }
};
//栈类！！！
template<class T>
class Stack 
{
private:
    int top;
    T arr[MAX_SIZE];
public:
    Stack() : top(-1) // intialize top to -1, which means the stack is empty
    {
        cout << "Stack constructor has been constructed" << endl;
    }
    ~Stack() 
    {
        cout << "Stack destructor has been destructed" << endl;
    }
    //
    void push(T val) // push a value onto the stack
    {
        if(top >= MAX_SIZE - 1) 
        {
            throw StackException();
        }
        arr[++top] = val;
    }
    void pop() // pop the top element of the stack
    {
        if(top < 0) 
        {
            throw StackException();
        }
        top--;
    }
    T pop()  //另一种弹出栈顶元素的方式
    {
        assert( ! isEmpty() );
        return arr[top--];
    }
    T gettop() // return the top element of the stack
    {
        if(top < 0) 
        {
            throw StackException();
        }
        return arr[top];
    }
    //
    bool isEmpty() // check if the stack is empty
    {
        return (top == -1);
    }
    bool isFull() // check if the stack is full
    {
        return (top == MAX_SIZE - 1);
    }
    void clear()//清空栈
    {
        top = -1;
    }
};
```

### 队列类

有三种状态：队空、队满、一般状态

#### 使用数组实现

```c++
template<typename T, int MAX_SIZE>
class Queue {
private:
    T elements[MAX_SIZE];  // 存放队列元素的数组
    int front;  // 队列的前端，指向队首元素
    int rear;   // 队列的后端，指向队尾元素的下一个位置

public:
    Queue() : front(0), rear(0) {}  // 构造函数，初始化队列的前端和后端为0
    ~Queue() {}  // 析构函数

    void enqueue(const T& value) {
        if (isFull()) {  // 如果队列已满，则抛出异常
            throw std::out_of_range("Queue is full");
        }
        elements[rear] = value;  // 将元素存入队列的后端
        rear = (rear + 1) % MAX_SIZE;  // 更新队列的后端位置，循环利用数组空间
    }

    void dequeue() {
        if (isEmpty()) {  // 如果队列为空，则抛出异常
            throw std::out_of_range("Queue is empty");
        }
        front = (front + 1) % MAX_SIZE;  // 更新队列的前端位置，循环利用数组空间
    }

    T& getFront() const {
        if (isEmpty()) {  // 如果队列为空，则抛出异常
            throw std::out_of_range("Queue is empty");
        }
        return elements[front];  // 返回队列的前端元素
    }

    bool isEmpty() const {
        return front == rear;  // 如果队列的前端等于后端，表示队列为空
    }

    bool isFull() const {
        return (rear + 1) % MAX_SIZE == front;  // 如果队列的后端的下一个位置等于前端，表示队列已满
    }

    void clear() 
    {
        front = 0;  // 清空队列，将前端和后端都设置为0
        rear = 0;
    }
};
```



#### 链表实现

```c++
template<typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;

        Node(const T& value) : data(value), next(nullptr) {}
    };

    Node* front;  // 队列的前端
    Node* rear;   // 队列的后端

public:
    Queue() : front(nullptr), rear(nullptr) {}
    ~Queue() {
        clear();
    }

    void enqueue(const T& value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = newNode;
            rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    void dequeue() 
    {
        if (isEmpty()) 
        {
            throw std::out_of_range("Queue is empty");
        }
        Node* temp = front;
        front = front->next;
        delete temp;
        if (front == nullptr) 
        {
            rear = nullptr;
        }
    }

    T& getFront() const {
        if (isEmpty()) {
            throw std::out_of_range("Queue is empty");
        }
        return front->data;
    }

    bool isEmpty() const 
    {
        return front == nullptr;
    }

    void clear() 
    {
        while (!isEmpty()) 
        \
        {
            dequeue();
        }
    }
};
```

### 群体数据的组织

#### 插入排序

由不同的寻找插入位置的方法，又可分为不同的插入排序法

```c++
#include <vector>

template<typename T>
void insertionSort(std::vector<T>& arr) {
    int n = arr.size();
    
    for (int i = 1; i < n; ++i) {
        T key = arr[i];
        int j = i - 1;
        
        // 将比 key 大的元素向右移动
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            --j;
        }
        
        arr[j + 1] = key;
    }
}
///直接插入排序的函数模板
```

#### 直接选择排序函数模板

```c++
#include <vector>

template<typename T>
void selectionSort(std::vector<T>& arr) {
    int n = arr.size();
    
    for (int i = 0; i < n - 1; ++i) {
        int minIndex = i;
        
        // 在剩余的元素中找到最小值的索引
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        // 将最小值交换到当前位置
        std::swap(arr[i], arr[minIndex]);
    }
}
```

#### 冒泡排序函数模板

```c++
#include <vector>

template<typename T>
void bubbleSort(std::vector<T>& arr)
{
    int n = arr.size();
    
    for (int i = 0; i < n - 1; ++i) {
        bool swapped = false;
        
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        
        // 如果某次遍历没有发生交换，则表示数组已经有序，可以提前结束
        if (!swapped) {
            break;
        }
    }
}
```

#### 顺序查找

#### 折半查找(二分法)

```c++
#include <vector>

template<typename T>
int binarySearch(const std::vector<T>& arr, const T& target)
{
    int left = 0;
    int right = arr.size() - 1;
while (left <= right) 
{
    int mid = left + (right - left) / 2;
    
    if (arr[mid] == target) 
    {
        return mid;
    }
    
    if (arr[mid] < target)
    {
        left = mid + 1;
    }
    else
    {
        right = mid - 1;
    }
}

return -1; // 如果未找到目标元素，则返回 -1 表示不存在
}
```
# STL

标准模块库：容器、算法、迭代器

六大组件：容器、算法、迭代器、仿函数、适配器、空间配置器

1. 顺序容器：将一组具有相同类型的元素以严格的线性形式组织起来。向量，双端队列，列表
2. 关联容器：具有根据一组索引来快速提取元素的能力。集合，映射
3. 使用不同的容器，需要包含不同的头文件

1. 迭代器提供了顺序访问容器中每个元素的方法
2. 用“++”运算符来获得指向下一个元素的迭代器
3. 用“*”运算符访问该迭代器所指向的元素
4. 用“->”运算符访问该迭代器所指向元素的一个成员
5. 迭代器是泛化的指针
6. 使用STL的迭代器，需要包含**<iterator>**头文件

1. 函数对象是一个行为类似函数的对象
2. 函数对象是泛化的函数
3. 使用STL的函数对象，需要包含头文件**<functional>**

1. STL包含70多个算法
2. 查找，排序，消除，计数，比较，变换，置换，容器管理等
3. 使用STL的算法，需要包含**<algorithm>**头文件
4. STL把迭代器作为算法的参数，通过迭代器来访问容器而不是把容器直接作为算法的参数
5. STL把函数对象作为算法的参数而不是把函数所执行的运算作为算法的一部分

## 迭代器

### 输入流、输出流迭代器

**输入流迭代器**用于从输入流中读取数据，并将其作为迭代器的值。可以使用输入流迭代器来遍历输入流中的数据，就像遍历容器中的元素一样。通常使用 **`istream_iterator`** 类来创建输入流迭代器。

```c++
#include <iostream>
#include <iterator> // ！！头文件
#include <numeric>  // for accumulate
using namespace std

int main() {
    // 创建输入流迭代器，从标准输入读取整数
    istream_iterator<int> inputIterator(cin);

    // 创建输入流迭代器的结束迭代器
    istream_iterator<int> endIterator;

    // 使用 accumulate 算法计算输入的整数的总和
    int sum = accumulate(inputIterator, endIterator, 0);

    // 输出总和
    cout << "Sum: " << sum << endl;

    return 0;
}
//在上述示例中，我们使用 istream_iterator<int> 创建了输入流迭代器 inputIterator，并将其与 std::cin（标准输入）关联。然后，我们使用 accumulate 算法将输入流迭代器的值累加到变量 sum 中。最后，我们输出计算得到的总和。
```

**输出流迭代器**用于向输出流中写入数据，就像将数据插入到容器中一样。可以使用输出流迭代器来逐个写入元素，或者使用迭代器范围一次写入多个元素。通常使用 **`ostream_iterator`** 类来创建输出流迭代器。

```c++
#include <iostream>
#include <iterator>
#include <vector>

int main() 
{
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // 创建输出流迭代器，将整数写入标准输出
    std::ostream_iterator<int> outputIterator(std::cout, " "); //后一个参数代表了没个输出数据之间的分隔符

    // 使用输出流迭代器将容器中的整数写入标准输出
    for (const auto& num : numbers) {
        *outputIterator = num;  // 写入当前元素
        ++outputIterator;       // 移动迭代器到下一个位置
    }

    std::cout << std::endl;

    return 0;
}
```

+课本主要内容

## 容器

### 基本功能与分类

<img src="D:\资料\学科学习资料\编程笔记\面向对象技术\IMG_20230528_103421.jpg" alt="IMG_20230528_103421" style="zoom:30%;" />

有时需要显式地写出迭代器类型，下面举例：类型为S的容器的相关迭代器

1. `S::iterator`普通迭代器类型，所指向元素的类型为`T`
2. `S::const_iterator`常迭代器类型，所指向元素的类型为const T

以下是STL中常见容器的头文件以及它们所属的概念：

1. vector（向量）：
   - 头文件：`<vector>`
   - 概念：动态数组，支持快速的随机访问和动态调整大小。
2. list（链表）：
   - 头文件：`<list>`
   - 概念：双向链表，支持快速的插入和删除操作。
3. deque（双端队列）：
   - 头文件：`<deque>`
   - 概念：双端队列，支持在两端进行高效的插入和删除操作。
4. array（数组）：
   - 头文件：`<array>`
   - 概念：固定大小的数组，支持快速的访问和遍历。
5. set（集合）：
   - 头文件：`<set>`
   - 概念：有序集合，存储唯一的元素，并按照一定的顺序进行排序。
6. multiset（多重集合）：
   - 头文件：`<set>`
   - 概念：有序多重集合，可以存储重复的元素，并按照一定的顺序进行排序。
7. map（映射）：
   - 头文件：`<map>`
   - 概念：键值对的集合，按照键的顺序进行排序。
8. multimap（多重映射）：
   - 头文件：`<map>`
   - 概念：键值对的多重集合，可以存储重复的键值对，并按照键的顺序进行排序。

这些容器提供了不同的数据结构和操作方式，适用于不同的场景和需求。通过包含相应的头文件，可以使用这些容器来存储和操作数据。

STL为每个**可逆迭代器**提供了逆向迭代器，逆向迭代器可通过以下成员函数实现：`S.rbegin() & S.rend()`
一个迭代器和他的逆向迭代器之间可以相互转化

### 顺序容器

#### 顺序容器的一些常用构造函数：

1. 默认构造函数：创建一个空的容器。
   ```cpp
   std::vector<int> vec;  // 默认构造一个空的vector
   std::list<int> lst;    // 默认构造一个空的list
   std::deque<int> deq;   // 默认构造一个空的deque
   std::array<int, 5> arr;   // 默认构造一个大小为5的array，元素默认初始化为0
   ```

2. 带有初始元素的构造函数：创建一个包含初始元素的容器。
   ```cpp
   std::vector<int> vec = {1, 2, 3};  // 创建一个包含初始元素1、2、3的vector
   std::list<int> lst = {4, 5, 6};    // 创建一个包含初始元素4、5、6的list
   std::deque<int> deq = {7, 8, 9};   // 创建一个包含初始元素7、8、9的deque
   std::array<int, 5> arr = {1, 2, 3, 4, 5};   // 创建一个包含初始元素1、2、3、4、5的array
   ```

3. 拷贝构造函数：创建一个与现有容器相同的副本。
   ```cpp
   std::vector<int> vec1 = {1, 2, 3};
   std::vector<int> vec2(vec1);   // 使用vec1的副本初始化vec2
   std::list<int> lst1 = {4, 5, 6};
   std::list<int> lst2(lst1);     // 使用lst1的副本初始化lst2
   ```

4. 范围构造函数：创建一个包含另一个容器指定范围内元素的容器。
   ```cpp
   std::vector<int> vec1 = {1, 2, 3, 4, 5};
   std::vector<int> vec2(vec1.begin() + 1, vec1.end() - 1);  // 创建一个包含vec1中索引1到索引3的元素的vector
   std::list<int> lst1 = {4, 5, 6, 7, 8};
   std::list<int> lst2(lst1.begin(), lst1.end());  // 创建一个包含lst1中所有元素的list
   ```

5. 填充构造函数：创建一个包含重复元素的容器。
   ```cpp
   std::vector<int> vec(5, 10);   // 创建一个包含5个值为10的元素的vector
   std::list<int> lst(3, 7);      // 创建一个包含3个值为7的元素的list
   std::deque<int> deq(4, 3);     // 创建一个包含4个值为3的元素的deque
   std::array<int, 5> arr{0};     // 创建一个包含5个值为0的元素的array
   ```
   
   #### 赋值函数
   
   在STL中，顺序容器提供了`assign()`函数来将指定的元素赋值给容器。该函数用于替换容器中的现有元素，并将新元素插入到容器中。
   
   #### 元素的插入+.....
   
   ![IMG_20230528_110050](D:\资料\学科学习资料\编程笔记\面向对象技术\IMG_20230528_110050.jpg)

## 初识

### vector存放内置数据类型

在C++中，`vector` 是一个**动态数组**容器，可以用于存放内置数据类型（如整数、浮点数等）。

下面是一个示例，展示如何使用 `vector` 存放内置数据类型：

```c++
#include <iostream>
#include <vector> //包含头文件
using namespace std;

int main()
{
    vector<int> numbers; // 声明一个存放整数的 vector :numbers
    //  vector<int> numbers(N); 定义一个大小为N的容器

    // 添加元素到 vector
    numbers.push_back(10);
    numbers.push_back(20);
    numbers.push_back(30);
    
    //通过迭代器访问容器中的数据
    vector<int> :: iterator itBegin = numbers.begin(); //起始迭代器，指向第一个元素
	vector<int> :: iterator itEnd = numbers.end(); //结束迭代器，指向容器中的最后一个元素的下一个位置
    
    //第一种访问方式
    while(itBegin != itEnd)
    {
        cout << *itBegin << endl;
        itBegin++;
    }
    
    //第二种访问方式
    for(vector<int> :: iterator it = numbers.begin(); it != numbers.end(); it++)
    {
        cout << *it << endl;
    }
    
    //第三种访问方式，利用STL提供的遍历算法
    void myPrint(int val)
    {
        cout << val << endl;
    }
    for_each(numbers.begin(), numbers.end(), myPrint);
    
    // chatgpt给出的访问 vector 中的元素
    for (int i = 0; i < numbers.size(); i++)
    {
        cout << numbers[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### 存放自定义数据类型

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// 自定义类
class Person {
public:
    string name;
    int age;
    Person(const string& n, int a) : name(n), age(a) {}
};

int main() {
    vector<Person> people; // 声明一个存放 Person 对象的 vector

    // 添加 Person 对象到 vector
    people.push_back(Person("Alice", 25));
    people.push_back(Person("Bob", 30));
    people.push_back(Person("Charlie", 35));

    // 遍历数据
    for (vector<Person> :: iterator it = People.begin(); it != People.end(); it++) 
    {
        cout << "Name: " << (*it).name << ", Age: " << (*it).age << endl;
    }

    return 0;
}
```

### vector容器嵌套容器

`vector< vector<数据类型> > 容器名;` 

向小容器中添加数据；然后将小容器插入到大容器中；通过大容器将所有数据遍历一遍，其中嵌套有遍历小容器的循环



## string容器

string本质是一个类，类内部封装了`char*`，是一个`char*`型的容器

### 构造函数

1. 默认构造函数：

   ```c++
   string str;               // 创建一个空字符串
   ```

2. 字符串字面值构造函数：

   ```c++
   string str = "Hello";     // 使用字符串字面值初始化字符串
   ```

3. 字符串拷贝构造函数：

   ```c++
   string str1 = "Hello";
   string str2(str1);        // 使用另一个字符串进行拷贝构造
   ```

4. 子串构造函数：

   ```c++
   string str1 = "Hello, world!";
   string str2(str1, 7, 5);  // 从 str1 的第 7 个位置开始，长度为 5 构造子串
   ```

5. 重复字符构造函数：

   ```c++
   string str(5, 'A');       // 构造一个包含 5 个重复字符 'A' 的字符串
   ```

6. 使用字符串进行初始化：

   ```c++
   const char * str = "hello";
   string s(str);
   ```

### 赋值操作

1. 字符串赋值(等号方式)：

   ```c++
   string str1 = "Hello";
   string str2;
   str2 = str1;      // 将 str1 的值赋给 str2
   ```

2. 字符串字面值赋值(等号方式)：

   ```c++
   string str;
   str = "Hello";    // 将字符串字面值赋给 str
   ```

3. 字符赋值(等号方式)：

   ```c++
   string str;
   str = 'A';       // 将单个字符赋给 str
   ```

4. assign方式：

   ```c++
   //1
   string str1;
   str1.assign("hello");
   //2
   string str2;
   str2.assign("hello", 3);//对前三个赋值
   //3
   string str3;
   str3.assign(str2);
   //4
   string str4;
   str4.assign(10, 'w');
   ```

### 字符串拼接

1. 使用 `+` 运算符：

   ```c++
   string str1 = "Hello";
   string str2 = " world!";
   string result = str1 + str2;    // 使用 + 运算符拼接字符串
   ```

2. 使用 `append` 函数：

   ```c++
   string str1 = "Hello";
   string str2 = " world!";
   string result = str1.append(str2);    // 使用 append 函数拼接字符串
   ```

无论是使用 `+` 运算符还是 `append` 函数，都可以实现字符串的拼接。需要注意的是，使用 `+` 运算符时，两个操作数必须都是 `string` 类型的对象或字符串字面值；而使用 `append` 函数时，可以将一个 `sstring` 类型的对象或字符串字面值追加到另一个字符串末尾。

此外，还可以使用其他方式进行字符串拼接，例如使用 `+=` 运算符将一个字符串追加到另一个字符串末尾，或使用 `ostringstream` 类来进行复杂的字符串拼接操作。选择合适的方法取决于具体的需求和代码风格。

### 字符串查找和替换

1. 字符串查找：
   - `find` 函数：查找指定子字符串在原字符串中第一次出现的位置，返回位置的索引值，如果找不到则返回 `std::string::npos`。
   - `rfind` 函数：从字符串末尾开始查找指定子字符串，返回位置的索引值，如果找不到则返回 `std::string::npos`。
   - `find_first_of` 函数：查找原字符串中任意一个指定字符出现的位置，返回位置的索引值，如果找不到则返回 `std::string::npos`。
   - `find_last_of` 函数：从字符串末尾开始查找原字符串中任意一个指定字符出现的位置，返回位置的索引值，如果找不到则返回 `std::string::npos`。
2. 字符串替换：
   - `replace` 函数：将指定范围内的字符替换为新的字符串。
   - `substr` 函数：获取原字符串中指定位置和长度的子字符串，然后可以使用赋值操作符或其他替换方法将其替换为新的字符串。

下面是使用这些函数进行字符串查找和替换的示例代码：

```c++
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello world!";

    // 字符串查找
    size_t found = str.find("world");  // 查找子字符串 "world"
    if (found != std::string::npos) {
        std::cout << "Found at index: " << found << std::endl;
    }

    // 字符串替换
    str.replace(found, 5, "everyone");  // 将 "world" 替换为 "everyone"
    std::cout << "Modified string: " << str << std::endl;

    return 0;
}
```



## map容器

### 概念

- map中每个元素都是一对，第一个元素为key（键值），第二个为value（数据）
- 所有元素会依据元素的键值**自动排序**
- 属于关联式容器，用二叉树实现
- map与multimap区别

### 构造及赋值

构造函数：

```c++
std::map<Key, Value> map;                          // 默认构造函数，创建一个空的 map 容器
std::map<Key, Value> mapCopy(anotherMap);          // 使用另一个 map 容器初始化新的 map 容器
std::map<Key, Value> mapWithInitializer = { {key1, value1}, {key2, value2}, ... };  // 使用初始化列表创建 map 容器
```

赋值操作：

```c++
std::map<Key, Value> map1;
std::map<Key, Value> map2;

// 使用赋值操作符 "=" 将一个 map 容器的内容复制到另一个 map 容器
map2 = map1;

// 使用成员函数 assign() 将一个 map 容器的内容复制到另一个 map 容器
map2.assign(map1.begin(), map1.end());

// 使用成员函数 insert() 插入另一个 map 容器中的元素到当前 map 容器
map2.insert(map1.begin(), map1.end());

// 使用成员函数 swap() 交换两个 map 容器的内容
map1.swap(map2);
```

在使用 `insert` 函数向 `std::map` 容器中插入元素时，需要注意以下事项：

1. 插入单个元素：可以使用 `std::pair` 对象或者使用 `{key, value}` 形式的初始化列表来插入单个键值对元素。

   ```c++
   std::map<Key, Value> map;
   Key key = ...;
   Value value = ...;
   
   // 使用 std::pair 对象插入单个元素
   map.insert(std::pair<Key, Value>(key, value));//一定要有pair
   
   // 使用初始化列表插入单个元素
   map.insert({key, value});
   ```

2. 插入多个元素：可以使用迭代器范围或者初始化列表来插入多个键值对元素。

   ```c++
   std::map<Key, Value> map;
   std::map<Key, Value> anotherMap;
   
   // 使用迭代器范围插入多个元素
   map.insert(anotherMap.begin(), anotherMap.end());
   
   // 使用初始化列表插入多个元素
   map.insert({{key1, value1}, {key2, value2}, ...});
   ```

3. 重复键处理：`std::map` 容器中的键是唯一的，**如果插入的键已经存在于容器中，那么插入操作将不会进行任何改变。**

### map容器的大小和交换

1. 大小操作（Size）
   - 使用成员函数`size()`来获取`std::map`容器中键值对的数量。
   - 返回值类型为`size_t`，表示容器的大小。

```c++
std::map<Key, Value> map;
// 添加元素到map容器中
map.insert({key1, value1});
map.insert({key2, value2});

// 获取map容器的大小
size_t size = map.size();
std::cout << "Size of the map: " << size << std::endl;
```

1. 交换操作（Swap）
   - 使用成员函数`swap()`可以交换两个`std::map`容器的内容。
   - 交换后，原来的容器将包含另一个容器的元素，而另一个容器将包含原来容器的元素。

```c++
std::map<Key, Value> map1;
std::map<Key, Value> map2;

// 添加元素到map1和map2中

// 交换map1和map2的内容
map1.swap(map2);
```

交换操作对于需要在不同地方使用不同的`std::map`容器，或者需要重新构建容器内容时非常有用。它可以高效地交换容器的内容，而无需复制或重新分配元素。

### 插入和删除

删除元素

- 使用`erase()`函数可以从`std::map`容器中删除指定的键值对。
- 可以通过指定要删除的键或者迭代器来执行删除操作。

```c++
std::map<Key, Value> map;

// 添加元素到map容器中

// 通过键删除元素
map.erase(key1);

// 通过迭代器删除元素
std::map<Key, Value>::iterator it = map.find(key2);
if (it != map.end()) {
    map.erase(it);
}
```

在执行删除操作时，如果指定的键不存在于容器中，`erase()`函数将不会执行任何操作

### 查找和统计

1. 查找元素
   - 使用`find()`函数可以在`std::map`容器中查找指定的键，并**返回**一个指向该键的**迭代器**。
   - 如果找到了指定的键，则返回指向该键的迭代器；如果未找到，则返回指向容器末尾的迭代器(`end()`迭代器)。
   - 可以使用返回的迭代器来访问找到的键值对。

```c++
std::map<Key, Value> map;

// 添加元素到map容器中

// 查找指定键
std::map<Key, Value>::iterator it = map.find(key);
if (it != map.end()) {
    // 找到了指定键
    // 使用迭代器访问键值对
    Key foundKey = it->first;
    Value foundValue = it->second;
} else {
    // 未找到指定键
}
```

1. 统计元素出现次数
   - 使用`count()`函数可以统计指定键在`std::map`容器中的出现次数。
   - 返回一个表示指定键出现次数的整数值，要么是0（表示未找到），要么是1（表示找到一次，因为`std::map`容器中的键是唯一的）。

```c++
std::map<Key, Value> map;

// 添加元素到map容器中

// 统计指定键的出现次数
int occurrences = map.count(key);
if (occurrences > 0) {
    // 指定键出现了至少一次
} else {
    // 指定键未找到
}
```

### 排序

如果要改变排序的方式，可以使用自定义的比较函数（比较器）来指定排序规则。

以下是使用自定义比较函数进行排序的示例：

```c++
#include <iostream>
#include <map>

// 自定义比较函数，按照键的降序进行排序
struct Compare {
    bool operator()(const int& a, const int& b) const {
        return a > b;
    }
};

int main() {
    std::map<int, std::string, Compare> map;

    // 向map容器中添加元素
    map[3] = "Three";
    map[1] = "One";
    map[2] = "Two";

    // 遍历map容器，按照排序规则输出键值对
    for (const auto& pair : map) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

输出结果：

```c++
makefileCopy code3: Three
2: Two
1: One
```

在上述示例中，通过自定义比较函数`Compare`，将键按照降序进行排序。在创建`std::map`容器时，通过指定比较函数的类型为`Compare`来应用自定义的排序规则。

注意，在使用自定义比较函数时，需要确保比较函数满足严格弱序关系（Strict Weak Ordering）的要求，以保证排序的正确性。

# 注意事项

1. **只有构造函数可以使用初始化列表进行初始化**

2. assert语句
   `assert` 是 C++ 中的一个宏，用于在程序中进行断言（Assertion）。**它的作用是在运行时检查一个条件是否为真，如果条件为假，则终止程序的执行并输出错误信息。**

   ```c++
   #include <cassert>
   
   int main() {
       int x = 5;
       assert(x > 0);  // 断言 x > 0
       // 如果 x <= 0，程序将终止执行并输出错误信息
   
       // 其他代码...
   
       return 0;
   }
   ```

   在上述示例中，`assert(x > 0)` 表示断言条件 `x > 0`，即检查变量 `x` 是否大于 0。如果 `x` 不满足该条件，那么程序将停止执行，并输出一个错误信息，指示断言失败的位置和条件。

   `assert` 宏的使用场景通常是在开发过程中用于检查程序的正确性，例如检查输入参数的有效性、检查循环或函数内部的不变量等。当程序在调试模式下运行时，断言会被执行并提供错误提示，但在发布版本中会被忽略，以避免性能损失。

   需要注意的是，断言是用于检查程序逻辑和假设的工具，并不适用于处理运行时错误和异常情况。对于需要处理异常的情况，应该使用适当的异常处理机制来处理错误。

3. 




在C++中，`std::string` 是一个非常常用的字符串容器类，它提供了一系列操作和功能，使得处理字符串变得更加方便和高效。

下面是一些 `std::string` 容器的常用操作和功能：

1. 创建字符串对象：

   ```c++
   std::string str;                        // 创建一个空字符串
   std::string str = "Hello, world!";       // 使用字符串字面值初始化字符串
   std::string str("Hello, world!");        // 使用构造函数初始化字符串
   ```

2. 访问字符串的字符：

   ```
   cppCopy codechar ch = str[i];                        // 通过下标访问字符串的字符
   char& ref = str[i];                      // 通过下标获取字符的引用，可以修改字符
   ```

3. 修改字符串内容：

   ```
   cppCopy codestr = "New value";                       // 重新赋值
   str += " Appended";                      // 追加字符串
   str.append(" More");                     // 追加字符串
   str.insert(pos, "Inserted");              // 在指定位置插入字符串
   str.erase(pos, count);                    // 删除指定位置的字符
   ```

4. 获取字符串的长度和子串：

   ```
   cppCopy codeint length = str.length();                // 获取字符串的长度
   std::string substr = str.substr(pos, len); // 获取子串，从指定位置开始，长度为 len
   ```

5. 查找和替换字符串：

   ```
   cppCopy codesize_t pos = str.find("substring");        // 查找子串的第一次出现的位置
   size_t pos = str.find("substring", pos);   // 从指定位置开始查找子串的出现位置
   str.replace(pos, len, "newstring");        // 替换指定位置的子串为新的字符串
   ```

6. 比较字符串：

   ```
   cppCopy codeint result = str.compare(other);           // 比较字符串和另一个字符串，返回比较结果
   bool equal = (str == other);               // 判断字符串是否相等
   ```

7. 输入和输出字符串：

   ```
   cppCopy codestd::cout << str;                          // 输出字符串
   std::cin >> str;                           // 输入字符串
   std::getline(std::cin, str);                // 从输入流读取一行字符串
   ```

`std::string` 还提供了许多其他的成员函数和操作符重载，用于处理字符串。你可以根据需要查阅 C++ 的文档，深入学习 `std::string` 的使用和功能。

需要注意的是，`std::string` 是基于动态内存分配的，可以自动管理字符串的内存，因此你无需手动管理内存，从而简化了字符串的操作和处理。



q
