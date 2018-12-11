# C#基础
## 面向对象编程
* 为了让编程更加清晰，把程序中的功能进行模块化划分，每个模块提供特定的功能，而且每个模块都是孤立的，这种模块化编程提供了非常大的多样性，大大增加了重用代码的机会
* 类实际上是创建对象的模板，每个对象都包含数据，并提供了处理和访问数据的方法。
* 类定义了类的每个对象（称为实例）可以包含什么数据和功能
* 类中的数据和函数称为类的成员

```C#
using System;
using System.Collections.Generic;
using System.Text;
//通过class创建了一个类，并且声明该类的属性
namespace _003_面向对象编程
{
    public class Shell//定义类
    {
        //数据成员：里面包含了四个字段
        public float thearyspeed;
        public float caliber;
        public float blastlength;
        public float time;
        //函数成员：里面包含了一个方法
        public void print()
        {
            Console.WriteLine("理论速度 " + thearyspeed + "m/s");
            Console.WriteLine("炮弹口径 " + caliber + "mm");
            Console.WriteLine("爆炸参数 " + blastlength + "");
        }
    }
}
```
* 通过上面创建的类来声明一个具有该类所有属性的对象

```C#
using System;
namespace _003_面向对象编程
{
    class Program
    {
        static void Main(string[] args)
        {
            //如果要使用一个类的话，要先引入它所在的命名空间，因为customer位于当前的命名空间下，所以不需要引入，我们可以直接使用customer
            Shell tigerap = new Shell();//声明一个shell类并且初始化
            tigerap.thearyspeed = 700;//访问该类里面的值并且赋值
            tigerap.caliber = 88;
            tigerap.blastlength = 1;
            tigerap.print();//访问该类里面的方法
            Console.ReadKey();
        }
    }
}
```
## 类的定义与声明
* 创建一个类，在类中声明一些私有变量，通过set方法让外界可以访问

```C#
using System;
using System.Collections.Generic;
using System.Text;
namespace _004_类的定义与声明
{
    class Vector3
    {
        //编程规范上，习惯把所有的字段设置为private，只可以在类内部访问，不可以通过对象访问
        private float x, y, z;
        //为字段提供Set方法，来设置字段的值
        public void SetX(float x)//外界可以通过调用这个方法来访问类中的x字段
        {
            this.x = x;
        }
        public void SetY(float y)
        {
            //如果我们直接在方法内部访问同名的变量的时候，优先访问最近（形参）
            //我们可以通过this.表示访问的是类的字段或者方法
            this.y = y;
        }
        public void SetZ(float z)
        {
            this.z = z;
        }
        public float Length()
        {
            return MathF.Sqrt(x * x + y * y + z * z);
        }
    }
}
```
```C#
using System;
namespace _004_类的定义与声明
{
    class Program
    {
        static void Main(string[] args)
        {
            Vector3 vector3 = new Vector3();
            vector3.SetX(1);//通过SetX方法访问类中的x变量并且赋值
            vector3.SetY(1);
            vector3.SetZ(1);
            float i = vector3.Length();
            Console.WriteLine(i);//1.732051
            Console.ReadKey();
        }
    }
}
```
## 构造函数
* 在构造对象的时候，对象的初始化过程是自动完成的，但是在初始化对象的过程中有的时候需要做一些额外的工作，例如需要初始化对象存储的数据，构造函数就是用于初始化数据的函数。
* 声明基本的构造函数的语法就是声明一个和所在类同名的方法，但是该方法没有返回类型。
* 当我们使用new关键字创建类的时候，就会调用构造方法。
我们一般会使用构造方法进行初始化数据的一些操作。
构造函数可以进行重载，跟普通函数重载是一样的规则
* 当我们不写，任何构造函数的时候，编译器会提供给我们一个默认的无参的构造函数，但是如果我们定义了一个或者多个构造函数，编译器就不会再提供默认的构造函数

```C#
//在之前的类里面填加一个构造函数
public Vector3(float x,float y,float z)
{
    //我们定义了一个构造函数，那么编译器不会为我们提供构造函数了
    this.x = x;
    this.y = y;
    this.z = z;
    float length = Length();
}
```
```C#
//通过类声明一个对象
Vector3 vector3 = new Vector3(1, 1, 1);//直接把值传递给构造函数
```
## 属性
```C#
//属性的定义结构
public int MyIntProp{
	get{
		// get code
	}
	set{
		//set code
	}
}
```
* 定义属性需要名字和类型
* 属性包含两个块 get块和set块
* 访问属性和访问字段一样，当取得属性的值的时候，就会调用属性中的get块，所以get块，类型需要一个返回值就是属性的类型；当我们去给属性设置值的时候，就会调用属性中的set块，我们可以在set块中通过value访问到我们设置的值。

```C#
//定义属性
public float X//也可以叫get，set方法
{
    //可以在get或者set块前面加private使这个块变成私有的，只能在类内部调用
    get//通过get访问x的值
    {
        return x;
    }
    set//通过set块给x赋值
    {
        x = value;
    }
    //如果只有get或者set中的一个块，那么调用该方法只能实现赋值或者访问中的一种功能
}
```
```C#
Vector3 vector3 = new Vector3(1, 1, 1);//直接把值传递给构造函数
vector3.X = 2;//可以通过调用X方法来改变或者访问x字段
Console.WriteLine(vector3.X);//2
```
* 给一个私有字段添加get，set块，并且不给里面添加内容，编译器会自动生成一个字段，并且外界也可以给这个私有字段赋值或者访问

```C#
private float Y { get; set; }//编译器会自动给我们提供一个字段，来存储Y
```
## 匿名类型
```C#
var a = 2432;//var可以声明各种类型的变量
a = 241.321;//，但是每一个类型一旦确定就不能更改,所以这一行会报错
var m = "akgahb";
var b = false;
```
## 堆和栈
* 栈空间比较小，但是读取速度快
* 堆空间比较大，但是读取速度慢

### 栈的特征：
* 数据只能从栈的顶端插入和删除
* 把数据放入栈顶称为入栈（push）
* 从栈顶删除数据称为出栈（pop）

### 堆的特征
* 堆是一块内存区域，与栈不同，堆里的内存能够以任意顺序存入和移除

## 值类型和引用类型在内存中的存储
```C#
using System;
namespace 值类型和应用类型在内存中的存储
{
    class vector3
    {
        public int x;
        public int y;
        public int z;
    }
    class Program
    {
        static void Main(string[] args)
        {
            text1();
            text2();
            text3();
            text4();
            text5();
            Console.ReadKey();
        }
        static void text1()
        {
            int num1 = 34;//整数类型属于值类型，直接存储在栈空间
            int num2 = 34;//栈空间比较小，但是读取速度快
            int temp = 334;//栈的特征： 数据只能从栈的顶端插入和删除   把数据放入栈顶称为入栈（push）   从栈顶删除数据称为出栈（pop）
        }
        static void text2()
        {
            int num1 = 34;
            int num2 = 345;
            char num = 'a';//字符类型属于值类型，存储在栈空间
            string name = "liuyongchao";//字符串类型属于引用类型，需要两段内存 第一段存储实际的数据，它总是位于堆中  第二段是一个引用，指向数据在堆中的存放位置
        }
        static void text3()
        {
            string name1 = "liuyongchao";
            string name2 = "china";
            name2 = name1;//此时name2为liuyongchao，name1不变
            name2 = "chinese";//此时name2为chinese，name1不变
            Console.WriteLine(name1 + "   " + name2);//liuyongchao   chinese
        }
        static void text4()
        {
            vector3 vector1 = new vector3();//自定义的类属于引用类型
            vector3 vector2 = new vector3();
            vector1.x = 1;
            vector1.y = 2;
            vector1.z = 3;
            vector2.x = 100;
            vector2.y = 200;
            vector2.z = 300;
            vector2 = vector1;//vector1和vector2指向堆中相同的存放位置的数据
            vector2.x = 123;//修改了vector1和vector2共同指向的堆中的存放位置的数据
            Console.WriteLine(vector1.x);//123
        }
        static void text5()
        {
            vector3[] array = new vector3[] { new vector3(), new vector3(), new vector3() };//数组是引用类型，如果数组是一个值类型的数组（数组中存储的是值类型），那么数组中直接存储值，如果是一个引用类型的数组（数组中存储的是引用类型），那么数组中存储的是引用（内存地址）
            vector3 vector = array[0];
            array[0].x = 100;
            vector.x = 200;
            Console.WriteLine(array[0].x);//200
        }
    }
}
```
# 如果有不足的地方，欢迎指教
