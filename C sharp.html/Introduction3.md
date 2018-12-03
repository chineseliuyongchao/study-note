# C#基础
## 函数的定义
```C#
class Program
{
    static int result(int num1,int num2)//声明一个返回值类型为int的函数
    {
        int res = num1 + num2;
        return res;
    }
    static void Main(string[] args)
    {
        int a = 30, b = 40;
        int c = result(a, b);//把a，b传递给函数并且用c接收返回值
        int d = result(12, 24);
        Console.WriteLine(d);//36
        Console.WriteLine(c);//70
        Console.ReadKey();
    }
}
```
## 函数的声明和使用
```C#
class Program
{
    static int max(int[] num)
    {
        int num1 = num[0];
        for(int i=0;i<num.Length;i++)
        {
            if(num1<num[i])
            {
                num1 = num[i];
            }
        }
        return num1;
    }
    static void Main(string[] args)
    {
        int[] a = { 123, 43, 23, 23455, 2, 1324, 23, 2367, 5667, 67 };
        int b = max(a);
        Console.WriteLine(b);//23455
        Console.ReadKey();
    }
}
```
```C#
class Program
{
    static int[] getdivisor(int num)
    {
        int num1=0, j=0;
        for(int i=1;i<=num;i++)
        {
            if(num%i==0)
            {
                num1++;
            }
        }
        int[] divisor = new int[num1];
        for (int i = 1; i <= num; i++)
        {
            if (num % i == 0)
            {
                divisor[j] = i;
                j++;
            }
        }
        return divisor;
    }
    static void Main(string[] args)
    {
        int a = Convert.ToInt32(Console.ReadLine());
        int[] b = getdivisor(a);
        for (int c = 0; c < b.Length; c++)
        {
            Console.Write(b[c] + " ");
        }
    }
}
```
## 参数数组_定义一个参数个数不确定的函数
```C#
class Program
{
    //定义一个函数，用来取得数字的和，但是数字的个数不确定
    //解决方案1：定义一个函数，参数传递过来一个数组
    static int and(int[] num)
    {
        int sum=0;
        for (int i = 0;i < num.Length; i++)
        {
            sum += num[i];
        }
        return sum;
    }
    static void Main(string[] args)
    {
        int[] a= {1,2,3};
        int b = and(a);
        Console.WriteLine(b);
        Console.ReadKey();
    }
}
```
```C#
class Program
{
    //定义一个函数，用来取得数字的和，但是数字的个数不确定
    //解决方案2：定义一个参数个数不确定的函数，这个时候使用参数数组
    static int puls(params int[] num)//params代表这是一个参数数组，在传递参数的时候可以直接传递多个变量，编译器会自动组成一个数组。如果是数组参数，那么这个数组需要自己去手动创建。
    {
        int sum = 0;
        for (int i = 0; i < num.Length; i++)
        {
            sum += num[i];
        }
        return sum;
    }
    static void Main(string[] args)
    {
        int c = puls(1, 2, 3, 4, 5);
        Console.WriteLine(c);
        Console.ReadKey();
    }
}
```
## 结构函数
```C#
namespace _039结构函数
{
    struct Vector3//可以在结构体中定义一个函数，有些时候可以使代码更加方便
    {
        public float x;
        public float y;
        public float z;
        public double Distance()
        {
            return Math.Sqrt(x * x + y * y + z * z);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Vector3 myVector3;
            myVector3.x = 3;
            myVector3.y = 4;
            myVector3.z = 5;
            Console.WriteLine(myVector3.Distance());//7.07106781186548
            Console.ReadKey();
        }
    }
}
```
## 函数的重载
* 当函数名相同，参数不同，这个叫作函数的重载(编译器会通过不同的参数去识别应该调用哪一个函数)

```C#
class Program
{
    static int MaxValue(params int[] intnum)
    {
        int a=intnum[0];
        for(int i=0;i<intnum.Length;i++)
        {
            if(a<intnum[i])
            {
                a = intnum[i];
            }
        }
        return a;
    }
    static double MaxValue(params double[] intnum)
    {
        double a = intnum[0];
        for (int i = 0; i < intnum.Length; i++)
        {
            if (a < intnum[i])
            {
                a = intnum[i];
            }
        }
        return a;
    }
    static void Main(string[] args)
    {
        int[] a = { 1, 2, 3, 4, 5, 6 };
        double[] b = { 1.3, 3.4, 5.7 };
        Console.WriteLine(MaxValue(a));//6
        Console.WriteLine(MaxValue(b));//5.7
        Console.ReadKey();
    }
}
```
## 委托的定义
* 委托(delegate)是一种存储函数引起的类型。委托的定义指了一个返回类型和一个参数列表
* 定义了委托之后，就可以声明该委托类型的变量，接着就可以把一个返回类型跟参数列表跟委托一样的函数赋值给这个变量

```C#
namespace _041委托的定义
{
    //定义一个委托跟函数差不多，区别在于
    //1：定义委托需要加上delegate关键字
    //2：委托的定义不需要函数体
    public delegate double mydelegate(double num1, double num2);//定义一个委托
    class Program
    {
        static double function1(double num1,double num2)//定义一个乘法函数
        {
            return num1 * num2;
        }
        static double function2(double num1,double num2)//定义一个加法函数
        {
            return num1 + num2;
        }
        static void Main(string[] args)
        {
            mydelegate de;//利用我们定义的委托类型声明了一个新的变量
            de = function1;//直接把一个函数名赋给委托，委托就相当于这个函数
            Console.WriteLine(de(1.1, 1.1));//1.21
            de = function2;//当我们给一个委托的变量赋值的时候，返回值跟参数列表必须一样，否则无法赋值
            Console.WriteLine(de(1.1, 1.1));//2.2
            Console.ReadKey();
        }
    }
}
```
## 异常处理
* 我们知道如何查找和修正错误，但是不能肯定错误不会发生，此时最好能预料错误的发生，编写足够健壮的代码以处理这些错误，而不必中断程序的执行。
* 错误处理就是用于这个目的。

```C#
//异常是指运行期间代码中产生的错误
int[] myArray={1,2,3,4};
int myEle=myArray[4];
//运行到这里的时候，会出现异常，这个异常的定义已经在CLR中定义好了。如果我们不去处理这个异常，那么当异常发生的时候，程序会终止掉，然后异常后面的代码都无法执行
```
* 我们处理异常的语法结构如下(包含了三个关键字try catch finally)

```C#
try{//包含了可能出现异常的代码(一条或者多条语句)
    
}
catch(<exceptionType> e){//用来捕捉异常，当代码发生异常，那么异常的类型和catch块中的类型一样的时候，就会执行该catch，如果catch块的参数不写，表示发生任何异常都执行这个catch块
    
}
finally{//包含了始终会执行的代码，不管有没有异常参数都会执行
    
}
```
* 其中catch块可以有0或者多个，finally块可以有0或者1个
* 但是如果没有catch块，必须有finally块，没有finally块，必须有catch块，catch块和finally块可以同时存在

```C#
static void Main(string[] args)
{
    try//try，catch，finall是标准的异常捕捉语句
    {
        int[] asdf = { 1, 2, 3, 4 };//可能发生异常的代码
        int a = asdf[4];
    }
    catch (IndexOutOfRangeException)//异常类型：数组下标越界
    {
        Console.WriteLine("你访问的数组下标越界了");
    }
    catch//没有标明类型就会默认执行
    {
        Console.WriteLine("你访问的数组下标越界了");
    }
    finally//一定会执行的部分
    {
        Console.WriteLine("这里是finally部分");
    }
    Console.ReadKey();
}
```
```C#
static void Main(string[] args)
{
    //一个对用户输入的两个数就行加法运算的有异常捕捉操作的程序
    int num1 = 0;
    int num2 = 0;
    Console.WriteLine("请输入第一个数字");
    while (true)
    {
        try
        {
            num1 = Convert.ToInt32(Console.ReadLine());//如果发生异常，将不会执行try中后面的代码
            break;
        }
        catch
        {
            Console.WriteLine("输入的不是数字，请重新输入");
        }
    }
    Console.WriteLine("请输入第二个数字");
    while (true)
    {
        try
        {
            num2 = Convert.ToInt32(Console.ReadLine());
            break;
        }
        catch
        {
            Console.WriteLine("输入的不是数字，请重新输入");
        }
    }
    int sum = num1 + num2;
    Console.WriteLine(sum);
    Console.ReadKey();
}
```
# 如果有什么问题，欢迎指教
