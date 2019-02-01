## 简单工厂模式实现商场打折系统
* 具体方法
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace _02_策略模式01
{
    abstract class CashSuper//商场收费模式基类
    {
        public abstract double acceptCash(double money);
    }
    class CashNormal : CashSuper//继承自基类的原价收费类
    {
        public override double acceptCash(double money)
        {
            return money;
        }
    }
    class CashRebate : CashSuper//继承自基类的打折收费类
    {
        private double moneyRebate = 1d;
        public CashRebate(string moneyRebate)
        {
            this.moneyRebate = double.Parse(moneyRebate);
        }
        public override double acceptCash(double money)
        {
            return money * moneyRebate;
        }
    }
    class CashReturn : CashSuper//继承自基类的满减收费类
    {
        private double moneyCondition = 0.0d;
        private double moneyReturn = 0.0d;
        public CashReturn(string moneyCondition, string moneyReturn)
        {
            this.moneyCondition = double.Parse(moneyCondition);
            this.moneyReturn = double.Parse(moneyReturn);
        }
        public override double acceptCash(double money)
        {
            double result = money;
            if (money >= moneyCondition)
            {
                result = money - Math.Floor(money / moneyCondition) * moneyReturn;
            }
            return result;
        }
    }
}
```
* 工厂类
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace _02_策略模式01
{
    class CashFactory//收费工厂，负责向客户端返回优惠方法
    {
        public static CashSuper createCashAccept(string type)//接受客户端输入的方法字符串
        {
            CashSuper cs = null;
            switch (type)//判断
            {
                case "正常收费":
                    cs = new CashNormal();
                    break;
                case "满减":
                    cs = new CashReturn("300", "100");
                    break;
                case "打折":
                    cs = new CashRebate("0.8");
                    break;
            }
            return cs;//返回优惠方法
        }
    }
}
```
* 客户端
```C#
using System;

namespace _02_策略模式01//收费活动简单工厂模式
{
    class Program//收费客户端
    {
        static void Main(string[] args)
        {
            CashSuper cash;
            Console.WriteLine("请输入要进行的价格计算类型（“正常收费”，“满减”或“打折”）");
            cash = CashFactory.createCashAccept(Console.ReadLine());
            Console.WriteLine("请输入原价");
            double result = cash.acceptCash(Convert.ToDouble(Console.ReadLine()));
            Console.WriteLine("实付价格为{0}", result);
            Console.ReadKey();
        }
    }
}
```
## 简单工厂模式结合策略模式实现商场打折系统
* 具体方法
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace _02_策略模式_02
{
    abstract class CashSuper//商场收费模式基类
    {
        public abstract double acceptCash(double money);
    }
    class CashNormal : CashSuper//继承自基类的原价收费类
    {
        public override double acceptCash(double money)
        {
            return money;
        }
    }
    class CashRebate : CashSuper//继承自基类的打折收费类
    {
        private double moneyRebate = 1d;
        public CashRebate(string moneyRebate)
        {
            this.moneyRebate = double.Parse(moneyRebate);
        }
        public override double acceptCash(double money)
        {
            return money * moneyRebate;
        }
    }
    class CashReturn : CashSuper//继承自基类的满减收费类
    {
        private double moneyCondition = 0.0d;
        private double moneyReturn = 0.0d;
        public CashReturn(string moneyCondition, string moneyReturn)
        {
            this.moneyCondition = double.Parse(moneyCondition);
            this.moneyReturn = double.Parse(moneyReturn);
        }
        public override double acceptCash(double money)
        {
            double result = money;
            if (money >= moneyCondition)
            {
                result = money - Math.Floor(money / moneyCondition) * moneyReturn;
            }
            return result;
        }
    }
}
```
* 结合策略模式的工厂类
```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace _02_策略模式_02
{
    class CashContext//结合策略模式后的工厂类
    {
        CashSuper cs = null;
        public CashContext(string type)//判断使用哪一个优惠方法
        {
            switch(type)
            {
                case "正常收费":
                    CashNormal cs0 = new CashNormal();
                    cs = cs0;
                    break;
                case "满减":
                    CashReturn cr1 = new CashReturn("300","100");
                    cs = cr1;
                    break;
                case "打折":
                    CashRebate cr2 = new CashRebate("0.8");
                    cs = cr2;
                    break;
            }
        }
        public double GetResult(double money)//直接向客户端返回需要的钱
        {
            return cs.acceptCash(money);
        }
    }
}
```
* 客户端
```C#
using System;

namespace _02_策略模式_02//收费模式策略模式+简单工厂模式
{
    class Program//客户端代码
    {
        static void Main(string[] args)
        {
            double result = 0.0;
            Console.WriteLine("请输入要进行的价格计算类型（“正常收费”，“满减”或“打折”）");
            CashContext cash = new CashContext(Console.ReadLine());
            Console.WriteLine("请输入原价");
            result = cash.GetResult(Convert.ToDouble(Console.ReadLine()));
            Console.WriteLine("实付价格为{0}", result);
            Console.ReadKey();
        }
    }
}
```
