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
[image4]: ./misc/capturea.jpg
[image5]: ./misc/captureb.jpg
[image6]: ./misc/capturec.jpg
[image7]: ./misc/final.jpg

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

1. Populate the process_image() function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap. Run process_image() on your test data using the moviepy functions provided to create video output of your result.

The process_image() function had a basic structure with 6 required coding steps to accomplish the process of reading the incoming image. The image would then be identified in terms of navigable terrain, obstacle, or a rock sample. The processed image coming in (figure A top left below) would be change to RGB values through a perceptive transformation (warped image). The warped image would be viewed as filters in terms of transformation. Then that process would be giving us colors to determine what was navigable, obstacles or samples to pick up (top right figure A below). While we are processing the incoming images, part of the data will be used to plot what the rover sees on the left side top in basis RGB colors and on the bottom left, will plot what has been mapped and the location of the rock samples found.  The rover centric data containing the coordinates be covered to world coordinates (See figure B below bottom left, circled in blue, with differing light colors and the brown area as a rock sample). during the conversion.  By using the simulator, you can record in training mode and use the notebook to analyze each image recorded and create a short video.

Steps required list: 
1.	Define source and destination points for perspective transform
2.	Apply perspective transform
3.	Apply color threshold to identify navigable terrain/obstacles/rock samples
4.	Convert thresholded image pixel values to rover-centric coords
5.	Convert rover-centric pixel values to world coords
6.	Update worldmap (to be displayed on right side of screen)

##                                        Figure A

![alt text][image4] 

##                                        Figure B

![alt text][image5]

Autonomous Navigation and Mapping
1. Fill in the perception_step() (at the bottom of the perception.py script) and decision_step() (in decision.py) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

The perception.py file has a perception_step() function that following the same logic as we saw in the Python Jupyter Notebook simulated. Minor adaption was necessary to make the code run in the new simulation environment from the notebook. Instead of reading as data (class) from the (data= Databucket()) in the notebook, the function interacts with the Rover (class) (Rover = RoverState()). In so doing and in trying to increase the fidelity, a) added a margin of 2 in the roll and pitch (angles below 2 or over 358). If the rover is rolling along at a good pace the data will not be mapped stopping the latency in screen updates and this is allowed the rover to maintain a fidelity of almost 62%. b) added 2 fucntions of rock_sample_thresh and obstacles_thresh for better detection with a greater starting fidelity resulted in the 90 percentile. This basic test or adaptation is translated in the scope and direction of the rover as seen as a decision in which direction to go (decision.py). 

The decision.py file with scripting functions is to decide what the rover can do at this instant. That decision flows for a decision tree similar to the if, then statements in other languages, but as if’s and Else if’s.  The decision by the code will allow the rover to move forward if no obstacles exist, stop, reverse or change directions.  Each decision was based-on velocity (vel) and has the rover change positions. If the rover was stopped then a process started that allowed the rove to try and free itself for the obstacle or wall it bumped into. The decision tree allowed the Rover to map over 80% with high fidelity.

2. Launching in autonomous mode your rover can navigate and map autonomously.

Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines! Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by drive_rover.py) in your writeup when you submit the project so your reviewer can reproduce your results.

The project was ran with variuos settings for both resoluiton and screen graphics rate - as seen in Figure C. The resolution for my simulated environment preformed best at 640x480, with fastest graphic quality. I increased the memory (Ram) of my machine to 8GB to stop so the issue with the freezes during the simulation runs.  Most of the decision process by decision.py as explained above was used in the process by the rover to run autonomously in the section above. Items that worked well were finally getting the right graphics output set (lots of trial and errors) along with cleaning up the code. The program did a decent job of maintain fidelity of over 80% and maps over 80% of the map given enough time. It's also able to pick most, if not all, of the rocks. The FPS is around 16.

##                  Figure C
![alt text][image6]
##                  Figure D
![alt text][image7]
