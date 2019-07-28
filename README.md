# PCLManipulator
An open design for a 2DoF manipulator for 3D point cloud scanning

This design was created for my PhD research in 3D Point Cloud Analysis. Fusion 360 was used to create a parameterized model capable of many changes. This manipulator can be fully constructed of 3D printed pieces (any plastic will be fine), lasercut wood (3mm baltic birch, in my case), a carbon fiber tube (found at a local hobby shop), 2 Dynamixel XL430 motors, a Realsense D4xx camera, and simple mechanical screws.

A camera in space, for the purposes of observing an object, would need 6DoF (3 for pose, 3 for orientation). For this project, 6DoF would be an unnecesary amount of time, labor, and data. By making the rule that the camera will always face a central origin of the object, we immediately eliminate 3Dof. We can eliminate another by converting to spherical coordinates and constraining the camera to always be a specific distance away from the object. In this final 2DoF representation, we can call the two axes Yaw and Pitch.

## Software

The software is made for a Linux system with the point cloud library (PCL), Realsense SDK 2.0, and Dynamixel SDK installed. Before compilation, you will need to adjust the CMakeLists.txt file to point to your local libraries, as well as adjust the file storage location in main.cpp. This was compiled in Ubuntu 16.04 but I see no reason that it won't work in other Linux distributions as long as the correct libraries are installed and located by CMake.

The software moves the object to a position, obtains the Realsense point cloud, filters the cloud to remove all points outside of a cartesian box, transforms the point cloud to the central origin, and saves the point cloud to external storage. As the PID controllers in the motors cannot make short jumps reliably, the current code moves the two axes randomly in the configuration space, rather than iterating progressively through each possible position. This allows sufficient movement to go to a position within a reasonable margin of error. Despite whatever pose error may be present, the software reads and saves the data as the current position (as opposed to the goal position) which removes the pose error from the collected data. Data points will not be overwritten. Considering the action space is 4096*2048 possible locations, it will take approximately 2 weeks to obtain 90% of the possible positions.

In the future I hope to release code that will fully rotate the object, obtain a streamed point cloud, and use PCL registration to create a fully scanned 3D model of the centralized object. As this does not currently relate to my research projects, it is not at the top of my priority list, but if anybody would like to take on the project let me know and I could provide assistance.

## Hardware

Currently, I will only be releasing the STL files and DXF files for construction, but after I clean up and merge the Fusion 360 projects, I will post those files as well.

For 3D Printing, a Prusa i3 mk3s was used for the pieces, with some pieces being printed in PETG and others in PLA. As relatively little stress will be placed on the pieces, the actual plastic doesn't matter. The only piece that should be printed with high detail is the carbon fiber mount. Ensure the carbon fiber rod does not move in the mount and the mount is secure on the motor with no wiggle room. As the standoffs needed to be specific heights to allow the camera to be facing directly at the origin, these were 3D printed in high quality. If you can find another way to securely ensure the height of each layer, feel free to go that route. This just worked well for us. We even 3D printed the nuts and bolts, but I do admit this is unnecessary considering we could have just made a trip to the hardware store.

For laser cutting, a Full Spectrum Laser 20x12 Hobby lasercutter was used with RetinaEngrave and CorelDraw. The pieces were all constructed to fit within the bounds of the lasercutter. 3mm baltic birch was used, but if the parameter in Fusion360 for material thickness is changed, there is no reason that a different size of material wouldn't work. For the manipulator itself, simple wood glue and clamps were used for adhesion.

Let me know if you have any questions. I don't know how many adjustments or changes I'd be willing my make to the model, as it suits my needs in the current form, but if you have any feel free to create a pull request and we can change it!
