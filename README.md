
# Technical Requirements Document
# WallCraft using Meta Quest SDK

## Introduction

This document outlines the technical approach, algorithm, and implementation plan for the development of WallCraft, an app designed to detect walls in a room and apply selected wall panel designs using the Meta Quest SDK. The goal is to offer users a seamless experience in customizing their wall panels while ensuring they do not obstruct any objects in the room.

## Problem Description
Users desire an AR application that accurately detects vertical walls in a room and allows them to customize wall panel designs without obstructing other objects.

Tech Stack:
 - C#
 - Oculus SDK
 - OpenXR
 - Unity
 - JavaScript (WebXR)

  Terminology
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

## Solution Approach

1. Wall Detection
   - Create a 3D core project in Unity and import necessary AR and XR packages (e.g, AR foundation, ARcore, XR Interaction Toolkit, XR Plugin Management).
   - Add 'AR session origin' and 'AR session' from the hierarchy, then attach the 'AR Plane Manager' component to 'AR session origin'.
   - Configure an 'AR default plane' prefab in AR Plane Manager's prefab, this prefab will detect the planes in the room, to get only vertical planes change the setting in detection mode.
   - Update build and player settings as per user requirements e.g., target platform Meta Quest or Android and player setting such as resolution, input settings, API level, etc.
   - This process will detect vertical walls and create a mesh renderer on them.
  
2. Carousel UI for Wall Panels
   - Add a 'canvas' from UI and adjust its resolution according to the requirements.
   - Attach a 'scrollview' component inside canvas and set functions for the carousel like horizontal or vertical scrolling, movement type.
   - Insert multiple panels within the scroll view to store the wall panel designs.
   - Customize UI elements such as buttons and dot animation, to facilitate navigation through the wall panel designs, allowing users to select their desired options efficiently.
   - Add an 'AR default plane' and write a C# script to handle the transition from 2D to AR.
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
    - Create an empty object i.e., 'ShapeCreator', add C# script with the logic of updating the vertical wall planes according to the selected wall panel, add the created materials under the shapecreator script which enables the update.
    - In the button object of the scrollview, update the on Click() function according to the shapecreator numbering to set the desired wall panel design in the panels of scrollview.

4. Object filteration algorithm
  - An object recognition library will be required, research available pre-trained object recognition models like YOLO, SSD, or MobileNet, choose a model based on factors such as accuracy, efficiency, and compatibility with Unity.
  - Import necessary components like Unity ML-Agents toolkit, download the pre-trained model files, including model architecture and weights and if required convert the model files to TensorFlow for format compatibilty with unity.
  - Write C# script to handle integration of the object recognition model, including functions for loading the model, preprocessing input images, running inference, and post-processing outputs.
  - Determine input source and output visualization, whether input images will be captured from a camera feed or loaded as static images, and format for visualizing object detection outputs focusing on walls for e.g., drawing bounding boxes around detected objects to distinguish them from walls.

Pseudo code :  

    private ObjectRecognitionModel recognitionModel;
    public Material wallMaterial;

    void Start() {
        recognitionModel = new ObjectRecognitionModel();
    }

    void Update() {
        Texture2D inputImage = Camera.main.RenderToTexture();
        DetectedObject[] detectedObjects = recognitionModel.DetectObjects(inputImage);

        foreach (DetectedObject obj in detectedObjects) {
            if (IsWall(obj)) {
                RemoveMeshFromWall(obj);
                ApplyWallPanel(obj);
            }
        }
    }

    bool IsWall(DetectedObject obj) {
        return obj.Classification == ObjectClass.Wall;
    }

    void RemoveMeshFromWall(DetectedObject wall) {
        Destroy(wall.gameObject.GetComponent<MeshRenderer>());
        Destroy(wall.gameObject.GetComponent<MeshCollider>());
    }

    void ApplyWallPanel(DetectedObject wall) {
        wall.gameObject.GetComponent<Renderer>().material = wallMaterial;
    }

A reference flowchart image is atttached in the repository above.

   # Conclusion
   The Technical Requirements Document (TRD) provides a detailed blueprint for the development of WallCraft, an AR application utilizing technologies such as C#, Oculus SDK, OpenXR, Unity, and JavaScript (WebXR) to empower users in customizing wall panel designs seamlessly. By addressing crucial technical requirements like accurate wall detection, carousel UI implementation for panel selection, and intelligent overlay of panels onto detected vertical planes, the TRD ensures a structured approach towards achieving the app's objectives. Furthermore, considerations for integrating object recognition algorithms ensure that wall panels don't obstruct other objects in the room. This TRD serves as a solid foundation, guiding the development process towards crafting a user-friendly and immersive AR solution that holds great potential for enhancing interior customization experiences.

 
