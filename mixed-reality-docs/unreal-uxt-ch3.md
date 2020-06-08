---
title: 3. Setting up your project for mixed reality
description: Part 3 of 6 in a tutorial series to build a simple chess app using Unreal Engine 4 and the Mixed Reality Toolkit UX Tools plugin
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, mixed reality, tutorial, getting started, mrtk, uxt, UX Tools, documentation
---

# 3. Setting up your project for mixed reality

## Overview

In the previous tutorial, you spent time setting up the chess app project. This section is going to walk you through setting up the app for mixed reality development, which means adding an AR session. You'll be using an ARSessionConfig data asset for this task, which has a lot of useful AR settings like spatial mapping and occlusion. If you want to dive deeper, the Unreal Engine documentation has more details on the [ARSessionConfig](https://docs.unrealengine.com/en-US/PythonAPI/class/ARSessionConfig.html) asset and the [UARSessionConfig](https://docs.unrealengine.com/en-US/API/Runtime/AugmentedReality/UARSessionConfig/index.html) class.

## Objectives
* Working with Unreal Engine's AR settings 
* Using an ARSessionConfig data asset
* Setting up a Pawn and game mode

## Adding the session asset
AR sessions in Unreal don't happen by themselves. To use a session you need an ARSessionConfig data asset to work with, which is your next task:

1. Click **Add New > Miscellaneous > Data Asset** in the **Content Browser**. Make sure you're at the root **Content** folder level. 
    * Select **ARSessionConfig**, click **Select**, and name the asset **ARSessionConfig**.

![Create a data asset](images/unreal-uxt/3-createasset.PNG)

3. Double-click **ARSessionConfig** to open it, leave all default settings and hit **Save**. Return to the Main window. 

![AR Session Config](images/unreal-uxt/3-arsessionconfig.PNG)

With that done, your next step is to make sure that the AR session starts when the level loads. Luckily, Unreal has a special kind of blueprint called a **Level Blueprint** that acts as a level-wide global event graph. Connecting the ARSessionConfig asset in the **Level Blueprint** guarantees the AR session will fire right when the game starts playing.

1. Click **Blueprints > Open Level Blueprint** from the editor toolbar: 

![Open Level Blueprint](images/unreal-uxt/3-level-blueprint.PNG)

5. Drag the execution node (left-facing arrow icon) off **Event BeginPlay** and release. Search for the **Start AR Session** and hit enter.  
    * Click the **Select Asset** dropdown under **Session Config** and choose the **ARSessionConfig** asset. 
    * Hit **Compile**, then **Save** and return to the Main window.

![Start AR Session](images/unreal-uxt/3-start-ar-session.PNG)

## Create a Pawn
At this point, the project still needs a player object. In Unreal, a **Pawn** represents the user in the game, but in this case it's going to be the HoloLens 2 experience.

1. Click **Add New > Blueprint Class** in the **Content** folder and expand the **All Classes** section at the bottom. 
    * Search for **DefaultPawn**, click **Select** and double-click the asset to open. 

![Create a new Pawn inheriting from DefaultPawn](images/unreal-uxt/3-defaultpawn.PNG)

> [!NOTE]
> By default, Pawns have mesh and collision components. In most Unreal projects, Pawns are solid objects that can collide with other components. Since the Pawn and user are the same in mixed reality, you want to be able to pass through holograms without any collisions. 

2. Select **CollisionComponent** from the **Components** panel and scroll down to the **Collision** section of the **Details** panel. 
    * Click the **Collision Presets** dropdown and change the value to **NoCollision**. 
    * Do the same for the **MeshComponent**, then **Compile** and **Save** the Blueprint. 

![Adjust the Pawn's Collision Presets](images/unreal-uxt/3-nocollision.PNG)

With your work here done, return to the Main Window.

## Create a Game Mode
The last puzzle piece of the mixed reality setup is the Game Mode. The Game Mode determines a number of settings for the game or experience, including the default pawn to use.

1.	Click **Add New > Blueprint Class** in the **Content** folder and expand the **All Classes** section at the bottom. 
    * Search for **Game Mode Base**, name it **MRGameMode** and double-click to open. 

![MRGameMode in the Content Browser](images/unreal-uxt/3-gamemode.PNG)

2.	Go to the **Classes** section in the **Details** panel and change the **Default Pawn Class** to **MRPawn**. 
    * Hit **Compile**, then **Save** and return to the Main window. 

![Set the Default Pawn Class](images/unreal-uxt/3-setpawn.PNG)

3.	Select **Edit > Projects Settings** and click **Maps & Modes** in the left-hand list. 
    * Expand **Default Modes** and change **Default Game Mode** to **MRGameMode**. 
    * Expand **Default Maps** and change both **EditorStartupMap** and **GameDefaultMap** to **Main**. This way when you close and reopen the editor, or play the game, the Main map will be selected by default.

![Project Settings - Maps & Modes](images/unreal-uxt/3-mapsandmodes.PNG)

With the project fully setup for mixed reality, you're ready to move on to the next tutorial and start adding user input to the scene. 

[Next Section: 4. Making your scene interactive](unreal-uxt-ch4.md)