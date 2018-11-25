# 协程+鼠标相关函数+Mathf常用方法
## 协程
### 什么是协程、它是如何执行的
* 方法运行时，如果调用到一个普通方法，会等待普通方法执行完在继续运行。如果是协程方法，不会等待协程方法执行，而是直接继续运行。
```C#
public class API06 : MonoBehaviour {
	void Start () {
        StartCoroutine(Fire());//协程方法的调用StartCoroutine(Fire());
        //协程方法开启后，会继续运行下面的代码，不会等协程方法运行结束才继续执行
        print(4399);
	}
    IEnumerator Fire()//返回值是IEnumerator
    {
        print(123);
        yield return null;//返回参数的时候使用yield return null
    }
}
```
### 使用Coroutine实现颜色动画渐变
* yield return new WaitForSeconds(s); 放入协程函数中可以让程序运行到这里暂停s秒
```C#
//使用协程制作颜色渐变的效果（方法1）
public class API06 : MonoBehaviour {
    public GameObject Cube;
	void Start () {
        StartCoroutine(Color());//协程方法的调用StartCoroutine(Color());
    }
    IEnumerator Color()//返回值是IEnumerator
    {
        for(float i = 0; i< 1; i += 0.01f)
        {
            Cube.GetComponent<MeshRenderer>().material.color = new Color(i, i, i, i);//调用Cube的颜色并且让其发生变化
            yield return new WaitForSeconds(0.02f);//暂停0.02秒
        }
    }
}
```
```C#
//使用协程制作颜色渐变的效果（方法2）
public class API06 : MonoBehaviour {
    public GameObject Cube;
    void Start()
    {
        StartCoroutine(Colorr());//协程方法的调用StartCoroutine(Colorr());
    }
    IEnumerator Colorr()
    {
        for (; ; )//默认死循环
        {
            Color color = Cube.GetComponent<MeshRenderer>().material.color;//获得cube的颜色，并且赋给color
            Color newcolor = Color.Lerp(color, Color.red, 0.02f);//进行差值运算，并且将预算结果赋给newcolor
            Cube.GetComponent<MeshRenderer>().material.color = newcolor;//让cube的颜色等于newcolor的颜色
            yield return new WaitForSeconds(0.02f);//让协程暂停0.02秒
            if (Mathf.Abs(Color.red.g - newcolor.g) <= 0.01f)//如果颜色特别接近就结束循环
            {
                break;
            }
        }
    }
}
```
### Coroutine协程的开启和关闭
* StopCoroutine(); 关闭协程
```C#
private IEnumerator ie;
void Start()
{
    ie = Colorr();
    StartCoroutine(ie);//协程方法的调用StartCoroutine(Colorr());
    StopCoroutine(ie);//关闭协程
}
```
## 鼠标相关函数
### 跟鼠标相关事件函数OnMouseXXX讲解
* OnMouseDown 鼠标按下
* OnMouseDrag 鼠标按下并且拖拽的时候
* OnMouseEnter 鼠标移动到上面时
* OnMouseOver 鼠标停留在上面时
* OnMouseExit 鼠标离开的时候
* OnMouseUp 鼠标抬起的时候
* OnMouseUpAsButton 当鼠标在按下鼠标的那个游戏物体上面抬起的时候
* 检测鼠标事件函数有两个条件：1，打开检测物体碰撞体的触发器。2，Edit→Project Setting→Physics→Queries Hit Triggers勾选
## Mathf常用方法
### Mathf里面的静态常量
* PI 圆周率
* Reg2Rad 角度变弧度的参数
* Rad2Reg 弧度变角度的参数
* Epsilon 无限接近于零的正小数
* Infinity 无限大的整数
* NegativeInfinity 无限小的整数
### Mathf中的Clamp限定方法
* Abs 取绝对值
```C#
int num = Mathf.Abs(-5);//num=5
```
* Ceil 向上取整（会返回float类型数值）
```C#
float num1 = Mathf.Ceil(10.7f);//num1=11
float num2 = Mathf.Ceil(-10.7f);//num2=-10
```
* CeilToInt 向上取整并且返回int类型的数值
* Floor 向下取整
* Clamp 夹紧一个变量，必须使用float类型的变量进行操作
```C#
float num1 = 3;
float num2 = 5;
float num3 = 8;
num1 = Mathf.Clamp(num1, 4.1f, 7.4f);//num1=4.1
num2 = Mathf.Clamp(num2, 4.1f, 7.4f);//num2=5
num3 = Mathf.Clamp(num3, 4.1f, 7.4f);//num3=7.4
```
* Clamp01 用0和1夹紧一个变量
### Mathf中的常用方法
* ClosestPowerOfTwo(int value) 取得2的整数次方中离value最近的数字
* DeltaAngle 计算两个角度的最小距离
```C#
float num1 = 2300;
float num2 = 234;
float num3 = Mathf.DeltaAngle(num1, num2);//num3=94
```
* Exp(float power) 取得e的power次方
* Max(float a,float b) 返回较大值
* Max(parems float[]values) 返回最大值
* Min(float a,float b) 返回较大值
* Min(parems float[]values) 返回最大值
* Pow(float f,float p) 取得f的p次方
* Sqrt(Sqrt t) 取得t的平方根
### 关于游戏开发中的插值运算
* Lerp(float a,float b,float t) 差值运算。a:起始值。b:目标值。 c:每一帧的变化比例。
```C#
public float a = 4;
public float b = 6;
void Start()
{
    float num0 = Mathf.Lerp(a, b, -0.5f);//num0=4
    float num1 = Mathf.Lerp(a, b, 0.1f);//num1=4.2
    float num2 = Mathf.Lerp(a, b, 0.7f);//num2=5.4
    float num3 = Mathf.Lerp(a, b, 2f);//num3=6
    print(num0);
    print(num1);
    print(num2);
    print(num3);
}
```
```C#
public GameObject Cube;
void Start()
{
    Cube.transform.position = new Vector3(0, 0, 0);
}
void Update()//通过差值运算让游戏物体的x轴从0到10
{
    float x = Cube.transform.position.x;
    float newx = Mathf.Lerp(x, 10, 0.1f);
    Cube.transform.position = new Vector3(newx,0,0);
}
```
### 使用MoveTowards做匀速运动
* MoveTowards(float current,float target,float maxDelta)current:当前值。target：目标值。maxDelta：每一帧的变化量。
### 使用PingPong方法实现乒乓的来回运动效果
* PingPong(float t，float length);         在0到length之间来回移动
```C#
float num0 = Mathf.PingPong(5, 20);//num0=5
float num1 = Mathf.PingPong(18, 20);//num1=18
float num2 = Mathf.PingPong(29, 20);//num2=11
float num3 = Mathf.PingPong(55, 20);//num3=15
```
```C#
public GameObject Cube;
public int speed = 1;
void Update()
{
    Cube.transform.position = new Vector3(Mathf.PingPong(Time.time*speed, 5), 0, 0);//让游戏物体沿着x轴在0到5之间以1的速度来回移动
}
```
# 如果哪里有问题，欢迎指教
