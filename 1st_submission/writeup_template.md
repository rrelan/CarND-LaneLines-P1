#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.



In order to build the pipeline I first read all the images in a loop by using imread function (which reads
images in RGB format) . After loading the images , next step I converted all the images into gray scale
by using helper function - "gray" . On the gray images then I applied gaussian blur function (helper function)
which was also part of the lessons followed by canny edge detection . For canny edge detection I used low_threshold of
150 and high threshold of 200 (I came to this value by manually changing values to get desired output , earlier I
had kept minimum threshold as 80 during which lines next to grass where road
ends were also getting detected).

Next step was to find region of intrest which was basically the lower part of the image where the lane lines are.
I created a variable boxes which was giving the vertices by truncating the image (for this I used image.shape)
and then I used HELPER function REGION_OF_INTREST where I passed the image (output from canny edge detection)
and second input being the box variable.


After getting region of intrest , I do a hough transformation where I input the partial image (image having area of intrest).
After doing hough transfgormation, I call draw_lines function .

How does draw_line function works  ?
In draw_line function , we take x1,y1 and x2,y2 coordinates from a line (this is taken using for loop).
Then we call slope function and find the slope of the line. Based on negative and positive slope value we identify
we identify left and right lanes. 

Then we find the left and right slopes , by taking average of coordinates and using get_slope function .
Once we have the coordinates  , I use cv2.line function to draw the lines. I also use hard coded top and bottom variables
which we used for finding the region of intrest.  Then we use weighted image HELPER function to add the two images which
produces our intial image with lane lines superimposed on top of it.
 


###2. Identify potential shortcomings with your current pipeline


Potential shortcoming with my algorithm is that it might not work 
in detecting lane lines when there are shadows or due to bad weather
or snow or less light this algo would not be able to detect the lane
lines. Also , we are detecting straight lines , when there are
curvatures not sure if this would work perfectly (I need to try that
though) . 


###3. Suggest possible improvements to your pipeline


A possible improvement would be to test my lane lines in different
weather condition . Also , I would like to add some kind of machine
learning / dep learning (assuming I have good amount of image data)
so that I could detect the lane lines when weather is not good and 
images are unclear. 


