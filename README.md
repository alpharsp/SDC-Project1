[Image1]:./supportImages/original.png "Original"
[Image2]:./supportImages/YW.png "First Step"
[Image3]:./supportImages/Edges.png "Edges"
[Image4]:./supportImages/Mask.png "Mask"
[Image5]:./supportImages/MaskedEdges.png "Masked Edges"
[Image6]:./supportImages/AllLines.png "All the Lines"
[Image7]:./supportImages/Final.png "Final Image"
##**Finding Lane Lines on the Road**
---
###This project consists on Processing Images taken on the road with a camera located in front of the car, as it would be located in a self driving car.
###To have access to the Python Code, please refer to final_Project_1.ipynb
---
##Reflection
###1) PipeLine Description
![Image1]

The typical pipeline would start on converting the image to grayscale for the edge detection processing, however to be able to accurately identify these lines on more complex sufaces, my first step was to identify tones in a Range of Yellow and White, removing every other component from the image. As you can see, all the components that we care about are shown in white and everything else is in black.

![Image2]

Once we have this Image we need to detect the edges which are defined as rapid changes in the intensity of the grayscale/Black and White Image, the Canny Algorithm provided on the OpenCV library can be use for this type of filtering.

![Image3]

