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
# 如果有什么问题，欢迎指教
