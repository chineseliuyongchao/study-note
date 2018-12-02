# C#入门
## C#第一个程序
```C#
Console.WriteLine("hello word");
```
## 变量
```C#
static void Main(string[] args)
{
    int hp = 67;//int类型变量
    int xp = 3456;
    string name = "lyc";//字符串类型变量
    Console.WriteLine(hp);//输出hp的值，即67
    Console.ReadKey();等待键盘输入，退出程序。使调试时能看到输出结果。如果没有此句，命令窗口会一闪而过。
}
```
## 类型
```C#
static void Main(string[] args)
{
    byte hp = 34;//byte表示在0~255之间的整数
    int xp = 45378;//int表示在-2147483648~2147483647之间的整数
    long mony = 123456789;//long表示在-9223372036854775808~9223372036854775807之间的整数
    Console.WriteLine("hp:{0},xp:{1},mony:{2}", hp, xp, mony); //hp:34,xp:45378,mony:123456789
    float high = 1.85f;//单精度浮点型小数
    double tall = 1.834;//双精度浮点型小数
    Console.WriteLine("high:{0},tall:{1}", high, tall); //high:1.85,tall:1.834
    char MyChar = 'a';//一个字符
    string MyString = " ";
    string MyString2 = "afhsjkzhvkb";
    bool MyBool = false;//希尔值，true或false
    Console.WriteLine("MyChar:{0},MyString:{1},MyString2:{2},MyBool:{3}", MyChar, MyString, MyString2, MyBool); //MyChar:a,MyString: ,MyString2:afhsjkzhvkb,MyBool:False
    Console.ReadKey();
}
```
## 主角的信息
```C#
static void Main(string[] args)
{
    string name = "siki";//练习定义一个主角的信息，并且把它输出
    byte hp = 67;
    byte level = 26;
    int mony = 1234567890;
    Console.WriteLine("name:{0},hp:{1},level:{2},money:{3}", name, hp, level, mony);
    Console.ReadKey();
}
```
## @的使用
```C#
static void Main(string[] args)
{
    //如果我们不想去识别字符串中的转义字符，可以在字符串前面加一个@符号（除了\"其他转义字符都不再识别）
    string MyString = @"I am a good man,
        \\you are a bad gril.";
    //I am a good man,
    //    \\you are a bad gril.
    Console.WriteLine(MyString);
    string MyString2 = @"I am a good man,\\you are a bad gril";//I am a good man,\\you are a bad gril
    Console.WriteLine(MyString2);
    string path = "C\\xxxx\\xxx\\xxxxxxxxxx";//C\xxxx\xxx\xxxxxxxxxx
    Console.WriteLine(path);
    string path2 = @"C\xxxx\xxx\xxxxxxxxxx";//C\xxxx\xxx\xxxxxxxxxx
    Console.WriteLine(path2);
    Console.ReadKey();
}
```
## 多变量的声明与使用
```C#
static void Main(string[] args)
{
    //我们可以用一条语句声明多个类型一样的变量
    byte hp = 89, level = 35, money = 230;
    Console.WriteLine(hp);//89
    Console.ReadKey();
}
```
## 数字运算符
```C#
static void Main(string[] args)
{
    int num1 = 12;
    int num2 = 4;
    int res1 = num1 + num2;//数字相加
    int res2 = num1 - num2;//数字相减
    int res3 = num1 * num2;//数字相乘
    int res4 = num1 / num2;//数字相除
    int res5 = num1 % num2;//数字取余
    Console.WriteLine("{0},{1},{2},{3},{4}", res1, res2, res3, res4, res5);//16,8,48,3,0
    string str="asdf";
    int num3=123;
    string str1 = str + num3;//当一个字符串跟一个数字相加的话，首先把数字转变成字符串，然后连接起来，结果是字符串
    Console.WriteLine(str1);//asdf123
    Console.ReadKey();
}
```
## 数字运算符的自加和自减
```C#
static void Main(string[] args)
{
    byte num1 = 34;
    byte num2 = num1;
    byte res1 = num1++;
    byte res2 = ++num1;
    byte res3 = num2--;
    byte res4 = --num2;
    Console.WriteLine("{0},{1},{2},{3}", res1, res2, res3, res4);//34,36,34,32
    Console.ReadKey();
}
```
## 接受用户输入的字符串_整数和小数
```C#
static void Main(string[] args)
{
    string str1 = Console.ReadLine();//输入一个字符串
    int num1 = Convert.ToInt32(str1);//输入一个数字，C#只能接受字符串，所以需要用Convert.ToInt32()方法将字符串转换为数字
    Console.WriteLine(num1);//输出刚刚输入的东西
    string str2 = Console.ReadLine();
    double num2 = Convert.ToDouble(str2);
    Console.WriteLine(num2);
    Console.ReadKey();
}
```
## 案例练习_接受用户从控制台输入的两个数字_并计算和_输出到控制台
```C#
static void Main(string[] args)
{
    string str1 = Console.ReadLine();
    string str2 = Console.ReadLine();
    int num1 = Convert.ToInt32(str1);
    int num2 = Convert.ToInt32(str2);
    int num3 = num1 + num2;
    Console.WriteLine(num3);
    Console.ReadKey();
}
```
## 赋值运算符
```C#
static void Main(string[] args)
{
    int num1 = 34;
    num1 += 23;//num1=num1+23=57
    num1 -= 23;//num1=num1-32=34
    num1 *= 2;//num1=num*2=68
    num1 /= 2;//num1=num1/2=34
    num1 %= 4;//num1=num1%4=2
    Console.WriteLine(num1);//2
    Console.ReadKey();
}
```
## 运算符的优先级
```C#
static void Main(string[] args)
{
    int num1 = 2 + 3 * 4;//C#中会先运算优先级高的，再运算优先级低的
    int num2 = 3 * 5 / 2;//括号会重写优先级，括号内的优先级最高
    int num3 = (5 + 7) * 2;
    Console.WriteLine(num1);
    Console.WriteLine(num2);
    Console.WriteLine(num3);
    Console.ReadKey();
    //优先级由高到低(按行降低，同一行优先级相同)
    //++、--(用作前缀)、+、-(一元)
    //*、/、%
    //+、-
    //=、*=、/=、%=、+=、-=
    //++、--(用作后缀)
}
```
## 布尔运算
```C#
static void Main(string[] args)
{
    int num1 = 99;
    bool res = num1 >= 50;//因为num1大于50，所以res返回的是true
    Console.WriteLine(res);//tue
    Console.ReadKey();
}
```
## 布尔运算符
```C#
static void Main(string[] args)
{
    int num1 = 23;
    int num2 = 45;
    bool res1 = num1 == num2;
    bool res2 = num1 != num2;
    bool res3 = num1 > num2;
    bool res4 = num1 < num2;
    bool res5 = num1 >= num2;
    bool res6 = num1 <= num2;
    Console.WriteLine(res1);//false
    Console.WriteLine(res2);//true
    Console.WriteLine(res3);//false
    Console.WriteLine(res4);//true
    Console.WriteLine(res5);//false
    Console.WriteLine(res6);//true
    Console.ReadKey();
}
```
## 条件布尔运算符
```C#
static void Main(string[] args)
{
    bool var1 = true;
    bool var2 = false;
    bool res1 = var1 & var2;
    bool res2 = var1 | var2;
    bool res3 =!var1;
    bool res4 = var1 ^ var2;//如果两个一样，就返回false，如果不一样，就返回true
    Console.WriteLine(res1);//false
    Console.WriteLine(res2);//true
    Console.WriteLine(res3);//false
    Console.WriteLine(res4);//true
    Console.ReadKey();
}
```
## goto语句
```C#
static void Main(string[] args)
{
    int num1 = 34;
    goto my;//会直接跳转到"my:Console.WriteLine(num1);",并且运行
    num1++;//这一行不会运行
    my:Console.WriteLine(num1);
    Console.ReadKey();
}
```
## if语句
```C#
static void Main(string[] args)
{
    bool var1 = true;
    if (var1)//如果var1为true，就执行括号内的语句，如果不是，就不执行
    {
        Console.WriteLine("---------");//会执行
    }
    Console.WriteLine("+++++++++++");//不会执行
    if (49 >= 90)//如果49>90成立，就执行括号内的语句，如果不成立，就不执行
    {
        Console.WriteLine("\\\\\\\\\\\\\\\\");//不会执行
    }
        Console.WriteLine("------------");
        Console.ReadKey();
    }
```
## 三元运算符
```C#
static void Main(string[] args)
{
    string str1 = Console.ReadLine();
    int num1 = Convert.ToInt32(str1);
    //如果满足？前面的条件就返回：前面的，如果不满足就返回：后面的
    string resstr = num1 > 50 ? "输入的数字大于50" : "输入的数字小于50";
    Console.WriteLine(resstr);//如果输入的数字大于50，就会输出"输入的数字大于50":如果输入的数字小于50，就会输出"输入的数字小于50"
    Console.ReadKey();
}
```
## if_else语句
```C#
static void Main(string[] args)
{
    Console.WriteLine("请输入分数");
    string str = Console.ReadLine();
    int num1 = Convert.ToInt32(str);
    if (num1 >= 90)
    {
        Console.WriteLine("优秀");
    }
    else if (num1 >= 80)
    {
        Console.WriteLine("良好");
    }
    else if (num1 >= 60)
    {
        Console.WriteLine("及格");
    }
    else
    {
        Console.WriteLine("不及格");
    }
        Console.ReadKey();
    }
```
# 如果有什么问题，欢迎指教
