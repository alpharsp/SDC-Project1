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

![Image4] 
![Image5]

With only the edges of the lane lines exposed, we can simplify these edges into multiple continuous lines that we can characterize using the Houghs Transform. Not everyline in the image is useful, we need to stablish a set of assumptions to discard the lines that don't met our criteria:

-There is a minimum length for the lines we can consider useful.

-The edges Image is made out of discrete dots in the cartesian space with sometimes gaps in between the points that consitute a straight line. we need to stablish an allowance for these gaps in the Houghs transform.

-The lines slope is a powerfull way to determine what lines belong to what side of the road and which lines need to be discarted.

![Image6]

Finally, we can trace single lines on each side of the road described as the weighted average of the Gradient and Bias of every single smaller line; where the weight factor is the length of the lines. Using these methods we allow the longer lines detected to have more influence than the small ones in the final product.

![Image7]

###2) Possible Shortcomings

This initial project is obviously based on very ideal conditions on a highway, the following conditions would become a threat at the time of setting the lane boundaries:

-Sharp turns

-Blury old lines

-Overlapping of oldlines and new lines

-Objects or paint in the road within our line color parameters

-Other Vehicle interfeering with the image capture

-Large gaps in between dotted lines

-Absence of lines in a highway


###3) Possible Improvements
-This algorithm is very static, it only uses the information from one line at a time, which is fine in the event that we have ideal consitions. However in the event of a shortcoming such as the ones mentioned above, it would be very benefitial to use control theory to set the angle and positions of the boundaries using the Proportional Integrative and Derivative properties of the detected input lines. In other words to consider the past position/orientation of the boundaries, the present input of the road image and to predict the future position/orientation.

