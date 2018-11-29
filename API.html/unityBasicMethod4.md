# 欧拉角与四元数+Application+SceneManager
## 欧拉角与四元数
### Quaternion四元数介绍以及和欧拉角的区别
* 在Inspector界面中，修改游戏物体的Transform.Rotation时，修改xz轴是围绕自身坐标系，修改y轴是围绕世界坐标系

```C#
print(this.transform.eulerAngles);//当游戏物体在初始位置时，输出(0.0,0.0,0.0)
print(this.transform.rotation);//当游戏物体在初始位置时，输出(0.0,0.0,0.0,1.0)
this.transform.rotation = new Vector3(5, 5, 5);//由于transform.rotation是四元数，所以不能用三维变量赋值，所以会报错
this.transform.eulerAngles = new Vector3(5, 5, 5);//transform.eulerAngles反映了游戏物体的三维旋转量，所以可以用三维变量赋值
```
### Quaternion中的LookRotation方法
* Euler 可以把一个欧拉角变成四元数

```C#
//两种让游戏物体xyz轴的旋转都变成45°的方法 
this.transform.eulerAngles = new Vector3(45, 45, 45);//直接给欧拉角赋值
this.transform.rotation = Quaternion.Euler(new Vector3(45, 45, 45));//通过把三维变量转换为四元数，然后赋给游戏物体
```
* eulerAngles 可以把一个四元数变为欧拉角

```C#
print(this.transform.rotation.eulerAngles);//(0.0,0.0,0.0)
```
* LookRotation 可以把一个向量转换成一个四元数类型的方向
* 下面是一个控制主角面朝敌人的方法(z轴朝向)

```C#
public class API09 : MonoBehaviour {
    public GameObject palyer;//声明一个作为主角的游戏物体
    public GameObject enemy;//声明一个作为敌人的游戏物体
	void Start () {
        Vector3 vector3 = enemy.transform.position - palyer.transform.position;//计算出从主角到敌人的向量
        vector3.y = 0;//让计算出的向量的y轴等于0，使主角不会倾斜
        palyer.transform.rotation = Quaternion.LookRotation(vector3);//将计算出的向量转换成四元数形式的旋转方向并且赋给主角
    }
```
### Quaternion中的Lerp和Slerp插值运算
* Slerp 球形差值运算
* Lerp 线性插值

```c#
public class API09 : MonoBehaviour {
    public GameObject palyer;//声明一个作为主角的游戏物体
    public GameObject enemy;//声明一个作为敌人的游戏物体
	void Update () {
        Vector3 vector3 = enemy.transform.position - palyer.transform.position;//计算出从主角到敌人的向量
        vector3.y = 0;//让计算出的向量的y轴等于0，使主角不会倾斜
        Quaternion target = Quaternion.LookRotation(vector3);//将计算出的向量转换成四元数形式的旋转方向并且赋给主角
        palyer.transform.rotation = Quaternion.Slerp(palyer.transform.rotation, target, Time.deltaTime);//通过差值运算让主角缓慢朝向敌人
    }
}
```
### Rigidbody刚体组件中position和MovePosition控制移动
* centerOfMass 取得游戏物体的重心
* freezeRotaition 冻结旋转

```C#
this.GetComponent<Rigidbody>().constraints = RigidbodyConstraints.FreezeRotation;//将游戏物体的旋转锁定
this.GetComponent<Rigidbody>().constraints -= RigidbodyConstraints.FreezeRotation;//将游戏物体的旋转解除
```
* position/rotation 通过刚体控制游戏物体的移动，比在transform修改节约性能

```C#
this.GetComponent<Rigidbody>().position = this.transform.position + Vector3.forward * Time.deltaTime;//让小球向前做运动
```
* MovePosition 通过差值运算控制游戏物体的移动，可以让小球移动的更加平滑

```C#
this.GetComponent<Rigidbody>().MovePosition(this.transform.position + Vector3.forward * Time.deltaTime * 50);//让小球向前做运动
```
### 通过刚体控制游戏物体旋转

```C#
public class API09 : MonoBehaviour {
    public GameObject palyer;//声明一个作为主角的游戏物体
    public GameObject enemy;//声明一个作为敌人的游戏物体
	void Update () {
        Vector3 vector3 = enemy.transform.position - palyer.transform.position;//计算出从主角到敌人的向量
        vector3.y = 0;//让计算出的向量的y轴等于0，使主角不会倾斜
        Quaternion target = Quaternion.LookRotation(vector3);//将计算出的向量转换成四元数形式的旋转方向并且赋给主角
        palyer.GetComponent<Rigidbody>().rotation = Quaternion.Lerp(palyer.transform.rotation, target, Time.deltaTime);//通过差值运算让主角缓慢朝向敌人

    }
}
```
### 通过AddForce控制运动
* AddForce 通过给游戏物体施加力来控制游戏物体的移动

```C#
this.GetComponent<Rigidbody>().AddForce(10,1,1);//分别在三个轴上面给游戏物体施加力,因为有摩擦力，所以当力足够大时，游戏物体才会运动
```
### Camera类的学习和常用方法
* 通过照相机的射线检测将鼠标碰到的游戏物体输出

```C#
public class API10 : MonoBehaviour {
    private Camera maincamera;//声明一个照相机
	void Start () {
        maincamera = Camera.main;//让这个照相机等于主照相机
	}
	void Update () {
        Ray ray = maincamera.ScreenPointToRay(Input.mousePosition);//将鼠标所在位置的坐标转换成一条从摄像机的屏幕上面发出的射线
        RaycastHit hit;//声明一个用来存储射线检测信息的变量
        bool isCollision = Physics.Raycast(ray, out hit);//声明一个布尔值用来判断射线是否碰到游戏物体，并且通过hit返回碰撞信息
        if (isCollision)//如果射线碰撞到了游戏物体
        {
            print(hit.collider);//输出碰撞到的游戏物体
        }
	}
}
```
* 将上面那射线打印出来

```C#
Ray ray = maincamera.ScreenPointToRay(Input.mousePosition);//将鼠标所在位置的坐标转换成一条从摄像机发出的射线
Debug.DrawRay(ray.origin, ray.direction*10, Color.red);//将射线打印出来，ray.origin表示射线的起点，ray.direction表示射线的方向
```
## Application
### 通过Application获取datapath
* Streaming Assets 在发布的时候unity里面的大部分资源都会合并，但是有一些文件不需要合并，可以直接在StreamingAssets文件夹中读取。

```C#
print(Application.dataPath);//返回存放工程所需要的路径
print(Application.streamingAssetsPath);//返回可以通过文件浏览读取的一些数据
print(Application.persistentDataPath);//返回可以进行实例化的数据
print(Application.temporaryCachePath);//返回临时存储的数据
```
### Application中的常用静态变量和静态方法
* File→BuildSetting→PlayerSetting→CompanyName 设置工程名
* File→BuildSetting→PlayerSetting→ProjectName 设置游戏名(游戏发布以后将会以这个名字命名)
* IsMobilePlatform 是否在安卓平台上运行
* IsPlaying 是否在编译器模式下运行
* Platform 判断在哪个平台下面运行
* runInbackground 判断游戏是否可以在后台运行(移动平台不行)
* quit 用来退出应用

```C#
public class API11 : MonoBehaviour {
	void Start () {
        print(Application.identifier);//com.Company.productName  默认标识
        print(Application.companyName);//DefaultCompany  没有设置，默认
        print(Application.productName);//roll a ball  工程名字
        print(Application.installerName);//  没有安装名
        print(Application.installMode);//Editor  编译器模式下
        print(Application.isEditor);//True  编译器模式下
        print(Application.isFocused);//True  编译器模式下，游戏视图处于焦点
        print(Application.isMobilePlatform);//False  当前不是移动平台
        print(Application.isPlaying);//True  游戏正在运行
        print(Application.platform);//WindowsEditor  在windows下的编辑器
        print(Application.unityVersion);//2018.2,15f1  版本
        print(Application.version);//1.0  游戏版本
        print(Application.runInBackground);//False  不能在后台运行

        Application.Quit();//在编辑器以外退出游戏
        Application.OpenURL("www.sikiedu.com");//打开网页"www.sikiedu.com"
    }
	void Update () {
        if (Input.GetKeyDown(KeyCode.Space))//如果按下空格键
        {
            UnityEditor.EditorApplication.isPlaying = false;//在编译器中退出游戏
        }
	}
}
```
## SceneManager
### 如何切换加载场景
* SceneManager.LoadScene(a); //加载第a个场景
* SceneManager.LoadSceneAsync(a);//异步加载场景a
### 关于SceneManager的其他方法
* ScenceCount 当前加载的场景数量
* GetActiveScence 获得当前加载的场景

```C#
using UnityEngine.SceneManagement;
public class API11 : MonoBehaviour {
	void Start () {
        print(SceneManager.sceneCount);//1  场景数量
        print(SceneManager.sceneCountInBuildSettings);//1  生成设置的场景数
        print(SceneManager.GetActiveScene().name);//New Scence  当前场景名字
        print(SceneManager.GetSceneAt(0).name);//New Scence  第0个场景的名字
    }
```
# 如果有什么问题，欢迎指教
