
# WallCraft

## Introduction

This document outlines the technical approach, algorithm, and implementation plan for the development of WallCraft, an app designed to detect walls in a room and apply selected wall panel designs using the Meta Quest SDK. The goal is to offer users a seamless experience in customizing their wall panels while ensuring they do not obstruct any objects in the room.

## Summary

Problem Description: Users desire an AR application that accurately detects vertical walls in a room and allows them to customize wall panel designs without obstructing other objects.

Tech Stack:
 - C#
 - Oculus SDK
 - OpenXR
 - Unity
 - JavaScript (WebXR)

Suggested Solution: The proposed solution involves creating a 3D core project in Unity, configuring an AR Plane Manager to detect only vertical planes, and implementing a carousel UI for wall panel selection. The solution aims to seamlessly transition between 2D UI and AR content and overlay selected wall panels onto detected vertical wall planes. /////

- Glossary or Terminology
  - AR: Augmented Reality
  - SDK: Software Development Kit
  - XR: Extended Reality
  - UI: User Interface

- Product Requirements:
  - Users can seamlessly customize wall panel designs.
  - Wall detection accurately identifies vertical planes.
  - AR content overlays selected wall panels without obstructing other objects.

- Technical Requirements:
  - Integration of AR and XR packages.
  - Implementation of a carousel UI for wall panel selection.
  - Development of logic for updating wall panels on detected vertical planes.

- Non-Goals or Out of Scope
  - Advanced interior design features beyond wall customization.
  - Performance optimization for low-end devices.

- Future Goals
  - Implementation of additional interior design features.
  - Optimization for various device configurations.

- Assumptions
  - Availability of necessary AR and XR packages.
  - Access to machine learning models for object recognition.

## Approach

1. Wall Detection
   - Create a 3D core project in Unity and import necessary AR and XR packages.
   - Add 'AR session origin' and 'AR session' from the hierarchy, then attach the 'AR Plane Manager' component to 'AR session origin'.
   - Configure an 'AR default plane' prefab in AR Plane Manager's prefab to detect only vertical planes from detection mode.
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
