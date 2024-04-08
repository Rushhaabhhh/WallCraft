# WallCraft

1. Introduction

The purpose of this document is to outline the technical approach, algorithm, and implementation plan for developing an app that detects walls in a room and applies selected wall panel designs to these walls using the Meta Quest SDK. The app aims to provide users with a seamless experience in selecting and applying wall panels, ensuring that they only cover the visible wall planes and not obstruct any objects in the room.

2. Approach
   
   2.1 : Wall Detection
         -> In unity, create 3D core project and import required AR and XR packages.
         -> Add 'AR session origin' and 'AR session' from hierarchy and under AR session origin, add 'AR Plane Manager' component.
         -> Create an 'AR default plane' and place it in plane prefab of AR origin, change the detection mode to vertical which limits to detect                only the vertical planes, and not floor and ceiling.
         -> Update the build and player setting according to user requirements.
   This steps will detect all the vertical walls and create a mess renderer on them.

   2.2 : Carousel UI for Wall Panels
   			-> Add 'canvas' from UI and set its resolution, add 'scrollview' component and set the functions in 					 it, like movement type, horizontal or vertical.
   			-> Inside scrollview, add multiple panels to contain the scrollable content, 
