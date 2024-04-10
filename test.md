## Hololens Development Issues and Solutions

This document outlines various issues encountered during Hololens development along with their respective solutions.

official step: https://learn.microsoft.com/zh-cn/windows/mixed-reality/develop/advanced-concepts/using-visual-studio?tabs=hl2

### 1. Absence of "Device" Button in Visual Studio during Deployment

**Problem:** Upon deploying software from Visual Studio to Hololens, the "Device" button is not found.

**Solution:** After deploying the project from Unity to Universal Windows Platform (UWP), it becomes a .sln file. However, upon opening the file in Visual Studio, the "Device" button may not be visible. In such cases, navigate to the "Solution Explorer" on the right side of Visual Studio, right-click on "YourProjectName", and select "Set as Startup Project", as illustrated below:

 ![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/0531de47-9402-433e-a74d-43d1d4fce86d)
 
source:https://blog.csdn.net/Autumn_horse/article/details/115800329

### 2. Error Message "WindowsMobile version 10.0.xxx.0"
**Problem:**: Error message indicates an issue with "WindowsMobile version 10.0.xxx.0".

**Solution:** 

Cause: Visual Studio (VS) compiles with default UWP-related SDK located in "C:\Program Files (x86)\Windows Kits".
Solution 1: In Solution Explorer, navigate to [Project] > References > Windows Mobile (with yellow exclamation mark) and delete it.
Solution 2: Manually add the WindowsMobile SDK back by editing the project file and adding the following ItemGroup:


<ItemGroup>
    <SDKReference Include="WindowsMobile, Version=10.0.18362.0"/>
</ItemGroup>
     
Alternatively, copy the manually installed WindowsMobile SDK from the directory "C:\z\Extension SDKs\WindowsMobile" to "C:\Program Files (x86)\Windows Kits\10\Extension SDKs". 

Source: https://blog.csdn.net/shenyi0_0/article/details/105874219

### 3. Failure to Connect Hololens Using "Universal Authentication" with Deployment
**Problem:**: Hololens fails to connect using "Universal Authentication", deployment fails, and the PIN input box does not appear.

**Solution:**  Upon comparing VS components, it's discovered that the USB Device Connectivity component is missing.

USB Device Connectivity


![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/4a1a26da-a2e7-4147-bf47-493451843c8e)

### 4. Dual-sided Rendering Issue with Material Shader Selection
**Problem:**: Some material shaders select MRTK, causing dual-sided rendering issues.

Dual-sided Rendering, select the **Dull Mode** as **OFF**

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/f2429aa7-40ed-40f3-ba91-0831f75dc4d0)
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/eff043c8-064a-444e-8735-bd49a52c81ad)

it is noted that some of the materials do not have the option, you may need to change the material.

### 5. Display of Plane Frame Instead of MR Version on Hololens Device
**Problem:**: After deploying from Unity to a real device using Visual Studio, the device displays a plane frame instead of the MR version.

Select the initial XR on startup in XR Plug-in Management of the project settings.
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/e92d2798-a796-42f3-a93d-f8aa584223dd)


### 6. Absence of Display and "Made with Unity" Message on Hololens Device
**Problem:**: After deploying from Unity to a real device using Visual Studio, there is no display and no "Made with Unity" message.

**Solution:**  Try switching scenes within the Unity project. Experiment with different scenes until one successfully deploys. Once a functional scene is identified, integrate assets from the original project into this scene.


However, even the source project of MRTK2 did not work, and there was still no display. Later, after switching to MRTK3, there was still no display, but an additional startup icon and four constantly displayed dots were present. Finally, the solution was to switch scenes, and finally, a usable one was found and successfully deployed. Based on this successful scene, copy and paste your assets into it. The final deployment setting is released with ARM in VS2019 stuidio.
![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/81d4350f-cf75-4927-b134-f768f5fc355c)

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/f08a8033-e448-49fb-a714-fe7e8d5aab65)

and select 'Run Without Debugging'

![image](https://github.com/yuanzero/Hololens_dev_issue/assets/26519097/501287d4-dd59-469c-9c2d-72902eded02a)

on your first deployment, it will ask you to input the PIN, which you can find in HoloLens.

These solutions should help address various issues encountered during Hololens development, ensuring smoother progress in development endeavors. 

If you encounter any other issues, feel free to share them on this page.
