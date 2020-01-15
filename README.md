# Develop VR applications in Unity for Oculus Quest

## Setup
---

### Install latest Unity version
1. Install one of the latest Unity version. For this tutorial we are using the latest official Unity version 2019.2.17f1. You can download and install the latest Unity version by going to Installs in the Unity Hub and selecting Add.
2. Select the latest release and click next
3. Add the latest Android Build Support tools
4. Click done

### Create project
1. Create a new Unity project with the latest Unity version, 3D template and select a name and location for your new project.

### Install Oculus Integration
1. Go to Window -> Asset Store and search for Oculus Integration
2. Download the package
3. Import the package
4. Update the Oculus Utilities Plugin, if requested
5. Update Spatializer Plugins, if requested
6. Restart Unity

### Install Oculus Android & Desktop
1. Go to Window -> Package Manager and scroll down to Oculus Android & Oculus Desktop
2. Install the Oculus Android package
3. Install the Oculus Desktop package

### Oculus Application ID
1. Go to Oculus -> Platform & select **Edit Settings**
2. Click on the **'Create / Find your app'** button
3. Your browser will open to the Oculus Dashboard. Sign in.
4. In the **Dashboard**, create a new app, give in a name and select **'Oculus GO & Gear VR'** as a platform.
5. Copy the App ID displayed on the next page
6. Open Unity and paste the Application ID in both the Oculus Rift & Oculus Go/Quest field
7. In Unity Editor Settings, disable the **'Use Standalone Platform'**

### Project Settings
1. Go to Edit -> **Project Settings** and select Player.
2. Change the **Company name** and **Product name**
3. Click on the Android icon to switch to the Android tab.
4. Click on **XR settings** (on the Android tab)
5. Enable **Virtual Reality Supported**
6. Click on the + icon and add Oculus
7. Enable V2 signing if you are building for Oculus Quest (Disable for Rift and Go)
8. Scroll up to **Other Settings**
9. Remove **Vulkan** from the **Graphics APIs**
10. Change the **Minimum API level** to version 4.4 (API level 19 - KitKat)
11. For VRTK4, you can change the Api Compatibility Level to .NET 4.x
12. Select **Time** at the left side of the Project Settings and change the **Fixed Timestep** to **1/90**. Unity checks frames 60 times per second, and not 90 times per seconds, which is required in VR. 

### Build Settings
1. Go to File -> **Build Settings** and select Android on the left side
2. Click on **Switch platform**. This can take some time.
3. For development iteration, leave Texture Compression to **'Don't override'**!

### USB Debugging
1. Connect your Oculus Quest to your computer using the provided USB C cable.
2. Open the Oculus app on your smartphone, pair & connect with your Quest.
3. Go to More Settings ->  Developer Mode Settings -> Enable Developer Mode.
4. Accept the request in your Oculus Quest.
5. In Unity, refresh the device list and you will be able to see your connected Quest.

## Extra: ProBuilder & ProGrids
ProBuilder is a tool that gives Unity the ability to edit the shape of primitive objects. This allows us to make more complex gameobjects. And ProGrids is a tool (similar to the Snap Settings in Edit -> Snap Settings) that will snap whatever it is we are doing, whether it be editing, scaling or rotating, to a grid. This allows for a very uniform look on our gameobjects.

1. Go to Window -> Package Manager
2. Search and install ProBuilder
3. At the time of writing, ProGrids is still in preview. Select Advanced next to the Search Bar and select 'Show Preview Packages'
4. Search and install ProGrids.
5. Go to Tools -> ProBuilder -> ProBuilder Window

## Oculus Virtual Reality
---
The OVR Utilities Plugin (OVRPlugin) provides Rift and Android support to the Unity Editor.
All Unity versions 5.1 and later ship with a bundled version of OVRPlugin that provides built-in support for Rift, Oculus Go, and Samsung Gear VR.

### OVRCameraRig
**OVRCameraRig** is a custom VR camera that may be used to replace the regular Unity Camera in a scene. 

The primary benefit to using **OVRCameraRig** is that it provides access to **OVRManager**, which provides the main interface to the VR hardware. If you do not need such access, a standard Unity camera may be easily configured to add basic VR support.

**OVRCameraRig** is a Component that controls stereo rendering and head tracking. It maintains three child “anchor” Transforms at the poses of the left and right eyes, as well as a virtual “center” eye that is halfway between them.
It is the main interface between Unity and the cameras. It is attached to a prefab that makes it easy to add comfortable VR support to a scene.

The **OVRCameraRig** is perfect for games that require a standing experience like Pistol Whip, Beat Saber, .. since you are not required to move around using teleportation or joystick movement.

Drag an OVRCameraRig into your scene and you will be able to start viewing the scene.
Select the **OVRCameraRig*** in the Player Controller and set the **Tracking Origin Type** to **Floor**.

**OVRManager**
**OVRManager** is the main interface to the VR hardware. It is a singleton that exposes the Oculus SDK to Unity, and includes helper functions that use the stored Oculus variables to help configure camera behavior.

This component is added to the **OVRCameraRig** prefab. It can be part of any application object. However, it should only be declared once, because it includes public members that allow for changing certain values in the Unity Inspector. If OVRManager is present in your scene, VR will be automatically enabled.

**Tracking Origin Type**
* **Eye Level**: Track the position and orientation y-axis relative to the HMDs position. 
* **Floor Level**: Track position and orientation relative to the floor, based on the users standing height as specified in the Oculus Configuration Utility. 
* **Stage Level**: Has its origin on the floor at the center of the play area with its forward direction pointed towards one of the edges of the bounding box of the play area. Not affected by user-initiated recenter. For example, an app might dynamically layout furniture to take advantage of the full guardian space defined by the user. 


**OVR Headset Emulator**
The **OVRCameraRig** contains an **OVRHeadsetEmulator** script that helps the development for Virtual Reality applications on your PC. With this script you will be able to move the player and move your mouse whole holding the control key.

### OVRPlayerController
The **OVRPlayerController** is the easiest way to start navigating a virtual environment. It is basically an **OVRCameraRig prefab** attached to a simple **character controller**. It includes a **physics capsule**, a **movement system**, a simple menu system with **stereo rendering** of text fields, and a **cross-hair component**.

To use, drag the player controller into an environment and begin moving around using a gamepad, or a keyboard and mouse.
Select the **OVRCameraRig** in the Player Controller and set the **Tracking Origin Type** to **Stage**.

### Adding controllers
You can add hands, controllers, cubes, ... by dragging the game object (hand, 3d model, cube) to the respective hand anchors in the **Tracking Space** of the **OVRCameraRig**.
In your **Project View**, search for *OculusTouchForQuestAndRiftS_Left* and *OculusTouchForQuestAndRiftS_Right* and drag it on the respective **LeftControllerAnchor** and **RightControllerAnchor**. The controllers track the position of the anchors and their transforms are adjusted, following it.

### Oculus Link
Oculus Link is here! Since there's little information available so far, here's a quick guide.

1. The cables that ship with the Oculus Quest don't work (even though the set up in Oculus Desktop shows that), you will need a good USB 3 to USB C cable.
2. Oculus Desktop app, Library > Update > download update (v1.43)
3. Restart app, update app, connect Quest, update Quest
4. Oculus Desktop App > Settings > General > enable Unknown Sources
5. In your Quest, enable Oculus Link by plugging it in or enabling in your settings
6. In Oculus Link, connect to your Unity project using Add Desktop Panel (+ icon)
 
You should be able to run your scene in your headset once you press play
You don't need to modify your Quest project to work right away with Oculus Link.
Should work with all versions of Unity listed by Oculus.
Works with Oculus Integrations 1.41 - Doesn't work with 1.38

More information: https://support.oculus.com/444256562873335/

Other notes
My controllers were in 3dof and invisible when I entered Oculus Link, restarting my quest/computer fixed that
The hands will turn into controllers when they stop registering input
The mouse in the virtual desktop disappears when both hands turn into controllers or the pointer is off screen
If you run Unity from Explore/Library, it will launch the project. You can't tell which project it'll open, so I choose to open it on my computer then Add Desktop Panel



