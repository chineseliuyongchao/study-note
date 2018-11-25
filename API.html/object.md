# 基本方法
## 事件函数
+ start 方法开始运行时执行一次  
+ update 方法每一帧调用一次  
+ reset 方法当游戏物体激活或者transform重置时候调用  
+ awake 方法当场景运行时调用  
+ fixedupdate 方法会每秒固定调用一定的次数  
+ lateupdate 方法每一帧调用一次，在update方法之后调用  
+ onTrigger 触发器  
+ onCollision 碰撞器  
+ OnApplicationPause 在游戏暂停时候调用  
+ OnApplicationQuit 在游戏暂停时候调用   
## Time类中静态变量介绍
+ deltatime 大约每1/60秒调用一次  
+ fixdeltatime 每一帧需要的时间  
+ fixedtime 游戏开始到现在所需要的时间  
+ framecount 游戏开始到现在运行了多少帧  
+ timescale 控制游戏速度  
## time.deltatime和realTimeSinceStartup的使用
deltatime可以让游戏物体匀速运动，不受帧数影响
```c#
transform.Translate(Vector3.forward*Time.deltaTime);

timescale可以更改deltatime的速率

Time.timeScale = 2;//改变Time.deltaTime的速率，默认是1

realTimeSinceStartup可以记录游戏运行的时间，也可以测量某一段代码运行时间
```

```C#

float time1 = Time.realtimeSinceStartup;//记录当前时间
for(int j = 0; j < num; j++)
{
    fun1();
}
float time2 = Time.realtimeSinceStartup;
Debug.Log(time1 - time2);
```
## 创建游戏物体的三种方法
```c#

void Start () {//三种创建游戏物体的方式
    new GameObject("Cube");
    GameObject.Instantiate(prefabs);//根据prefab或者根据其他游戏物体创建另外一个游戏物体
    GameObject game = GameObject.CreatePrimitive(PrimitiveType.Cube);//创建基本游戏物体
}
```
## 通过代码给游戏物体添加组件

```c#
game.AddComponent<Rigidbody>();//给游戏物体添加组件
```
## 禁用和激活游戏物体

+ activeinHierarchy 判断游戏物体是否被禁用（子物体会随着父物体的禁用而被禁用）  
+ tag 每一个游戏物体都有标签  
+ activeself 判断游戏物体是否被禁用（子物体不会随着父物体的禁用而被禁用）  
+ 通过setActive禁用游戏物体

```c#
prefabs.SetActive(false);
```

## unityEngine下object拥有的静态方法

destroy 销毁游戏物体或者组件（unity会统一回收，放入垃圾池，确认无用后销毁）

```c#
Destroy(this);
Destroy(gameObject);
Destroy(rigidbody);
```

+ FindObjectOfType 在场景当中搜索所有游戏物体中的所有组件并且返回第一个  
+ FindObjectsOfType 在场景当中搜索所有游戏物体中的所有组件并且返回所有的  
+ enabled 可以禁用或者启用组件

```c#
Light light=GameObject.FindObjectOfType<Light>();//获取组件
light.enabled = false;
Transform[]ts=FindObjectsOfType<Transform>();//不查找未激活的游戏物体
foreach(Transform t in ts)
{
    Debug.Log(t);
}
```

Instantiate 实例化游戏物体  

## Gameobject独有的静态方法

+ Find 查找游戏物体  
+ FindGameObjectsWithTag 根据标签查找所有的游戏物体  
+ FindGameObjectWithTag 根据标签查找游戏物体并且返回第一个

```c#
GameObject go = GameObject.Find("Main Camera");
GameObject go1 = GameObject.FindGameObjectWithTag("Main Camera");
```

## 游戏物体间消息的发送和接收

GameObject.BroadcastMessage 广播消息

```c#
public class API04 : MonoBehaviour {
    public GameObject game;
	void Start () {
        game.BroadcastMessage("Attake", 5, SendMessageOptions.DontRequireReceiver);//该游戏物体的所有子物体调用该方法
        //SendMessageOptions.DontRequireReceiver可以保证在找不到方法时不会报错
	}
}
```

GameObject.SendMessage 给该游戏物体发送一个消息  

```c#
game.SendMessage("Attake", 5, SendMessageOptions.DontRequireReceiver);//调用该游戏物体的"Attake"方法
```

GameObject.SendMessageUpawards 调用该游戏物体以及他的父物体的某个方法

```c#
game.SendMessageUpawards("Attake", 5, SendMessageOptions.DontRequireReceiver);//调用该游戏物体的"Attake"方法
```
## 得到组件的各种方法函数
* GetComponent 查找该游戏物体的一个某种组件
* GetComponentInChildren 查找该游戏物体以及其子物体的一个某种组件
* GetComponentInParent 查找查找该游戏物体以及其父物体的一个某种组件
* GetComponent 查找该游戏物体所有某种组件
* GetComponentInChildren 查找该游戏物体以及其子物体的所有某种组件
* GetComponentInParent 查找查找该游戏物体以及其父物体的所有某种组件
## MonoBehaviour总览
* ExecuteInEditMode 可以让放在后面的代码在编译器模式下面运行。
```C#
using UnityEngine;
[ExecuteInEditMode]
public class API05 : MonoBehaviour {
	void Start () {
        print(123);
	}
	void Update () {
        print(234);
	}
}
```
* Inoke 延迟时间调用函数
* InvokeRepeating 延迟时间重复调用函数
* CancelInvoke 结束调用所有Invoke和InvokeRepeating方法
* print 输出，适用于测试bug
* isActiveAndEnabled 用于判断当前组件是否启用
* enabled 用于激活或者禁用某个组件
## MonoBehaviour里面的常用变量
* tag 游戏物体的标签
* gameObject 获取游戏物体
* transform 获取游戏物体的transform组件（每个游戏物体都有一个transform组件）
* name 获取游戏物体的名字
## MonoBehaviour中Invoke的使用
* Inoke 延迟时间调用函数
* InvokeRepeating 延迟时间重复调用函数
* CancelInvoke 结束调用所有Invoke和InvokeRepeating方法
```C#
public class API05 : MonoBehaviour {
    int i = 0;
	void Start () {
	}
	void Update () {
        //Invoke("Fire", 1.0f);
        Invoke("Fire",1.0f);//第一个参数，方法名。第二个参数，延迟时间。
        InvokeRepeating("Firee", 1.0f, 2);//第一个参数，方法名。第二个参数，延迟时间。第三个参数，重复执行间隔
        if (i > 10)
        {
            CancelInvoke();//结束调用所有Invoke和InvokeRepeating方法
        }
    }
    void Fire()
    {
        print(123);
    }
    void Firee()
    {
        print(456);
        i++;
    }
}
```
# 如果哪里有问题，欢迎指教
