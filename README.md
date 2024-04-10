## Hololens开发问题及解决方案

本文档概述了Hololens开发中遇到的各种问题以及它们各自的解决方案。

官方步骤：https://learn.microsoft.com/zh-cn/windows/mixed-reality/develop/advanced-concepts/using-visual-studio?tabs=hl2

### 1. 在Visual Studio中部署时缺少“Device”按钮

**问题：** 在从Visual Studio部署软件到Hololens时，找不到“Device”按钮。

**解决方案：** 从Unity部署项目到通用Windows平台（UWP）后，它变成了一个 .sln 文件。但是，在Visual Studio中打开文件时，“Device”按钮可能不可见。在这种情况下，可以在Visual Studio右侧的“Solution Explorer”中导航到“YourProjectName”，右键单击它，然后选择“Set as Startup Project”，如下图所示：

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/0531de47-9402-433e-a74d-43d1d4fce86d)

来源：https://blog.csdn.net/Autumn_horse/article/details/115800329

### 2. 错误消息“WindowsMobile version 10.0.xxx.0”
**问题：** 错误消息指示与“WindowsMobile version 10.0.xxx.0”相关的问题。

**解决方案：** 

原因：Visual Studio（VS）使用位于“C:\Program Files (x86)\Windows Kits”中的默认UWP相关SDK进行编译。
解决方案1：在Solution Explorer中，导航到[Project] > References > Windows Mobile（带有黄色感叹号），然后将其删除。
通过编辑项目文件并添加以下ItemGroup，手动将WindowsMobile SDK添加回来：

```xml
<ItemGroup>
    <SDKReference Include="WindowsMobile, Version=10.0.18362.0"/>
</ItemGroup>
```


解决方案2：从目录“C:\z\Extension SDKs\WindowsMobile”手动复制安装的WindowsMobile SDK到“C:\Program Files (x86)\Windows Kits\10\Extension SDKs”中。

来源：https://blog.csdn.net/shenyi0_0/article/details/105874219

### 3. 使用“通用身份验证”连接Hololens时失败

**问题：** 使用“通用身份验证”连接Hololens失败，部署失败，PIN输入框不显示。

**解决方案：** 在比较VS组件时发现缺少USB设备连接组件。

USB设备连接

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/4a1a26da-a2e7-4147-bf47-493451843c8e)

### 4. 材质着色器选择时的双面渲染问题

**问题：** 一些材质着色器选择MRTK，导致双面渲染问题。

双面渲染，选择**关闭**作为**Dull Mode**

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/f2429aa7-40ed-40f3-ba91-0831f75dc4d0)
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/eff043c8-064a-444e-8735-bd49a52c81ad)

注意到有些材料没有此选项，可能需要更改材料。

### 5. 在Hololens设备上显示平面框架而不是MR版本

**问题：** 从Unity使用Visual Studio部署到真实设备后，设备显示平面框架而不是MR版本。

在项目设置的XR插件管理中选择启动时的初始XR。
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/e92d2798-a796-42f3-a93d-f8aa584223dd)

### 6. 在Hololens设备上缺少显示和“Made with Unity”消息

**问题：** 从Unity使用Visual Studio部署到真实设备后，没有显示和没有“Made with Unity”消息。

**解决方案：** 尝试在Unity项目中切换场景。尝试不同的场景，直到成功部署一个为止。一旦识别出一个功能性场景，请将原始项目的资产集成到此场景中。

然而，即使是MRTK2的源项目也没有起作用，仍然没有显示。后来，切换到MRTK3后仍然没有显示，但是额外的启动图标和四个不断显示的点出现了。最后，解决方案是切换场景，最终找到了一个可用的场景并成功部署。基于这个成功的场景，将您的资产复制粘贴到其中。最终部署设置在VS2019 Studio中以ARM发布。
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/81d4350f-cf75-4927-b134-f768f5fc355c)

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/f08a8033-e448-49fb-a714-fe7e8d5aab65)

并选择'Run Without Debugging'

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/501287d4-dd59-469c-9c2d-72902eded02a)

在第一次部署时，它会要求您输入PIN，您可以在HoloLens中找到它。

这些解决方案应该有助于解决Hololens开发中遇到的各种问题，确保开发工作的顺利进行。

如果您遇到其他问题，请随时在本页面分享。如果你觉得有用，帮忙点一下星星。
