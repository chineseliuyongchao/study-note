# C#入门
## switch语句
```C#
static void Main(string[] args)
{
    int state = 3;
    switch (state)//对state的值就行判断
    {
        case 0://如果state的值为0，执行下一行代码，然后break。如果不是0，执行下一个case。
            Console.WriteLine("开始界面");
            break;
        case 1:
            Console.WriteLine("战斗中");
            break;
        case 2:
            Console.WriteLine("暂停");
            break;
        case 3:
            Console.WriteLine("游戏胜利");
            break;
        case 4:
            Console.WriteLine("游戏失败");
            break;
        default://如果state的值不满足前面的所有条件，就执行default下面的代码
            Console.WriteLine("tan90");
            break;
    }
    Console.ReadKey();
}
```
## while循环
```C#
static void Main(string[] args)
{
    int num1 = 10;
    while (num1 >= 0)//如果满足while后面的条件，就执行循环，否则退出循环。并且在每次循环之前判断一次。
    {
        Console.WriteLine(num1);
        num1--;
    }
    Console.ReadKey();
}
```
## do_while循环
```C#
static void Main(string[] args)
{
    int num1 = 1;
    do
    {
        num1++;
        Console.WriteLine(num1);
    } while (num1 <= 9);//在每次循环执行完以后判断是否满足条件，如果满足就继续，不满足就退出循环。
    Console.ReadKey();
}
```
## for循环
```C#
static void Main(string[] args)
{
    for (int num = 1; num <= 9; num++)//(用来控制循环的参数；判断循环是否能够继续；参数进行变化)
    {
        Console.WriteLine(num);
    }
    Console.ReadKey();
}
```
## 循环的终止break
```C#
static void Main(string[] args)
{
    while (true)
    {
        string str1 = Console.ReadLine();
        if (str1 == "0")
        {
            break;//break可以终止循环，如果是循环套循环的话只能终止内循环
        }
        else
        {
            Console.WriteLine(str1);
        }
    }
}
```
## 循环的中断
```C#
static void Main(string[] args)
{
    int num = 0;
    while (true)
    {
        num++;
        if (num == 5)
        {
            continue;//结束本次循环，如果是循环套循环的话只能结束内循环
        }
        else if (num == 10)
        {
            break;
        }
        Console.WriteLine(num);
    }
}
```
## goto和return跳出循环
```C#
static void Main(string[] args)
{
    while (true)
    {
        string str = Console.ReadLine();
        if (str == "0")
        {
            goto back;//如果str=="0"，执行goto语句，就会直接跳到back;语句
        }
    }
    back:
    Console.WriteLine("跳出循环");

    while (true)
    {
        string str = Console.ReadLine();
        if (str == "0")
        {
            return;////如果str=="0"，执行return语句，就会直接结束程序的运行
        }
    }
    Console.WriteLine("跳出循环");
    Console.ReadKey();
}
```
## 显式转换和隐式转换
```C#
static void Main(string[] args)
{
    byte mybyte = 211;
    int num = mybyte;//把一个小类型的数据转换成大类型的时候，会自动完成隐式转换
    mybyte = (byte)num;//把一个大类型的数据转换成小类型的时候，需要手动完成显式转换
}
```
## 枚举类型
```C#
enum gamestate//定义一个枚举类型
{
    win,
    over,
    pause,
    start
}
class Program
{
    static void Main(string[] args)
    {
        gamestate state=gamestate.win;//声明一个枚举变量
        if (state == gamestate.win)//进行判断操作
        {
            Console.WriteLine("win");
        }
        Console.ReadKey();
    }
}
```

## 结构体
```C#
struct npc//定义一个结构体
{
    public int level;
    public int hp;
    public int soidiers;
    public int money;
    public countries country;
}
enum countries
{
    han,
    xiongnu,
    nanyue,
    donghu
}
class Program
{
    static void Main(string[] args)
    {
        npc general1;
        general1.level = 56;
        general1.hp = 134;
        general1.soidiers = 279;
        general1.money = 138000;
        general1.country = countries.han;
        npc general2;
        general2.level = 34;
        general2.hp = 95;
        general2.soidiers = 145;
        general2.money = 73000;
        general2.country = countries.nanyue;
        Console.WriteLine("level:{0}\thp:{1}\tsoldiers:{2}\tmoney:{3}\tcountry:{4}",general1.level,general1.hp,general1.soidiers,general1.money,general1.country);//level:56        hp:134  soldiers:279    money:138000    country:han
        Console.WriteLine("level:{0}\thp:{1}\tsoldiers:{2}\tmoney:{3}\tcountry:{4}", general2.level, general2.hp, general2.soidiers, general2.money, general2.country);//level:34        hp:95   soldiers:145    money:73000     country:nanyue
        Console.ReadKey();
    }
}
```
## 数组
```C#
static void Main(string[] args)
{
    int[] number = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };//定义一个数字数组
    Console.WriteLine(number[3]);//输出数组的第四位     4
    char[] a = new char[]{'z','x','c','v','b','n','m'};//定义一个字符类型的数组
    Console.WriteLine(a[4]);//输出数组的第五位     b
    string[] str = { "han", "xiongnu", "baiyue", "donghu" };//定义一个字符串类型的数组
    Console.WriteLine(str[2]);//输出数组的第三位     baiyue
    Console.ReadKey();
}
```
## 使用for_whle_foreach遍历数组
```C#
static void Main(string[] args)
{
    int[] num = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    for (int a = 0; a < num.Length; a++)
    {
        Console.WriteLine(num[a]);
    }
    int a = 0;
    while (a < num.Length)
    {
        Console.WriteLine(num[a]);
        a++;
    }
    foreach (int temp in num)//foreach会依次取到数组num中的值，然后赋值给temp，然后执行循环
    {
        Console.WriteLine(temp);
    }
    Console.ReadKey();
}
```
## 字符串的处理
```C#
static void Main(string[] args)
{
    string str = "    www.  taiker.COM   ";
    for (int i = 0; i < str.Length; i++)//输出字符串中的每一个字符，包括空格
    {
        Console.WriteLine(str[i]);
    }
    string res1 = str.ToLower();//把字符串转换成小写并返回
    string res2 = str.ToUpper();//把字符串转换成大写并返回
    string res3 = str.Trim();//删除字符串的前导空白字符和尾部空白字符
    string res4 = str.TrimStart();//删除字符串的前导空白字符
    string res5 = str.TrimEnd();//删除字符串的尾部空白字符
    string[] res6 = str.Split('.');//按照给定的字符串'.'将字符串分割并且生成一个新的数组
    Console.WriteLine(str + '|');//    www.  taiker.COM   |
    Console.WriteLine(res1 + '|');//    www.  taiker.com   |
    Console.WriteLine(res2 + '|');//    WWW.  TAIKER.COM   |
    Console.WriteLine(res3 + '|');//www.  taiker.COM|
    Console.WriteLine(res4 + '|');//www.  taiker.COM   |
    Console.WriteLine(res5 + '|');//    www.  taiker.COM|
    foreach (string temp in res6)
    {
        Console.WriteLine(temp);
    }
    Console.ReadKey();
}
```
# 如果有什么问题，欢迎指教
