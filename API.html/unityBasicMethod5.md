# 射线检测+事件接口
## 射线检测
### 射线检测之基本使用
```C#
//通过最简单的方法进行射线检测
Ray ray = new Ray(transform.position + transform.forward, transform.forward);//建立一条射线，并且给射线添加起点和方向
bool isCollision = Physics.Raycast(ray);//声明一个布尔值用来判断射线是否碰到游戏物体
print(isCollision);//输出布尔值，判断射线是否检测到了游戏物体
```
### 射线检测之重载方法
```C#
bool isCollision = Physics.Raycast(ray,1);//添加一个规定射线长度的变量，将射线的长度规定为1
```
```C#
bool isCollision = Physics.Raycast(ray, out hit);//通过out hit返回碰撞信息
print(hit.collider);//输出碰撞到的游戏物体的碰撞体(相当于输出碰撞到了哪个游戏物体)
print(hit.point);//输出发生碰撞的点
```
```C#
bool isCollision = Physics.Raycast(ray, Mathf.Infinity, LayerMask.GetMask("Default"));//Mathf.Infinity表示射线无限长，LayerMask.GetMask("Default")表示该射线只和Default发生碰撞
```
### 关于2D射线检测和检测碰撞到所有物体
* 只能和2d碰撞器发生检测
* Raycast只返回碰撞到的第一个游戏物体，RaycastAll可以以数组的形式返回所有碰撞到的游戏物体

### 通过代码添加对UGUI控件的事件监听
```C#
using System;
using UnityEngine.UI;
public class API13 : MonoBehaviour {
    public GameObject button;//声明ugui的按钮组件
    public GameObject slider;//声明ugui的滑块组件
    public GameObject dropdown;//声明ugui的下拉组件
	void Start () {
        button.GetComponent<Button>().onClick.AddListener(this.OnButton);//获取按钮组件的操作信息并且传递给OnButton()
        slider.GetComponent<Slider>().onValueChanged.AddListener(this.Onslider);//获取滑块组件的操作信息并且传递给Onslider()
        dropdown.GetComponent<Dropdown>().onValueChanged.AddListener(this.Ondropdowm);//获取下拉组件的操作信息并且传递给Ondropdowm()
    }
	void Update () {
	}
    void OnButton()
    {
        print("button");//如果按下按钮，输出"button"
    }
    void Onslider(float value)
    {
        print(value);//如果拖动滑块，输出滑块传递过来的fioat值
    }
    void Ondropdowm(Int32 num)
    {
        print(num);//如果操作下拉组件，输出下拉组件传递过来的int32类型的值
    }
}
```
## 事件接口
### 跟鼠标相关的事件接口的实现
```C#
using UnityEngine.UI;
using UnityEngine.EventSystems;//事件系统，添加鼠标事件实现的相关接口需要添加该类
using System;
public class API14 : MonoBehaviour,IPointerClickHandler,IPointerDownHandler,IPointerExitHandler,IPointerUpHandler,IPointerEnterHandler//添加接口
{   //此代码必须挂载在需要监听的UI组件下面，并且该UI组件的RaycastTarget必须勾选(默认勾选)。
    //假设该代码挂载在了Image组件下面
    public void OnPointerClick(PointerEventData eventData)//监测完整点击Image事件(包括按下和抬起)
    {
        Debug.Log("OnPointerClick");
    }
    public void OnPointerDown(PointerEventData eventData)//监测在Image上按下鼠标的事件
    {
        Debug.Log("OnPointerDown");
    }
    public void OnPointerEnter(PointerEventData eventData)//监测把鼠标移动到Image上面的事件
    {
        Debug.Log("OnPointerEnter");
    }
    public void OnPointerExit(PointerEventData eventData)//监测把鼠标从Image组件上面移开的事件
    {
        Debug.Log("OnPointerExit");
    }
    public void OnPointerUp(PointerEventData eventData)//监测在Image上抬起鼠标的事件
    {
        Debug.Log("OnPointerUp");
    }
}
```
### 跟拖拽相关的事件接口的实现
```C#
using UnityEngine.UI;
using UnityEngine.EventSystems;//事件系统，添加鼠标事件实现的相关接口需要添加该类
using System;
public class API14 : MonoBehaviour,IBeginDragHandler,IDragHandler,IEndDragHandler,IDropHandler//添加接口
{   //此代码必须挂载在需要监听的UI组件下面，并且该UI组件的RaycastTarget必须勾选(默认勾选)。
    //假设该代码挂载在了Image组件下面
    public void OnBeginDrag(PointerEventData eventData)//监测鼠标开始拖拽的事件
    {
        Debug.Log("OnBeginDragk");
    }
    public void OnDrag(PointerEventData eventData)//监测鼠标正在拖拽的事件
    {
        Debug.Log("OnDrag");
    }
    public void OnDrop(PointerEventData eventData)//如果在Image上结束拖拽时调用
    {
        Debug.Log("OnDrop");
    }
    public void OnEndDrag(PointerEventData eventData)//监测鼠标结束拖拽的事件
    {
        Debug.Log("OnEndDrag");
    }
}
```
### 如何通过WWW下载图片
```C#
//将一张网上的图片作为游戏物体的贴图
public string url = "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1543656667719&di=4a4f971369cd42297034a07ce53d411b&imgtype=0&src=http%3A%2F%2Fd.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F91ef76c6a7efce1b5ef04082a251f3deb58f659b.jpg";//输入图片网址
IEnumerator Start()
{
    using (WWW www = new WWW(url))
    {
        yield return www;
        Renderer renderer = GetComponent<Renderer>();
        renderer.material.mainTexture = www.texture;
    }
}
```
# 如果有什么问题，欢迎指教
