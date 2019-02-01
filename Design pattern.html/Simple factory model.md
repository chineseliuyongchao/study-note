## 原始加减乘除计算器
```C#
using System;

namespace 设计模式
{
    class Program//实现了加减乘除的运算
    {
        static void Main(string[] args)
        {
            double num1, num2;
            string operation;
            Console.WriteLine("请输入要进行运算的两个数字");
            num1 = Convert.ToDouble(Console.ReadLine());
            num2 = Convert.ToDouble(Console.ReadLine());
            Console.WriteLine("请输入要输入的运算符号");
            operation = Console.ReadLine();
            if(operation=="+")
            {
                Console.WriteLine("结果是：{0}", num1 + num2);
            }
            else if (operation == "-")
            {
                Console.WriteLine("结果是：{0}", num1 - num2);
            }
            else if (operation == "*")
            {
                Console.WriteLine("结果是：{0}", num1 * num2);
            }
            else if (operation == "/")
            {
                if(num2==0)
                {
                    Console.WriteLine("除数为零，不能运算");
                }
                Console.WriteLine("结果是：{0}", num1 / num2);
            }
            Console.ReadKey();
        }
    }
}
```

## 简单工厂模式计算器
* 实现运算的具体方法
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace 简单工厂模式02
{
    class Operation//运算基类
    {
        private double _numberA = 0;//参与运算的两个数字
        private double _numberB = 0;
        public double NumberA
        {
            get
            {
                return _numberA;
            }
            set
            {
                _numberA = value;
            }
        }
        public double NumberB
        {
            get
            {
                return _numberB;
            }
            set
            {
                _numberB = value;
            }
        }
        public virtual double GetRresult()//返回结果的方法
        {
            double result = 0;
            return result;
        }
    }
    class OperationAdd : Operation//继承自运算基类的加法运算类
    {
        public override double GetRresult()
        {
            double result = 0;
            result = NumberA + NumberB;
            return result;
        }
    }
    class OperationSub : Operation//继承自运算基类的减法运算类
    {
        public override double GetRresult()
        {
            double result = 0;
            result = NumberA - NumberB;
            return result;
        }
    }
    class OperationMul : Operation//继承自运算基类的乘法运算类
    {
        public override double GetRresult()
        {
            double result = 0;
            result = NumberA * NumberB;
            return result;
        }
    }
    class OperationDiv : Operation//继承自运算基类的除法运算类
    {
        public override double GetRresult()
        {
            double result = 0;
            result = NumberA / NumberB;
            return result;
        }
    }
}
```
* 运算工厂
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace 简单工厂模式02
{
    class OperationFactory//运算类工厂
    {
        public static Operation createOperate(string operate)
        {
            Operation oper = null;
            switch (operate)//判断要执行哪一个运算操作
            {
                case "+":
                    oper = new OperationAdd();
                    break;
                case "-":
                    oper = new OperationSub();
                    break;
                case "*":
                    oper = new OperationMul();
                    break;
                case "/":
                    oper = new OperationDiv();
                    break;
            }
            return oper;
        }
    }
}
```
* 客户端代码
```C#
 using System;

namespace 简单工厂模式02
{
    class Program
    {
        static void Main(string[] args)
        {
            Operation oper;//用运算基类声明一个对象
            string operation;
            Console.WriteLine("请输入要输入的运算符号");
            operation = Console.ReadLine();
            oper = OperationFactory.createOperate(operation);//通过输入的运算符号给对象实例化
            Console.WriteLine("请输入要输入的两个数字");
            oper.NumberA = Convert.ToDouble(Console.ReadLine());
            oper.NumberB = Convert.ToDouble(Console.ReadLine());
            double result = oper.GetRresult();
            Console.WriteLine("结果是{0}", result);
            Console.ReadKey();
        }
    }
}
```
