
# WallCraft

## Introduction

This document outlines the technical approach, algorithm, and implementation plan for the development of WallCraft, an app designed to detect walls in a room and apply selected wall panel designs using the Meta Quest SDK. The goal is to offer users a seamless experience in customizing their wall panels while ensuring they do not obstruct any objects in the room.

Tech Stack:

 - C#
 - Oculus SDK
 - OpenXR
 - Unity
 - JavaScript (WebXR)

## Approach

1. Wall Detection
   - Create a 3D core project in Unity and import necessary AR and XR packages.
   - Add 'AR session origin' and 'AR session' from the hierarchy, then attach the 'AR Plane Manager' component to 'AR session origin'.
   - Configure an 'AR default plane' prefab to detect only vertical planes from detection mode.
   - Update build and player settings as per user requirements.
   - This process will detect vertical walls and create a mesh renderer on them.
  
2. Carousel UI for Wall Panels
   - Add a 'canvas' from UI and set its resolution.
   - Attach a 'scrollview' component and set functions like horizontal or vertical scrolling, movement type.
   - Add multiple panels inside scrollview, here the wall panel designs will be stored.
   - Customize UI elements such as buttons and dot animations.
   - Add an 'AR default plane' and write a script to handle the transition from 2D to AR.
   - Upon interaction with the 2D scroll view (e.g., clicking on an item), deactivate the Canvas containing the 2D scroll view UI elements, and activate the AR session and AR content    
     GameObject(s) to show the AR environment.

Pseudo code for the same:

    // Deactivate 2D scroll view canvas
    scrollViewCanvas.SetActive(false);
    
    // Activate AR session
    arSession.enabled = true;
    
    // Activate AR content
    arContent.SetActive(true);

 3. Overlay selected wall panels onto the detected vertical wall planes.
    - Create materials for wall panels and customize them according to the content (e.g., color, texture).
    - Create an empty object i.e., 'ShapeCreator', add C# script with the logic of updating the vertical wall planes according to the selected wall panel, add the created materials under the        shapecreator script which enables the update.
    - In the button object of the scrollview, update the on Click() function according to the shapecreator to set the desired wall panel design.
