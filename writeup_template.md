## Project: Search and Sample Return
### Writeup Template: You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---


**The goals / steps of this project are the following:**  

**Training / Calibration**  

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook). 
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands. 
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.  

[//]: # (Image References)

[image1]: ./misc/rover_image.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg 

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.
Here is an example of how to include an image in your writeup.

![alt text][image1]

#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 
And another! 

![alt text][image2]
### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

In order to detect the obstacles, navigable areas, and the rocks, a function was created to recognize the difference in colors of the various objects in the world.  The first step was to ensure that the Import CV2 was added as a necessary package. We use the RGB color space to detect difference in colors. For obstacles, an inverse background was added from ground color threshold and seems to work very nicely. For the rock sample detection, a threshold was applied between the lower range of (100, 100, 20) and the upper range (255, 255, 30). 



#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  
The process_image() function had a basic structure with 6 required coding steps to accomplish the process of reading the incoming image. The image would then be identified in terms of navigable terrain, obstacle, or a rock sample. The processed image coming in (figure A top left below) would be change to RGB values through a perceptive transformation (warped image). The warped image would be viewed as filters in terms of transformation. Then that process would be giving us colors to determine what was navigable, obstacles or samples to pick up (top right figure A below). While we are processing the incoming images, part of the data will be used to plot what the rover sees on the left side top in basis RGB colors and on the bottom left, will plot what has been mapped and the location of the rock samples found.  The rover centric data containing the coordinates be covered to world coordinates (See figure B below bottom left, circled in blue, with differing light colors and the brown area as a rock sample). during the conversion.  By using the simulator, you can record in training mode and use the notebook to analyze each image recorded and create a short video.

Steps required list: 
1.	Define source and destination points for perspective transform
2.	Apply perspective transform
3.	Apply color threshold to identify navigable terrain/obstacles/rock samples
4.	Convert thresholded image pixel values to rover-centric coords
5.	Convert rover-centric pixel values to world coords
6.	Update worldmap (to be displayed on right side of screen)

Figure A

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  



![alt text][image3]


