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

As we can see on the Image we didn't only detect the edges for the lines but we have the edges of many other objects in the surroundings, we need to filter our image through a Mask to remove all the items that we dont need from it. Due to the nature of the Image, the position and perspective, a trapezoidal mask was used for this purpose.

![Image4] ![Image5]

With only the edges of the lanelines expl weosed, we can simplify these edges into multiple continuous lines that we can characterize using the Houghs Transform. Not everyline in the image is useful would need to implement a set of assumptions to discard the lines that don't met our criteria:
-There is a minimum length for the lines we can consider useful.
-The edges Image is made out of discrete dots in the cartesian space with sometimes gaps in between the point that consitute an straight line. we need to an allowance for these gaps in the Houghs transform.
-The lines slope is a powerfull way to determine what lines belong to what side of the road and which lines need to be discarted.

![Image6]
