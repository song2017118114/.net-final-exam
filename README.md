<!-- TOC -->autoauto- [c#知识点总结](#c知识点总结)auto- [3](#3)auto- [9 LINQ与泛型集合](#9-linq与泛型集合)auto- [10 类与对象](#10-类与对象)auto- [11继承](#11继承)auto- [12](#12)auto- [13异常处理](#13异常处理)auto- [14](#14)auto        - [简单事件驱动GUI](#简单事件驱动gui)auto        - [14.3.3 代理与事件处理机制](#1433-代理与事件处理机制)auto    - [14.4 控件属性与布局](#144-控件属性与布局)auto        - [Form属性、方法与事件](#form属性方法与事件)auto        - [控件的Control父类常见属性](#控件的control父类常见属性)auto        - [Label类（Control的派生类）常见属性：](#label类control的派生类常见属性)auto        - [TextBox：](#textbox)auto        - [Button：](#button)auto        - [GroupBox和Panel的区别：GroupBox可以显示标题而没有滚动条。](#groupbox和panel的区别groupbox可以显示标题而没有滚动条)auto        - [复选框、单选框：](#复选框单选框)auto        - [图形框PictureBox](#图形框picturebox)auto        - [工具提示ToolTip](#工具提示tooltip)auto        - [数字上下控件NumericUpDown](#数字上下控件numericupdown)auto        - [鼠标事件](#鼠标事件)auto        - [键盘事件](#键盘事件)auto- [15](#15)auto        - [MenuStrip](#menustrip)auto        - [MonthCalendar控件](#monthcalendar控件)auto        - [DateTimePicker控件](#datetimepicker控件)auto        - [LinkLabel控件](#linklabel控件)auto        - [ListBox](#listbox)auto        - [ChecedListBox控件](#checedlistbox控件)auto        - [ComboBox控件](#combobox控件)auto        - [TreeView](#treeview)auto        - [ListView可以在清单项目旁边显示图标](#listview可以在清单项目旁边显示图标)auto        - [TabControl控件](#tabcontrol控件)auto        - [MDI](#mdi)autoauto<!-- /TOC -->
# c#知识点总结


# 3

```c#
using System;//Using指令帮助编译器找到这个程序可以使用的预定义类
public class Welcome1{
    public static void Main(string [] args){//M s 大小写
        Console.WriteLine("Welcome to C#");
        Console.Write("{0}\n{1}","hello","bitch");
        
        int num = Convert.ToInt32(Console.ReadLine());//读取输入
    }
}
```

string 类型不是String

```java
using System;
//属性
public class GradeBook{
    private string courseName;
    
    public string CourseName{
        get{
            return courseName;
        }
        set{
            courseName = value;//value
        }
    }
}
```

自实现属性：必须同时有get与set方法

```c#
using System;
public class GradeBook{
    //public 修饰
    public string CourseName{get; set;}
    
    public void DisplayMessage(){
        Console.WriteLine("hello\n{0}",CourseName);
    }
}
```

**浮点数与decimal类型**

float、double称为浮点类型

decimal变量精确存储有限范围内的实数，而浮点数只存储实数的近似值，但取值范围大得多。

decimal应用——表示金额，后面加M或m eg：7.33M是decimal而不是默认的输入实数（double）

```c#
public static void Main(string[] args){
    decimal depositAmount = Convert.ToDecimal(Console.ReadLine());
    Console.WriteLine("adding {0:C} to account balance\n",depositAmount);
    //{0:C}，0后面的冒号表示下一个字符是格式指定符，C表示币值currency
}
```

- 字符串格式指定符
  - C/c：**货币值**，默认小数位2位
  - D：格式化为小数，将数字显式为**整数**
  - N：将字符串格式化为带**逗号**和默认两位小数
  - E：**科学计数法**，默认6位小数
  - F：**固定小数位**格式化字符串：F2：保留两位小数
  - G：**小数或科学计数法**，这个是隐式默认的
  - X：格式化字符串为**十六进制值**

```c#
private void IncrementLetterGradeCounter(int grade){
    switch (grade/10)
    {
        case 9:
        case 10:
            break;
            
        default:
            ++count
            break;
    }
}
```

- ^ 布尔逻辑异或，异或只有不同时为1，相同为0

- .NET框架类库FCL：提供了丰富的函数集合

- 方法

  - 静态方法Math.Sqrt(900.0)
  - Math类中Abs(x) Ceiling(x) Floor(x) Math.PI Math.E
  - num = **randomNumbers.Next(开始值,开始值+随机数个数)**，该函数是左闭右开

- 枚举类

  声明：private **enum** **Status** { CONTINUE, WOW, LOST}

  ​			private **enum** **DiceNames**

  ​			{

  ​					SNAKE_EYES = 2,

  ​					TREY = 3,	

  ​					SEVEN = 7

  ​			}

  使用：gameStatus = Status.WON

  case DiceNames.TREY

  - int sumOfDice = randomNumbers.Next(1,7);
  - switch( (**DiceNames**)  sumOfDice)——枚举类还能根据其类型进行强制转换
  
- C# 函数参数按值传递（call-by-value）：参数按值调用传递时，生成参数值副本并传给被调函数

  副本的改变不影响调用者的原始变量值，按引用调用时，调用者让被调函数直接能够访问调用者的数据，并允许被调函数修改其中的数据

  - 即使引用本身按值传递，这个方法仍然可以使用收到的引用来改变内存中的原对象，效果上**对象总是按引用传递**

  - ref、out——要按引用传递一个变量，使被调方法可以修改变量值

  - 参数声明中使用ref可以将变量按引用传递给法，可以修改原变量

  - ref主要用于调用方法中已经初始化的变量

  - 如果调用方法包含未初始化变量变元时，编译器产生错误，使用out可以建立输出参数，告诉编译器这个变元按引用传入被调方法，被调方法对调用者的原变量赋值

    ```c#
    public void test1(){
        int y = 5;
        int z;//未初始化
        
        A(ref y);
        B(out z);//未初始化要用out
    }
    
    void A(ref int x){
        x = x*x;
    }
    
    void B(out int x){
        x = 6;
        x = x*x;        
    }
    ```

- 数组，和java一样

  string[] b = new string[100],x = new string[27];

- 改变数组长度：

  int[] newArray = new int[5];

  Array.Resize(**ref** newArray,10);

- 数组长度，L大写：array.Length;

- 数组初始化器：int[] n = {10,20,30,40};

- 常量修饰符const int ARRAY_LENGTH = 10;

- foreach(**int** num **in** array){

  ​		total += num;

  }

- 隐藏类型局部变量：for、foreach都可以用

  foreach( var num in myArray)

- 还可以用于初始化数组而不显示指定类型

  **var** array = new [] {1,2,3,4}

- 被传入数组的函数形参 void ModifyArray ( double[]  b)

- c# 中存储数组之类的对象并不存储对象本身，而是存储对象的引用  

- c#可以用ref关键字引用传递引用类型变量，使被调方法修改调用者的原变量，使这个变量引用内存中的不同对象

- 按照值传递引用，只会改变之前变量的值；而按引用传递引用，则会改变这个引用对之前变量的引用

- 多维数组：C#支持矩形数组和齿状数组

- 数组初始化器：int**[  ,  ]** b = { {1,2} , {3, 4} };

- int[][] \[] [] jagged = { new int[] {1,2},

  ​								new int[] {3},

  ​								new int[] {4,5,6}};

- int[,] b; b = new int **[3,4]**;  //3行4列

- array.GetLength(0) 返回array第一维的长度（行数）1返回第二维的长度（列数）

- 二维数组的遍历

  ```c#
  public static void OutputArray(int [][] array){
  	foreach(var row in array){
          foreach(var element in row){
              Console.Write("{0}",element);
          }
      }    
      
      for (int row = 0; row < array.GetLength(0);row++){
          for (int col = 0; col < array.GetLength(1);col++){
              ..
          }
      }
  }
  ```

- 游长变元表：**params double[] numbers**

  ```c#
  public static double Average(params double[] numbers){
      double total = 0.0;
      foreach (double d in numbers){
          total += d;
      }
  }
  ```

- 命令行参数(string[] args)

  InitArray.exe 5 0 4

# 9 LINQ与泛型集合

- LINQ查询以from子句开始，指定**范围变量value**和要查询的**数据源values**。范围变量表示数据源中的每个项

- using System.Linq

- ```c#
  int values = {1,2,4,9,5,0,3};
  
  var filterd = 
      from value in values
      where value > 4//筛选
      select value;
  
  var sorted = 
      from value in values
      orderby value
      select value;//排序
  
  var sf = 
      from value in filterd
      orderby value descending
      selectc value;//从之前选出来的变量中逆序捕获
  
  var saf = 
      from value in values
      where value > 4
      orderby value descending
      select value;
  ```

- IEnumerable<int> result 类型的参数，只接受该接口的实现类，（数组和集合已经实现了IEnumerable<T>接口）

- string.Format("ddd {0:C}-{1:C} per month",4000,6000);

- 查询结果调用**Any**函数，看看返回值如果为真表示至少有一个元素

- 查询结果调用**First**方法，返回查询结果的第一个元素

- **Count**方法

- **匿名对象**：

  ```c#
  var names = 
      from e in employees
      select new {e.FirstName,Last = e.LastName};
  ```

  对所选属性制定新名称：Last = e.LastName;

  编译器创建匿名类型的时候，自动生成一个ToString方法

- 用泛型方法显示LINQ查询结果

  `public void Display<T> (IEnumerable <T> results)`

  foreach (T element in results)

- 集合简介

  List< T >类的常用属性与方法

  - Add
  - Capacity
  - Clear
  - Contains
  - Count
  - IndexOf
  - Insert(index,value)
  - Remove
  - RemoveAt
  - Sort
  - TrimExcess：将List的Capacity设置为List当前保存的元素个数

- List <string> items = new List<string>();

  items.Contains("red") ? string.Empty : "not"

- 可以用LINQ查询List

  ```c#
  List<string> items = new List<string>();
  
  var startWihR = 
      from item in items
      let upper = item.ToUpper()
      where upper.StartWith("R")//string的StarWith方法筛选
      orderby upper
      select upper;//一次定义，多次查询
  ```

- let声明一个新范围变量，可以对其赋值为一个表达式结果，对查询原先的范围变量进行操作

- LINQ的延迟执行deferred execution——查询只在访问结果的时候才执行而不是定义的时候查询执行。这样就可以一次创建查询，多次执行。


# 10 类与对象

```c#
return string.Format("{0}:{1:D2}:{2:D2} {3}",
                   ((hour == 0||hour == 12) ? 12 : hour%12)),
					minute,second,(hour < 12 ? "AM":"PM"));
```

D2：在不到两位数时添0

- **索引器**：可以像数组一样用索引访问元素清单。可以定义整数索引和非整数索引，可以让客户代码用字符串作为索引操纵数据，这个字符串表示数据项名称或描述。

  ```c#
  public class Box{
      private string[] names={"l","w","h"};
      private double[] dimensions = new double[3];
      
      public Box(double l,double w,double h){
          dimensions[0] = l;
          dimensions[1] = w;
          dimensions[2] = h;
      }
      //根据int访问索引器
      public double this[int index]{
          get{
              if( (index < 0)||(index > dimensions.Length))
                  return -1;
              else
                  return dimensions[index];
          }
          set{
              if(index >= 0 && index < dimensions.Length)
                  dimensions[index] = value;
          }
      }
      //根据string names访问
      public double this[string name]{
          get{
              int i = 0;
              while((i<names.Length)&&
                   (name.ToLower() != names[i]))//找到匹配的元素
                  ++i;
              return (i==names.Length)? -1:dimensions[i];//如果没有就返回-1
          }
          set{
              int i = 0;
              while((i < names.Length)&&
                   (name.ToLower() != names[i]))
                  ++i;
              if(i != names.Length)
                  dimensions[i] = value;
          }
      }
  }
  ```

  如何调用呢：像正常属性一样调用，但是形式是数组

  Console.WriteLine("box[0] = {0},box["w"] = {1}",box[0],box["w"]);

  box[0] = 10; box["w"] = 20;

- **重载构造函数**

  ```c#
  public Time() : this(0,0,0){}
  public Time(int h) : this(h,0,0){}
  public Time(int h,int m) : this(h,m,0){}
  public Time(int h,int m,int s){
      SetTime(h,m,s);
  }
  // 冒号和this，调用重载构造函数
  ```

- 对至少显式声明一个构造函数的类，编译器不生成默认构造函数。调用无参构造需要显式声明

- **Composition**：合成，引用，has - a

- **内存回收**与析构函数**destructor**：

  资源泄漏：如果管理资源的对象失去所有引用，而还没有显式释放资源，则程序不能再访问和释放这个资源，即产生了资源泄露

  CLR公共语言运行环境自动内存管理，用内存回收单元（garbage collector）释放对象不再需要的内存，其他对象可以使用。对象失去所有引用时，称为**析构**对象。每个对象有个特殊的成员叫**析构函数**：

  - 析构函数：由内存回收单元调用，在内存回收单元释放对象内存之前用于进行对象的终止整理工作。声明类似无参构造函数，在类名前面加代字号（~）

- **静态类成员**：静态变量表示类信息，类的所有对象共享同一数据，作用域是类

  ```c#
  public class Employee{
      private static int count = 0;
      public static int Count{//属性也要加 static
          get{
              return count;
          }
      }
  }
  ```

  - 静态方法不能直接访问非静态类成员，因为即使类对象不在，也可以调用静态方法
  - 静态方法中不能使用this引用，因为没有引用特定对象

- `private readonly int INCREMENT;`不用赋初值，可以在构造函数中给值

  `private const int PAI = 3;`需要赋初值，这两个都是不能改的。

- 抽象数据类型**ADT**包含两个概念：

  - 数据表达data representation
  - 数据允许的操作operation

  int、double、char类的类型都是抽象数据类型，实际上是在计算机系统中一定程度地近似表达实际中的概念

- 包访问**internal**访问：

  - 声明为internal的方法、实例变量和其他成员可以让同一汇编中的所有代码访问，其他汇编中的不行

    ```c#
    class InternalData{
        internal int number;
        internal string message;
    }
    public class MainClass{
        internalData.number = 77;
        internalData.message = "hello";
    }
    ```

  在同一编译单位就可以直接用

- **对象初始化器**：

  ```c#
  Time aTime = new Time{Hour = 14,Minute = 123,Second = 12};
  ```

  对象初始化器首先调用类的构造函数，然后对象初始化器将每个指定的属性设置为提供的值，没有写就是默认初始化值

- **扩展方法**：在现有的类中新增功能

  ```c#
  class Test{
      static void Main(string[] args){
          Time myTime = new Time();
          //隐式传入
          myTime.DisplayTime(myTime);
          Time timeAdded = myTime.AddHours(5);
          //显示传入
          TimeExtensions.DisplayTime(myTime);
      }
  }
  //扩展方法所在的类
  static class TimeExtensions{
      public static void DisplayTime(this Time aTime){//this 关键字对传入对象包装
          Console.WriteLine(aTime.ToString());
      }
      public static Time AddHours(this Time aTime,int hours){
          Time time = new Time();
          time.Minute = aTime.Minute;
          time.Second = aTime.Second;
          
          time.Hour = (aTime.Hour + hours) % 24;
          return time;
      }
  }
  ```

  反正就是对传入的对象进行包装扩展，前面加this关键字。传入的其他属性不用this

  - 如果扩展的类型定义了与扩展方法同名的实例方法，如果签名兼容，则实例方法会掩盖扩展方法

  - 全限定名调用时要制定扩展方法第一个参数的变元，类似于静态方法

    `TimeExtensions.DisplayTime(myTime);`

- 代理**Delegate**

  - 保存一个方法的引用
  - `public delegate bool NumberPredicate(int number);`存储任何取int变元和返回bool的方法引用
  - `private static List<int> FilterArray(int[] intArray,NumberPredicate predicate)`其中predicate这个参数可以接收之前指定的方法，并且可以调用`predicate(item);`

- **匿名方法**：

  ```c#
  delegate void NumberChange(int n);
  
  NumberChange nc = delegate(int x){
      Console.WriteLine("{0}",x);
  };
  ```

- **lambda**表达式

  - 可以定义简单的匿名函数，**匿名方法**

    `NumberPredicate evenPredicate = number => (number % 2 == 0);` 定义的时候根据goto的内容判断返回值类型

    `evenPredicate(4);` 调用的时候根据参数判断参数类型

    以上两句相当于之前的`NumberPredicate predicate = IsEven;`

  - 也可以当实参：

    `List<int> numberOver5 = FilterArray(numbers,`

    ​	`number => {return number > 5;})`

    形参还是之前那个定义`private static List<int> FilterArray(int[] intArray,NumberPredicate predicate)`，就可以直接传入

- **匿名类型**

  - 可以创建简单类，用于存储数据，不用编写类定义。
  - 匿名类型声明也称为匿名对象生成表达式
  - new 后面不指定类名，编译器根据表达式生成**新类定义**
  - 匿名属性：公用的、不可变的、只读的

  ```c#
  var bob = new {Name = "bob",Age = 37};
  bob.ToString();// {Name = bob, Age = 37}
  ```

  - 属性声明相同——相同类型；属性值也相同——相同对象
  - LINQ中的匿名类型

  ```c#
  var names = 
      from e in employees
      select new {e.FirstName,Last = e.LastName};
  				//隐式使用选中的属性名，除非另外指定
  ```

# 11继承

- 基类的protected成员可以让**基类**成员和**派生类**成员访问，而不必调用相应属性的set与get方法。（类成员也可以声明为protected internal）基类的**protected internal**成员可以由基类成员、派生类成员和同一汇编中的任何类访问。

- 任何派生类构造函数的第一个任务是调用直接基类的构造函数（显式或隐式，如果没有指定构造函数的调用），以保证正确地**初始化从基类继承的实例变量**。

- 用构造函数初始化器和关键字**base**调用基类构造函数：

  ```c#
  public class BaseBC : BC{
      private decimal bs;
      public BaseBC(int a,int b,int c,int bs) : base(a,b,c)
      {
          Bs = bs;
          
          Console.WriteLine("\nBs:\n"+ this);//构造方法中用this输出对象的字符串表示
      }
      
      public decimal BaseSalary{
          get{
              return baseSalary;
          }
          set{
              baseSalary = (value < 0) ? 0:value;
          }
      }
      
      public override decimal Earnings(){
          ...
      }
  }
  ```

- 将方法声明为**virtual**，可以让其子类的这个方法被重写，

  父类中：`public virtual decimal Earnings(){`

  ​			`return A*B;}`

  子类：

  ```c#
  public override decimal Earnings(){
      return Bs + base.Earnings();//不使用base.父类被重写方法，将会调用自己发生递归错误
  }
  ```

- Object类：

  - Equals()：比较两个对象的相等性。覆盖这个方法还要覆盖GetHashCode方法，保证相等对象具有相同的散列码，这个方法的默认实现只确定两个引用是否引用内存中同一对象。
  - Finalize：只在内存回收单元释放对象内存之前调用
  - GetHashCode
  - GetType
  - MemberwiseClone：试复制（shallow copy）建立所调用对象副本，实例变量复制到同一类型另一对象，引用类型只复制引用
  - ReferenceEquals：在两个对象是同一实例或是null引用才返回true，否则返回false

- **构造函数不继承**，但是即使没有构造函数，编译器为类隐式声明的默认构造函数也调用基类的默认或无参构造函数。

- ToString方法是特殊的，他是每个类直接或间接**从object继承的**

# 12

- 父类引用调用子类功能来调用派生类对象方法——调用的方法取决于实际引用的对象类型，而不是引用类型。（父类型变量可以引用子类型对象）

- 编译器允许父类赋予派生类变量，只要显式将基类引用转换为派生类类型——要通过向下转换技术显式将基类引用转换为派生类类型。A x <---- B  y。x = y / y = (B) x

- 抽象类与方法：抽象类需要作为基类被其他类继承，通常也把他称为”抽象基类“。

- **抽象类**的唯一用途是为其他类提供合适的基类，其他类可以**从它这里继承或实现接口**，从而共享共同设计

  - 抽象类声明用abstract。抽象方法声明`public abstract void Draw();`

  - 只要包含抽象方法，就要把这个类声明为抽象类，即使这个类中包含具体（非抽象）方法。

  - **属性也可以声明为abstract或virtual，然后在派生类中用override覆盖**，这样就使用抽象基类可以指定派生类的公共属性

    ```c#
    public abstract PropertyType MyProperty{
        get;
        set;
    }
    ```

    如果get和set方法都指定，则每个具体派生类要实现它们

    如果省略一个，子类也不能实现

  - 构造函数和静态函数不能声明为abstract，这些都不能被继承或实现

  - 可以用抽象基类声明变量，保存这些抽象类派生的任何具体类的对象引用——多态

  - 抽象基类中用abstract声明的方法，派生类中用override重写。

  - `if(抽象基类 is 子类)`，这个is，用于确定那个Employee对象是否为某一种特定的Employee类型，也适合于这种特定类型的派生类对象，因为派生类和基类存在“是”关系

  - 向下转型：BasePlusCommissionEmployee employee = (BasePlusCommissionEmployee ) currentEmployee; 课本380页

  - **var** employee = currentEmployee **as** BasePlusCommissionEmployee ; 如果不是BasePlusCommissionEmployee 类型，就返回null值。然后比较员工与null值，确定转换是否成功

  - GetType返回Type类的对象，包含对象类型信息，包括类名、共用方法和基类名

- 四种**将基类与派生类引用赋予基类与派生类变量**的方法

  - 基类引用赋予基类变量
  - 派生类引用赋予派生类变量
  - 派生类引用赋予基类变量是安全的，因为派生类对象是基类对象，但是这个引用只能引用基类成员
  - 避免基类引用赋予派生类变量产生的编译错误，需要显示地将基类引用转换成派生类类型。（向下转换）可以用is运算符保证只对派生类对象进行转换

- **sealed**（密封的）方法与类

  - 声明为virtual、override、abstract的方法才能在派生类中被覆盖
  - 基类中声明为sealed的方法不能在派生类中覆盖，声明为private的方法隐含sealed，但是派生类中可以声明与基类中专用方法同名的新方法
  - 声明为static的方法也隐含sealed。
  - **同时声明override与sealed的派生类**方法可以覆盖**基类方法**，但不能在继承层次的下层派生类中覆盖。
  - sealed方法声明不能改变，因此**所有派生类使用相同的方法实现**，调用sealed方法在编译时解析，称为静态绑定。
  - 编译器删除sealed方法调用，换成每个方法调用位置的拓展代码，称为**内联代码**
  - sealed类不能扩展，不能作为基类。
  - string类是sealed类，其中所有方法隐含为sealed

- **接口**

  - 接口声明从关键字**interface**开始，只能包含抽象方法、属性、索引器和事件
  - 所有**接口成员**隐式声明为**public**和**abstract**，每个接口可以扩展一个或多个其他接口

  - 实现接口的**具体类**要声明**接口声明中**指定了签名的每个接口成员

  - 实现接口就像与编译器签订一个协议，我会提供接口指定的**所有成员的实现**或将其声明为**abstract**

  - 不允许多继承，允许多实现，实现的多个接口用逗号隔开

    ```c#
    public interface IPayable{
        decimal GetPaymentAmount();
    }
    class Invoice : IPayble{
        //实现
        public decimal GetPaymentAmount(){
            return 1.1;
        }
        //不实现
        public abstract decimal GetPaymentAmount();
    }
    ```

- .net公共接口

  - IComparable，重写CompareTo方法
  - IComponent：定义组件要实现的行为
  - IDisposable：由提供显式资源释放机制的类实现。Dispose方法可以显式调用，释放资源
  - IEnumerator：用于一次一个元素地对集合/数组迭代

- 运算符重载

  - 关键字operator加运算符表示这个方法充在指定运算符

  ```c#
  public class ComplexNumber{
      public double Real{get;private set;}
      public double Imaginary{get;private set;}
      //默认构造
      public ComplexNumber(double a,double b){
          Real = a;
          Imaginary = b;
      }
      
      //运算符重载，对两个对象的+进行处理，掉用构造函数
      public static ComplexNumber operator +(
          ComplexNumber x, ComplexNumber y){
          return new ComplexNumber(x.Real+y.Real,
                                  x.Imaginary+y.Imaginary);
      }
      //其他的同理，但是方法头必须是 public static
  }
  
  x = new ComplexNumber(1.1,2.2);
  y = new ComplexNumber(3.1,2.2);
  
  x+y;//这个就可以被识别了，编译器知道对两个对象如何相加
  ```

- 派生类drived class、内联代码inlining code、late bingding后绑定、

# 13异常处理

- stack trace：堆栈踪迹：异常名+异常路径，列出一个个方法。堆栈踪迹中的第一个at行表示异常抛出点——发生异常的初始点
- 在catch的参数列表中可以只显示异常类型，不用写参数名。这代表我们声明了变量，但没有在catch块中使用。

```c#
public partial class DivideByZeroTestForm : Form{
    //partial表示把一个类放在多个地方
    public DivideByZeroTestForm(){
        InitializeComponet();
    }
    
    private void divideButton_Click(object sender,EventArgs e){
        outputLabel.Text = "";
        try{
            int num = Convert.ToInt32(numTextBox.Text);
            int den = Convert.ToInt32(denTextBox.Text);
            
            int res = num/den;
            
            outputLabel.Text = res.ToString();
        }catch(FormatException){
            MessageBox.Show("","",MessageBoxButtons.OK,MessageBoxIcon.Error);
        }catch(DivideByZeroException param){ 
            																		MessageBox.Show(param.Message,"",MessageBoxButtons.OK,MessageBoxIcon.Error);
        }
    }
}
```

- bool isSuccess = Int32. TryParse(string , res); 第一个是需要转换的字符串，第二个是存储转换结果的int变量，返回是否转换成功
- 通用catch块：catch块不指定异常类型或标识符，捕获所有的异常类型。try块后面至少要有一个catch块或finally块。
- 运行环境发现未捕获异常，程序暂停，出现异常助理窗口，显示异常发生在哪里、异常类型和异常处理的信息链接。
- **异常处理终止模型**：处理异常后，程序控制不返回抛出点，因为已过期，控制转换到最后一个catc块之后。
- 异常处理恢复模型resumption：while循环不断重复直到不出异常
- try块：try后面的代码块、try语句：从try开始到最后一个catch与finally块的所有代码
- 通常，处理需要显示释放的资源时会发生异常——finally中放上相应try块所请求和操纵的资源的资源释放代码
- 如果try块相关联的catch没有捕获异常，或try块相关联的catch块本身抛出异常，则finally块执行之后才由外层try块处理这个异常。
- try块中的局部变量不能在finally块中访问，因此要在try块和相应finally块中访问的变量要在try之前声明

- **using语句**可以简化取得资源、在try块中使用资源和在相应finally块中释放资源的代码

```c#
using (ExampleObject exampleObject = new ExampleObject()){
    exampleObject.SomeMethod();
    //ExampleObject类实现IDisposable接口
}
//等价于
{
    ExampleObject exampleObject = new ExampleObject();
    try{
        exampleObject.SomeMethod();
    }finally{
        if(exampleObject != null)
            ((IDisposable) exampleObject).Dispose();
    }
}
```

- Exception类的属性

  - Message：与Exception对象相关联的错误信息
  - StackTrace：包含的字符串表示方法调用堆栈
  - InnerException：在catch块中创建新的异常对象用，将原先的异常作为构造函数的变元传入，原先的异常对象就变为新的异常对象的InnerException。这个可以获取原异常的引用

  ```c#
  try{
      Convert.ToInt32("not an integer");
  }catch(FormatException param){
      throw new Exception("excepiton occurred in hhh",param);//param就相当于
  }
  ```

  

- **堆栈反转**unwinding：特定作用域中发生异常而没有捕获时，方法调用堆栈反转，在外层try块中捕获异常

- 用户定义异常类：

  - 直接或间接继承Exception类（p476）

# 14

### 简单事件驱动GUI

自动生成代码

```c#
using System;
using System.Windows.Forms;

namespace Example
{
    //partial修饰符，让这个类可以分解到多个文件中
	public partial class ExampleForm : Form
    {
        //默认构造函数
        public ExampleForm(){
            InitializeComponet();
        }
        
        private void exampleButton_Click(object sender,EventArgs e)
        {
        	MessageBox.Show("Button was clicked.");    
        }    
    }
}
```

创建一个Form窗体，改变Name属性为ExampleForm。将Button组件拖入ExampleForm中，在属性窗口中，改变Name属性为exampleButton，Text属性为。。双击button，跳转到点击事件函数

**事件处理器参数：**

- **object** sender ：引用产生事件的对象
- **EventArgs** e ：事件变元对象的引用，包含所发生时间的其他信息。

### 14.3.3 代理与事件处理机制

- 事件处理器通过所谓delegate的特殊对象连接**控件事件**，**代理保存一个方法的引用**，方法签名由代理类型的声明指定。

- 按钮单击事件的代理类型EventHandler，返回void,接受两个参数

  `public delegate void EventHandler (Object sender, EventArgs e);`

- **表示代理要调用的方法**：事件发送者调用代理对象时，就像调用一个方法，双击按钮控件，VS增加代理

  `new System.EventHandler(this.exampleButton_Click);`——创建EventHandler代理对象并用exampleButton_Click方法将其初始化。

  `this.exampleButton.Click += new System.EnentHandler(this.exampleButton_Click);`

  将代理加进按钮单击事件，使用`+=`运算符

- 多播代理使一个事件可以调用多个方法

- 默认时间以外的控件事件如何创建事件处理器：

  - 用属性窗口创建：单击属性窗口的Events图标
  - 一个方法可以处理多个控件的多个事件，三个按钮的Click事件可以用同一方法处理，可以对多个事件指定一个事件处理器，只要在属性窗口中选择一个方法和多个控件。

## 14.4 控件属性与布局

### Form属性、方法与事件

- AccpetButton：按enter键时单击的按钮
- AutoScroll：布尔值
- CancelButton：按Escape键时单机的按钮
- FormBorderStyle：FixedSingle时，窗体固定
- Font
- Text

方法：

- Close方法：关闭窗体，释放资源
- Hide：隐藏窗体，不破坏窗体和释放资源
- **Show**：显示隐藏的窗体

事件：

- Load，在显示窗体前发生

---

### 控件的Control父类常见属性

- Enable

- Focused：是否有焦点

- TabIndex：控件跳表顺序

- TabStop：true表示可以Tab把焦点放到控件上

- ForeColor：控件前景颜色，确定Text属性中文本的颜色

- Text

- Visable

方法

- Hide 隐藏控件（Visible：true）
- Select获得焦点，使其变成活动控件
- Show显示控件（Visible：false）

---

Archor：锚点使控件与容器边界保持固定距离：Bottom,Right

Dock：把控件连接到容器上，使控件沿整个边伸展

以上两个属性都是将对于父容器设置，可能是窗体或面板

Padding：容器边与停靠控件的间距

MinimumSize，MaximumSize

设置窗体尺寸固定：

- MiniumuSize、MaximumSize为相同值
- FormBorderStyle属性设置为FixedSingle

---

### Label类（Control的派生类）常见属性：

Font

Text

TextAlign属性：label文本与空间的对齐方式——水平和垂直



### TextBox：

- AcceptsReturn：true在多行文本框中另起新行，如果是false，按enter就相当于触发窗体上按AccpetButton属性指定的按钮
- Multiline：true表示文本框跨多行
- UseSystemPasswordChar：true，文本框变成口令文本框
- ReadOnly
- ScrollBars：对多行文本框，这个属性表示显示哪个滚动条

---

### Button：

- FlatStyle：外观
  - Flat（按钮不显示三维样子）
  - Popup（按钮先显示平面，用户将鼠标指针移到按钮上时再弹出）
  - Standard（三维）
  - System（系统控制）

- Text

---

Label、TextBox的属性**BorderStyle**都可以改为 Fixed3D

---

### GroupBox和Panel的区别：GroupBox可以显示标题而没有滚动条。

- GroupBox属性：
  - Controls：组框包含的一组控件
  - Text：指定组框顶部显示的标题文本
- Panel属性
  - AutoScroll：默认false
  - BorderStyle：None、Fixed3D、FixedSingle
  - Controls
- 要将控件加入GroupBox或Panel，需要调用每个控件的Controls属性的Add方法，这个是在                     `类名.Designer.cs`的部分类中

---

### 复选框、单选框：

- 和Button类一样，CheckBox和RadioButton类也是从`ButtonBase`派生的

- CheckBox复选框

  属性

  - Appearance：Normal，设置为Button时显示为按钮
  - Checked：返回布尔值
  - **CheckState**：返回枚举值（Checked、Unchecked、Indeterminate：显示阴影）
  - Text
  - ThreeState：默认false，改为true时有三状态，中间状态只能由程序设置

  事件

  - **CheckedChanged**：改变Checked属性时产生
  - CheckStateChanged：改CheckState
  
- 字体异或运算：

```c#
public partial class CheckBoxTestForm : Form{
    public CheckBoxTestForm(){
        InitializeComponent();
    }
    
    private void boldCheckBox_CheckedChanged(object sender,EnentArgs e){
        outputLabel.Font = new Font( outputLabel.Font,
                                   outputLabel.Font.Style ^ FontStyle.Bold);
        //第一个参数是原先的字体与自豪
        //第二个为枚举类型样式 FontStyle枚举成员指定
    }
    
    //逻辑异或运算 ^ 可以组合样式和取消现有样式设置
    private void italicCheckBox_CheckedChanged(object sender,EnentArgs e){
        outputLabel.Font = new Font( outputLabel.Font,
                                   outputLabel.Font.Style ^ FontStyle.Italic);
    }
}
```

- RadioButton：加进容器的所有单选钮成为同一组
  - Checked
  - Text
  - CheckedChanged
- p441例子

```c#
public partial class RadioButtonsTestForm:Form{
    private MessageBoxIcon iconType;
    private MessageBoxButtons buttonType;//都是预定义类型
    
    //到时候取得时候直接使用枚举常量如 MessageBoxButtons.OK
    
    //组框判断哪个按钮被选了
    private void iconType_CheckedChanged(object sender,EventArgs e){
        if(sender == errorRadioButton)
            iconType = MessageBoxIcon.Error;
    }
    
    //
    DialogResult result = MessageBox.Show("This is your MessageBox.",
                       "hh MessageBox",buttonType,iconType,0,0);
    					//0,0表示与父窗口位置
}
```

### 图形框PictureBox

属性

- Image
- SizeMode：枚举值，取值为
  - Normal图像框左上角
  - StretchImage根据图像框缩放图形
  - AutoSize根据图形缩放图相框
  - CenterImage、Zoom：将图形放到中央

事件

- Click

如何添加资源

1. 创建工程后双击解决资源方案管理器中的Properties节点打开工程属性
2. 单击Resources标签
3. 单击添加资源旁边的向下箭头，选择添加现有文件，将资源加入对话框
4. 即可在Resources文件中看到

工程的资源放在Resources类中，除工程资源还包含ResourcesManager对象，要访问一个图形，可以使用GetObject方法，其变元为资源名，返回资源对象

```c#
imageNum = (imageNum + 1)%3;
iamgePictureBox.Image = (Image)(Propertites.Resources.ResourcesManager.GetBoject(
	string.Format("image{0}",imageNum)));
```

**(Image)(Propertites.Resources.ResourcesManager.GetBoject("name"));**



Resources类还可以直接访问用表达式Resources.resoucesName定义的资源，例如Properties.Resources.image0表示第一个图形的Image对象

### 工具提示ToolTip

属性

- AutoPopDelay：提示显示多少毫秒
- InitialDelay：放多久毫秒出现提示
- ReshowDelay：两个工具提示间的时间量

常见事件

- Draw：显示工具提示发出时，可以用这个事件修改工具提示外观

从工具箱中加入**工具提示组件**时，其在组件价中显示。工具提示加进窗体后，**其他空间的属性窗口**出现一个新属性**ToolTip on label1**，可以改他的值修改提示的文本内容

### 数字上下控件NumericUpDown

属性

- DecimalPlaces：指定控件中显示多少位数
- Increment：decimal
- Maximum
- Minimum
- UpDownAlign：这些按钮放在左边或右边
- Value

### 鼠标事件

事件变元类型为EventArgs：

- MouseEnter
- MouseLeave

事件变元为**MouseEventArgs**的鼠标事件

- MouseDown
- MouseHover：光标位于控件边界内
- MouseMove
- MouseUp

**MouseEventArgs**类属性：

- Button：指定按下的鼠标按钮（Right、Left、Middle）
- Clicks：鼠标单击次数 `if (e.Button == MouseButtons.Left)`
- X
- Y

```c#
using (Graphics graphics = CreateGraphics()){
    graphics.FillEllipse(
    	new SolidBrush(Color.BlueViolet),e.X,e.Y,4,4);
}
```

### 键盘事件

- 变元为**KeyEventArgs**类型的键盘事件：
  - KeyDown：按下时产生
  - KeyUp：放开时产生

- **KeyEventArgs**类型的属性：

  - Alt	e.Alt ? "yes":"no"

  - Control

  - Shift

    是否按下他们

  - Handled：表示是否处理事件

  - KeyCode，用**keys枚举值**，不包括修饰键信息 H

  - KeyData，与**修饰键信息组成Keys值** H,Shift

  - KeyValue，返回键码的**int值**而不是Keys枚举值 72

  - Modifiers：返回一个**Keys值**，表示按下的修饰键

- **KeyPressEventArgs**类型的键盘事件

  - KeyPress：不指定发生键事件时是否按下修饰键。按下键时产生，出现在KeyDown之后，KeyPress之前

- 类**KeyPressEventArgs**属性

  - KeyChar：返回键击的ASCII字符：e.KeyChar
  - Handled：标识是否处理KeyPress事件

# 15

### MenuStrip

- 要创建菜单，打开工具箱并将MenuStrip控件拖动到窗体上。要将菜单项加入菜单中，单击TypeHere文本框并输入菜单项名称这样就在菜单中加进类型为**ToolStripMenuItem**的项目
- 要加快捷键：&File。要显示和号，输入&&。要加入菜单项的另一个快捷键，设置相应**ToolStripMenuItems**的**ShortcutKeys属性**，选择修饰键，再选择Key
- 属性
  - Items属性：设置顶级菜单
  - HasChildren
  - RightToLeft
- ToolStripMenuItem属性——顶级菜单项
  - Checked
  - CheckOnClick
  - Index
  - **DropDownItems**
  - ShortcutKeyDisplayString，快捷键旁边显示的文本
  - ShortcutKeys：
  - Text
- ToolStripMenuItem事件——Click



### MonthCalendar控件

属性

- FirstDayOfWeek：日历中每周先显示星期几
- MaxDate
- MaxSelectionCount

### DateTimePicker控件

- dateTimePicker的Value值用`DateTime`类型接收

- Format属性如果设置为Long，用户选择日期，不能选择时间

  - Long ： 年月日
  - Short：2019/11/28
  - Time：17:44：08

- dateTimePicker.MinDate = DateTime.Today

  dateTimePicker.MaxDate = DateTime.Today.AddYears(1);

### LinkLabel控件

- LinkArea：哪部分文本是链接
- linkLabel的事件处理器调用Process的Start方法，可以从程序中执行另一程序
- LinkVistited属性设置为true表示被访问过
- 逐字字符串(verbatim string) @C：\

```c#
private void linkLabel_LinkClicked(object sender,LinkLabelLinkClickedEventArgs e){
    linkLabel.LinkVisited = true;
    System.Diagnostics.Process.Start(@"C:\");
    System.Diagnostics.Process.Start("http://www.deitel.com");
    System.Diagnostics.Process.Start("notepad");
}
```

### ListBox

属性：

- Items：项目集合
- MultiColumn：是否可以分成多列
- SelectedIndex：返回所选项目的索引，如果没有就返回-1
- SelectedIndices
- SelectedItems
- SelectionMode
- Sorted

方法：

- ClearSelected
- GetSelected：取索引变元

事件：

SelectedIndexChanged

---

myListBox.Items.Add(myListItem);，也可以调用AddRange方法添加对象数组

displayListBox.Items.RemoveAt(displayLlistBox.SelectedIndex);

Application.Exit();

### ChecedListBox控件

属性

- SelectionMode：None代表不选择，One代表多选
- CheckedItems
- CheckedIndices
- CheckOnClick：False点两下确认或者取消，True点一下确认或取消

事件

`private void checkedListBox1_ItemCheck(object sender, ItemCheckEventArgs e)`

**ItemCheckEventArgs**  e 的属性

- CurrentValue：Checked、Unchecked、Indeterminate
- Index：
- NewValue：指定项目新CheckState状态值

```c#
private void checkedListBox1_ItemCheck(object sender, ItemCheckEventArgs e)
{
    string item = checkedListBox1.SelectedItem.ToString();
    if (e.NewValue == CheckState.Checked)
        listBox1.Items.Add(item);
    else
        listBox1.Items.Remove(item);
}
```

### ComboBox控件

DropDownStyle：Simple显示滚动条，DropDown显示向下箭头

Items

MaxDropDownItems：指定下拉清单可以显示的最大项目数

SelectedIndex

SelectedItem

Sorted

事件：SelectedIndexChanged事件

```c#
Graphics myGraphics = base.CreateGraphics();
Pen myPen = new Pen(Color.DarkRed);
SolidBrush mySolidBrush = new SolidBrush(Color.DarrkRed);
myGraphics.Clear(Color.White);
myGraphics.DrawEllipse(myPen,50,50,150,150);
myGraphics.FillRectangle(mySolidBrush,50,50,150,150);

myGraphics.Dispose();
```

### TreeView

TreeView中的节点是TreeNode类的实例

- Nodes属性：TreeNode集合清单，包含Add、Clear、Remove
- SelectedNode：选择合适的节点
- CheckBoxes：表示节点旁边是否显示复选框

TreeNode

- Checked
- FirstNode
- FullPath
- Nodes
- PrevNode，上一个同胞节点

方法

- Collapse缩合节点
- Expand展开节点
- ExpandAll
- GetNodeCount

`treeView.Nodes[myIndex].Nodes.Add(new TreeNode(childLabel));`

- Directory.GetDirectories(directoryValue);
- Directory.Exist(inputText.Text)

### ListView可以在清单项目旁边显示图标

- Activation：用户如何激活项目，取值为ItemActivation枚举，OneClick、TwoClick、Standard
- CheckBoxex：旁边是否有复选框
- Items：返回空间中的ListViewItem集合
- View：ListViewItem的样子，取值为LargeIcon、SmallIcon、List、Details、Tile

ListView可以定义图像，作为项目内容。需要ImageList组件。

把ListView的SmallImageList设置为新的ImageList对象

Directory.GetCurrentDirectory();



### TabControl控件

首先将控件加进TabPage对象，然后将TabPage加入TabControl控件

`myTabPage.Controls.Add(button);`

`myTabControl.TabPages.Add(myTabPage);`

在TabControl上右键单击Add Tab就可以加选项卡啦

单击事件Click

### MDI

要创建MDI窗体，创建新窗体并把他的`IsMdiContainer`属性设置为true

子窗体加入父窗体：创建新的Form对象，将其MdiParent属性设置为父窗体，调用子Form对象的Show方法

MDI窗体方法

- LayoutMdi：MdiLayout枚举，ArrageIcons、Cascade、TileHorizontal、TileVertical

MDI子属性

- IsMdiChild
- MdiParent

MDI夫属性

- ActiveMdiChild
- IsMdiContainer
- MdiChildren：返回MDI子窗体数组