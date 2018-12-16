# c#基础
## 继承
### 实现继承
* 表示一个类型派生于一个基类型,它拥有该基类型的所有成员字段和函数。在实现继承中,派生类型采用基类型的每个函数的实现代码,除非在派生类型的定义中指定重写某个函数的实现代码。在需要给现有的类型添加功能,或许多相关的类型共享一组重要的公共功能时,这种类型的继承非常有用。

### 接口继承
* 表示一个类型只继承了函数的签名,没有继承任何实现代码。在需要指定该类型具有某些可用的特性时,最好使用这种类型的继承。

### 实例
* 下面声明一个父类

```C#
using System;
using System.Collections.Generic;
using System.Text;
namespace _007_面向对象编程_继承
{
    class Enemy//创建一个父类，并且创建一些父类的字段和方法
    {
        private int hp;
        private int level;
        public int HP
        {
            get { return hp; }
            set { hp = value; }
        }
        public int Level
        {
            get { return level; }
            set { level = value; }
        }
        public void AI()
        {
            Console.WriteLine("这里是AI方法");
        }
    }
}
```
* 下面的子类继承自上面的父类

```C#
using System;
using System.Collections.Generic;
using System.Text;
namespace _007_面向对象编程_继承
{
    class Boss:Enemy//继承至父类Enemy，可以使用Enemy的所有公有的函数和数据
    {
        public void Attack()
        {
            Console.WriteLine("Boss开始攻击");
        }
    }
}
```
* 在主函数中使用子类

```C#
using System;
namespace _007_面向对象编程_继承
{
    class Program
    {
        static void Main(string[] args)
        {
            Boss boss = new Boss();//用子类Boss定义的对象，可以调用父类的所有公有的函数和数据
            boss.AI();//继承：父类里面所有的数据成员和函数成员都会继承到子类里面
            boss.Attack();
            boss.HP = 100;
            Console.WriteLine(boss.HP);//100
        }
    }
}
```
* 下面是子类和父类的互相转换关系

```C#
Enemy enemy;
enemy = new Boss();//用父类声明的对象，可以通过子类进行构造，子类声明的对象不可以使用父类构造
//enemy虽然使用父类进行了声明，但是使用了子类构造，所以本质上是一个子类类型的，我们可以通过强制转换转换成子类类型
Boss boss = (Boss)enemy;//可以通过强制转换执行
```
```C#
Enemy enemy = new Enemy();
Boss boss = (Boss)enemy;//一个对象是什么类型的，主要是看它是通过什么构造的，这里enemy使用了父类的构造函数，所以只有父类中的字段和方法，不能被强制转换成子类
```
## 虚方法
* 把一个父类函数声明为virtual,就可以在任何子类中重写该函数

```C#
class Enemy
{
	public virtual void Move()//virtual关键字表示这是一个虚方法，可以在子类中重写
    {
        Console.WriteLine("这里是移动方法");
    }
}
```
* 在子类中重写另外一个函数时，要使用override关键字显示声明

```C#
class Boss:Enemy
{
    public override void Move()//override表示这是一个重写的方法,如果使用new就会将同名的父类方法隐藏
    {
        Console.WriteLine("这里是Boss的移动方法");
    }
}
```
* 在主函数中使用虚方法

```C#
static void Main(string[] args)
{
    Boss boss = new Boss();
    boss.Move();//子类定义的对象使用子类中重写后的方法
    Enemy enemy = new Enemy();
    enemy.Move();//父类定义的对象使用的父类中原有的虚方法
}
```
## 隐藏方法
* 如果名字相同的方法在基类和派生类中都进行了声明，但是该方法没有分别声明为virtual和override，派生类就会隐藏基类方法。
* 
* 父类

```C#
class Enemy
{
	public void AI()
    {
        Console.WriteLine("这里是AI方法");
    }
}
```
* 子类

```C#
class Boss:Enemy
{
    public new void AI()//在写隐藏方法时，可以不加new关键字
    {
        Console.WriteLine("这里是Boss的AI方法");
    }
}
```
* 在主函数使用隐藏方法（使用虚方法时，通过子类构造的对象只能使用子类中重写后的方法，不能使用在父类中的原方法。使用隐藏方法时，既可以使用在父类中被隐藏的方法，也可以使用在子类中重写的方法）

```C#
Boss boss = new Boss();
boss.AI();//通过子类声明的对象使用子类的隐藏方法
Enemy boss1 = new Boss();
boss1.AI();//通过父类声明的对象使用父类的隐藏方法
```
## this和base关键字的作用
* this可以访问当前类中定义的字段,属性和方法，有没有this都可以访问，有this可以让IDE-VS编译器给出提示，另外当方法的参数跟字段重名的时候，使用this可以表明访问的是类中的字段，base可以调用父类中的公有方法和字段,有没有base都可以访问，但是加上base.IED工具会给出提示，把所有可以调用的字段和方法罗列出来方便选择

## 抽象方法
* C#允许把类和函数声明为 abstract。 抽象类不能实例化,抽象类可以包含普通函数和抽象函数，抽象函数就是只有函数定义没有函数体。 显然,抽象函数本身也是虚拟的Virtual(只有函数定义，没有函数体实现)。
* 类是一个模板，那么抽象类就是一个不完整的模板，我们不能使用不完整的模板去构造对象。 
* 创建一个抽象的父类

```C#
namespace _007_面向对象编程_继承
{
    abstract class Tank//abstract关键字代表这是一个抽象类
    {
        public float thearyspeed;
        public float truespeed;
        public abstract void attack();//abstract关键字代表这是一个抽象方法，抽象方法所在的类一定是抽象类，抽象方法需要重写
    }
}
```
* 创建一个子类继承该抽象类，并且重写类里面的抽象方法

```C#
namespace _007_面向对象编程_继承
{
    class Tiger:Tank//当继承了一个抽象类是，必须重写该抽象类的抽象方法
    {
        public override void attack()//使用override关键字重写抽象方法
        {
            Console.WriteLine("这里是重写的坦克攻击方法");
        }
    }
}
```
* 在主函数中使用这个类

```C#
static void Main(string[] args)
{
    Tank tank = new Tiger();//可以使用抽象类声明对象，但是不能使用抽象类构造对象
}
```
## 密封类和密封方法
* C#允许把类和方法声明为sealed。对于类,这表示不能继承该类；对于方法表示不能重写该方法。

```C#
namespace _008_密封类和密封方法
{
    sealed class BaseClass//密封类不能被继承
    {
        public void Move()
        {
        }
    }
}
```
```C#
namespace _008_密封类和密封方法
{
    class BaseClass
    {
        public virtual void Move()//密封方法不能直接写，只能在重写方法的时候写，所以只能在父类中写虚方法，然后在子类中重写成密封方法
        {
        }
    }
}
```
```C#
namespace _008_密封类和密封方法
{
    class Class1: BaseClass//sealed密封方法无法被继承
    {
        public sealed override void Move()//我们可以把重写的方法声明为密封方法，表示该方法不能被重写
        {
            base.Move();
        }
    }
}
```
## 构造函数
* 通过子类构造对象时会调用子类的构造函数，也会调用父类的构造函数
* 在父类定义了一个无参的构造函数

```C#
class BaseClass
{
    public BaseClass()
    {
        Console.WriteLine("BaseClass无参构造函数");
    }
}
```
* 在子类中也定义一个无参的构造函数

```C#
class Asd:BaseClass
{
    public Asd()//当我们没有在子类的构造函数中显示声明父类的构造函数，会默认调用父类的无参函数
    {
        Console.WriteLine("子类中的无参构造函数");
    }
}
```
* 在主函数中通过子类和父类各声明一个对象

```C#
class Program
{
    static void Main(string[] args)
    {
        Asd asd = new Asd();//会先调用父类的构造函数，然后调用子类的构造函数
        BaseClass baseClass = new BaseClass();//会调用父类的构造函数
        //编译器会输出:
        //BaseClass无参构造函数
        //子类中的无参构造函数
        //BaseClass无参构造函数
        Console.ReadKey();
    }
}
```
* 在父类中定义一个有参的构造函数

```C#
class BaseClass
{
    public BaseClass(int x)
    {
        this.x = x;
        Console.WriteLine("x ok");
    }
}
```
* 在子类中定义一个有参的构造函数

```C#
class Asd:BaseClass
{
    public Asd(int x,int y) : base(x)//在子类的构造函数中显示声明父类有参的构造函数，在运行时会调用父类有参的构造函数，否则系统只会按照默认的调用父类的无参构造函数
    {
        this.y = y;
        Console.WriteLine("y ok");
    }
}
```
* 在主函数中通过子类声明一个对象

```C#
class Program
{
    static void Main(string[] args)
    {
        Asd asd = new Asd(1, 2);
        //编译器会输出:
        //x ok
        //y ok
        Console.ReadKey();
    }
}
```
## 关于访问修饰符 protected和static
* private int x;//只能在类内部访问
* protected int y;//protected声明保护字段，方法。可以在继承类中使用。如果没有继承类，和private一样
* public static int z;//static声明的字段和方法为静态字段和静态方法，只能通过类名访问

## 定义和实现接口
```C#
namespace _010_定义和实现接口
{
    interface Itank//interface定义接口
    //定义一个接口在语法上跟定义一个抽象类完全相同，但不允许提供接口中任何成员的实现方式，一般情况下，接口只能包含方法，属性，索引器和事件的声明。
    //接口不能有构造函数，也不能有字段，接口也不允许运算符重载。
    //接口定义中不允许声明成员的修饰符，接口成员都是公有的
    //接口可以彼此继承，继承方式与类的继承相同
    {
        void Shoot();//接口中的所有方法都没有实现方式
        void Move();
    }
}
```
```C#
namespace _010_定义和实现接口
{
    class Tiger:Itank//实现接口要实现接口中的所有方法
    {
        public void Shoot()
        {
            Console.WriteLine("这里是Shoot方法");
        }
        public void Move()
        {
            Console.WriteLine("这里是Move方法");
        }
    }
}
```
# 如果有什么问题，欢迎指教
