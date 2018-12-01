# 按键操作+向量+随机数
## 按键操作
### Input类输入类（按键、按键、触摸相关检测）
* Edit→ProjectSetting→Input 设置相关的轴
### Input里面的GetKeyXXX的使用
* GetKey 键盘按键处于被按下状态时调用
* GetKeyDown 键盘按键被按下
* GetKeyUp 键盘按键被抬起 

```C#
if (Input.GetKey(KeyCode.Space))//检测空格键是否处于被按下状态
{
    print("GetKey");
}
if (Input.GetKeyDown(KeyCode.Space))//检测空格键是否被按下
{
    print("GetKeyDown");
}
if (Input.GetKeyUp(KeyCode.Space))//检测空格键是否被抬起
{
    print("GetKeyUp");
}
```
* 正常键: “a”, “b”, “c” …
* 数字键: “1”, “2”, “3”, …
* 方向键: “up”, “down”, “left”, “right”
* 小键盘键: “[1]”, “[2]”, “[3]”, “[+]”, “[equals]”
* 修改键: “right shift”, “left shift”, “right ctrl”, “left ctrl”, “right alt”, “left alt”, “right cmd”, “left cmd”
* 鼠标按钮: “mouse 0”, “mouse 1”, “mouse 2”, …
* 特殊键: “backspace”, “tab”, “return”, “escape”, “space”, “delete”, “enter”, “insert”, “home”, “end”, “page up”, “page down”
* 功能键: “f1”, “f2”, “f3”, …
### 鼠标按键事件的监测
* Input.GetMouseButtonDown(int button); 按下左键时，button=0。按下右键时，button=1。按下中键时，button=2。
* Input.GetMouseButtonUp(int button); 抬起左键时，button=0。抬起右键时，button=1。抬起中键时，button=2。
* Input.GetMouseButton(int button); 左键处于被按下状态时，button=0。右键处于被按下状态时，button=1。中键处于被按下状态时，button=2。

```C#
if (Input.GetMouseButton(0))
{
    Debug.Log("Pressed left click.");
}

if (Input.GetMouseButton(1))
{
    Debug.Log("Pressed right click.");
}

if (Input.GetMouseButton(2))
{
    Debug.Log("Pressed middle click.");
}
```
### GetButtonXXX相关事件监测
* Edit→ProjectSetting→Input 所有的虚拟按键
* 在InputManager中，Name表示虚拟按键的名字。如果使用GetButtonXXX调用虚拟按键。在按下NegativeButton/AltNegativeButton或者PositiveButton/AltPositiveButton对应的键之前返回一个值为false的布尔变量，按下NegativeButton/AltNegativeButton或者PositiveButton/AltPositiveButton对应的键之后返回一个值为true的布尔变量。

```C#
void Update () {
    //程序开始运行后按下AD键或者左右键
    bool a = false;
    bool b = true;
    print(a);//a=false
    print(b);//b=true
    a = Input.GetButtonDown("Horizontal");
    b = Input.GetButtonDown("Horizontal");
    print(a);//按下对应按键之前a=false，按下对应按键之后a=true
    print(b);//按下对应按键之前b=false，按下对应按键之后b=true
}
```
### 使用GetAxis得到轴的值的变化来控制移动
* 如果使用GetAxis调用虚拟按键。在按下NegativeButton/AltNegativeButton或者PositiveButton/AltPositiveButton对应的键之前返回一个值为0的float变量。按下NegativeButton/AltNegativeButton对应的键之后返回一个从零渐变到-1的float变量，按下PositiveButton/AltPositiveButton对应的键之后返回一个从零渐变到1的float变量，松开后会返回一个渐变到0的float变量。
* 如果使用GetAxisRaw调用虚拟按键。在按下NegativeButton/AltNegativeButton或者PositiveButton/AltPositiveButton对应的键之前返回一个值为0的float变量。按下NegativeButton/AltNegativeButton对应的键之后返回一个值为-1的float变量，按下PositiveButton/AltPositiveButton对应的键之后返回一个值为1的float变量，松开后会返回一个值为0的float变量。

```C#
void Update () {
    float a = Input.GetAxis("Horizontal");
    float b = Input.GetAxisRaw("Horizontal");
    print(a);//按下A键或者左键后a的值由0逐渐变到-1，按下D键或者右键后a的值由0逐渐变到-1，松开后渐变回0
    print(b);//按下A键或者左键后b直接变到-1，按下D键或者右键后b直接变到-1，松开后直接变回0
}
```
### 屏幕坐标系和鼠标的坐标
* anyKeyDown 检测是否有任何键按下，如果有。返回一个值为true的布尔变量
* mousePosition 获得鼠标在屏幕上面的位置（像素单位）
## 向量
### Vector2中的变量有哪些
* down vector2(0,-1)
* left vector2(-1,0)
* one vector2(1,1)
* right vector2(1,0)
* up vector2(0,1)
* zero vector2(0,0)
* magnitude 取得向量的长度
* normalized 将向量单位化
* sqrMagnitude 取得向量的长度的平方（比较向量长度不进行开根号就可以进行比较，节省性能）
* x 取得向量的x轴
* y 取得向量的y轴

```C#
void Update () {
    Vector2 vector2 = new Vector2(3, 4);
    print(vector2.magnitude);//5
    print(vector2.normalized);//(0.6,0.8)
    print(vector2.sqrMagnitude);//25
}
```
### 向量是结构体
* transform.position不能单独修改其中的某个变量，但是可以单独访问，也可以集体赋值。使用Vector3自己定义的三维向量是可以单独修改的。因为position不是一个结构体，它是transform类里面的一个成员，它的类型是Vector3，而在transform这个类中，position只提供了get和set这两个方法来访问，set规定修改就必须提供全部的变量。

```C#
void Update () {
    this.transform.position.x = 5;//这行会报错，因为无法单独修改position的返回值
    float a = this.transform.position.x;//下面的都可以正常运行
    Vector3 vector3=new Vector3(5,5,5);
    vector3.x = 5;
    this.transform.position = vector3;
}
```
### 二维向量Vector2中的静态方法
* Normalize 将自身单位化

```C#
void Update () {
    Vector2 vector2 = new Vector2(3, 4);
    vector2.Normalize();//将自身单位化
    print(vector2);//(0.6,0.8)
}
```
* Angle 取得两个向量的夹角

```C#
void Update () {
    Vector2 vector1 = new Vector2(3, 4);
    Vector2 vector2 = new Vector2(2, 5);
    print(Vector2.Angle(vector1, vector2));//会输出15.06848
}
```
* ClampMagnitude(Vector2 vector,roat maxLength); 给定一个二维向量，并且将其长度限定在一个范围内。

```C#
void Update () {
    Vector2 vector1 = new Vector2(3, 4);
    Vector2 vector2 = Vector2.ClampMagnitude(vector1, 2);
    Vector2 vector3 = Vector2.ClampMagnitude(vector1, 6);
    print(vector2);//(1.2,1.6)
    print(vector3);//(3.0,4.0)
}
```
* Distance(Vector2 a,Vector b); 取得两个坐标之间的距离/a到b的向量

```C#
void Update () {
    Vector2 vector1 = new Vector2(3, 4);
    Vector2 vector2 = new Vector2(2, 5);
    float a = Vector2.Distance(vector1, vector2);
    print(a);//a=1.414214
}
```
* Lerp 分别对向量的各个坐标进行差值运算
* LerpUnclamped(Vector2 a,Vector2 b,float t); when t=0,return a; when t=1,return b; when t=0.5,return (a+b)/2
* Max 返回长度较大的
* Min 返回长度较小的
* MoveTowards(Vector2 current,Vector2 target,float maxDistanceDeta);     输出由坐标current向target移动最大距离为maxDistanceDeta后的得到的坐标

```C#
void Update () {
    Vector2 vector1 = new Vector2(3, 4);
    Vector2 vector2 = new Vector2(2, 5);
    Vector2 vector3 = Vector2.MoveTowards(vector1, vector2, 1);
    Vector2 vector4 = Vector2.MoveTowards(vector1, vector2, 2);
    print(vector3);//(2.3,4.7)
    print(vector4);//(2.0,5.0)
}
```
### 关于三维向量Vector3
* 大部分二维向量的方法三维向量也是适用的
* back vector3(0,0,-1)
* down vector3(0,-1,0)
* forward vector(0,0,1)
* left vector3(-1,0,0)
* one vector3(1,1,1)
* right vector3(1,0,0)
* up vector3(0,1,0)
* zero vector3(0,0,0)
* Cross(Vector3 a,Vector3 b); a向量叉乘b向量，返回叉乘后的向量。右手叉乘法则：大拇指指向a，食指指向b，中指指向与大拇指食指垂直的方向，该方向就是叉乘向量的方向。

```C#
void Update () {
    Vector3 vector1 = new Vector3(1, 0, 0);
    Vector3 vector2 = new Vector3(0, 1, 0);
    Vector3 vector3 = Vector3.Cross(vector1, vector2);
    print(vector3);//(0.0, 0.0, 1.0);
}
```
* LerpUnclamped 差值运算。但是没有范围限制
* Project(Vector3 vector,Vector3 onNormal); 取得向量的投影

```C#
void Update () {
    Vector3 vector1 = new Vector3(3, 4, 5);
    Vector3 vector2 = new Vector3(8, 1, 8);
    Vector3 vector3 = Vector3.Project(vector1, vector2);
    print(vector3);//(4.2,0.5,4.2)
}
```
* reflect(Vector3 inDirection,Vector3 inNormal); 取得向量的反射向量

```C#
void Update () {
    Vector3 vector1 = new Vector3(3, 4, 5);
    Vector3 vector2 = new Vector3(0, 1, 0);
    Vector3 vector3 = Vector3.Reflect(vector1, vector2);
    print(vector3);//(3.0,-4.0,5.0)
}
```
* Slerp(Vector3 a,Vector3 b,float t) 进行向量/夹角差值运算
### 对向量的加减乘除操作
* Operators 向量运算
## 随机数
### 使用Random生成随机数
* Range

```C#
void Update () {
    float t = Random.Range(1.22f, 1.52f);
    print(t);//随机生成在1.22到1.52之间的小数
    int i = Random.Range(3, 5);
    print(i);//随机生成大于等3，小于5的整数
}
```
### 其他随机生成方法介绍
* value 生成一个0到1之间的小数
* rotation 得到一个随机旋转
* insideUnitCircle 在一个半径为1的圆内随机生成二维坐标 

```C#
void Update () {
    this.transform.position = Random.insideUnitCircle * 5;//让游戏物体随机移动到半径为5米的平面内
}
```
* insideUnitSphere 在一个半径为1的球内随机生成三维坐标 

```C#
void Update () {
    this.transform.position = Random.insideUnitSphere * 5;//让游戏物体随机移动到半径为5米的球内
}
```
# 如果有什么问题，欢迎指教
