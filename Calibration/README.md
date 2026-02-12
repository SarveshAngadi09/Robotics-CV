**Instrinsic Camera Calibration Notes**

Disclaimer: I have limited knowledge and trying to explain to the best of my capability, if there are any errors, or mistakes, please do let me know. Thank you!

Why do we need Camera Calibration?

Before this we need to understand what cameras are used for. 

They are not used just to acquire images, a lot of industrial use includes finding depth of the scene or object using cameras (just like our eyes give information about depth). I wouldn't worry about calibration if I used my camera just for acquiring pictures. 

What involves in calibration?

Calibration is mostly knowing about the system, and then tweaking it based on our requirements. Ex. Calibrating your eyes when it gets dark - pupils enlarge. 
(That is a very simple example - Let us get on to concrete examples soon).

In camera's, there are two types of calibration - intrinsic and extrinsic. As the names, one is internal aspects and external aspects of the camera. 

In this document we will explore only about the intrinsic calibration. (Also not adding calibration of distortion yet) 

Intrinsic calibration involves finding the focal length of the camera, principal point and distiortion parameters. 

What is focal length? https://en.wikipedia.org/wiki/Focal_length

What is principal point of camera? 

Principal point is the point on the camera sensor that is assumed to be at the center. It could be anything since it is defined with respect to optical center reference frame.

Optical center - this is the center of the lens in the camera.
Optical axis - A perpendicular to the face of the lens. 
These two form the optical camera frame.

![principal point](./images/1mUcU.png)

In the above image - Xc, Yc, Zc are the axis of optical camera frame.

Why do we need to find the focal length of the camera?

Focal length in simle words is the distance between the camera optical frame center to the sensor principal point. 

If we change the distance between the two points mentioned above, then we see that the point P(X, Y, Z) in real world is projected at different pixel positions of the camera sensor. (Simply slide the camera sensor back and forth and you see that the point (u,v) (in image) changes its position.)

So knowing focal length lets us know this projection of the ray. 

**Q** But wouldn't the focal length change as we move the lens - which happens in cameras or in modern cameras with liquid lens - does focal length change?

Yes, the focal lenght changes. But we **assume** that the change in focal length is very very negligible compared to the object distance. (1/f = 1/di + 1/do) f - focal length of the lens. di - distance between lens and sensor. do -  distance of object from the lens.

Okay so we are done with focal length. Let us talk about principal point. 

Why can't the principal point be the center of the sensor?

We are talking about principal time wrt the optical frame. If we just take the center pixels - how far are they from the optical frame coordinate? 
And **one important thing about image** - if we assume image to be a 2-D plane then the the **origin is not the center of the image**. Origin is the first top left pixel. See in the image, the u,v starts at the top left. 

Center along "u" will usually be total_width/2. (convert number of pixels in width to actualy length in meters or so, the size of each pixel is given by the manufacturers.)
center along "v" will usually be total_height/2.


**These are in general the principal point (cx, cy) = (width/2, height/2)
And z = f**


How do we find focal length and principal point? 