# Hololens_dev_issue
to list the problem and the solution in Hololens development

official step: https://learn.microsoft.com/zh-cn/windows/mixed-reality/develop/advanced-concepts/using-visual-studio?tabs=hl2

1. 在Visual Studio部署软件到Hololens时，没有发现“设备”按钮的问题

在Unity将项目部署到Universal Windows Platform平台后，会成为一个sln文件，但是在VisualStudio打开文件后，没有发现“设备按钮，如图。

这时只要在VS中右侧的“解决方案资源管理器”中，右侧点击“YourProjectName”，并选择”设为启动项目即可，如图。

 ![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/0531de47-9402-433e-a74d-43d1d4fce86d)
 
source:https://blog.csdn.net/Autumn_horse/article/details/115800329

2. 报错信息“WindowsMobile  version 10.0.xxx.0”

Bug原因：

VS在编译的时候是默认UWP相关SDK在C:\Program Files (x86)\Windows Kits中的

解决方案一：

在解决方案资源管理器中找到  [项目]>引用>Windows Mobile（带黄色感叹号）

直接右键删掉

加回的方法：

编辑工程文件,添加下面 ItemGroup。

<ItemGroup>
    <SDKReference Include="WindowsMobile, Version=10.0.18362.0"/>
</ItemGroup>
解决方案二：(亲测可用）

把手动安装的WindowsMobile SDK从目录

C:\z\Extension SDKs\WindowsMobile

拷贝到

C:\Program Files (x86)\Windows Kits\10\Extension SDKs\

Source: https://blog.csdn.net/shenyi0_0/article/details/105874219

3.
Hololens 未能使用“通用身份验证”连接到设备的问题 部署失败 解决方案
连pin码输入框都不弹出
VS部署的设置为Release和ARM64 设备
也尝试过Release和ARM64 远程
发现远程可以弹框 并部署

对VS组件进行一一对比之后发现缺少 USB设备连接性 组件
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/4a1a26da-a2e7-4147-bf47-493451843c8e)

  source:https://blog.csdn.net/weixin_44558405/article/details/115527190

 4. 双面渲染问题，有的materialshader选用MRTK
    ![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/bed05fbf-c4a1-4cd1-b719-73cc705e7881)

