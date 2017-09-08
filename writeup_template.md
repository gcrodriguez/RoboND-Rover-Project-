# Project: Search and Sample Return
### Objectives: In this work the goal is to make a rover move autonomously in order to map the environment and search dor yellow rocks. Through the images capture by the rover the navigable path, obstacles and collectible rocks are identified and updated to the map according to the rover displacemnt.

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

![image1](https://github.com/udacity/RoboND-Rover-Project/blob/master/misc/rover_image.jpg)

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.

The perception starts when the rover capture one image to its map. With this image we shall change its perspective to a top view in order to update the world map as the rover moves. After defining grid lines and its dimensions, the cv2 functions are applied in a function to get a perspective view and a binary image of the mask (which will diferentiate the obstacles and navigable terrain).

![image2](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/Images_for_writeup/grid.png)

![image3](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/Images_for_writeup/perspective_navigable.png)

Then the next step is to identify the navigable terrain, obstacles and rocks by color thresholding of the image pixels. Setting a limit of rgb = (160,160,160), the function color_thresh return a binary image which the pixels values above the limit (returning true of the above_thresh) are set to 1, appearing in white. The false values are set to 0 and appears in black. The image below illustrates the result.

![image4](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/Images_for_writeup/color_thresh.png)

The same strategy is used to identify rocks. As they have yellow color, the limit used was rgb = (110, 110, 50). But this time the image pixels values of the red and green layers shall be above limit and the correspondents to the blue layer below the limit. The image bellow shows the results.

![image5](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/Images_for_writeup/rock_indetify.png)

At this part, it is possible to update the map in different colors for navigable terrain, obstacles and rocks. But in order to update in almost real time and with the correct orientation, the image shall be repositioned to roover coordinate system, identify this system in worls map and also indicated the navigable direction. This is achived by applying rotations and translations of the pixels. The results obtained can be observed below.

![image6](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/Images_for_writeup/direction.png)

These whole procedure is done for each image captured by the rover while moving. Then the preliminary video recorded showing the rover in action (manually) is shown below.

![Video1](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/test_mapping.mp4)


The next part of the work is to apply these steps defined in process_image in the perception_step. After that, the decision_step is changed to make the rover autonomous. 

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

In the perception step (perception.py) the same procedure stablished in process_image is implemented. The only additional step made was the condition to add the rocks position in the world map (after identifying its pixels by color thresh). 

At the moment, the functions introduced to make the rover go to the rocks and pick them were not working. So they were removed from the percepetion and decision steps keeping the rover only moving and indetifying navigable paths, obstacles and rocks.

I pretend to return in the future at this part and make the rover pick the rocks and leave them at the initial point, as suggested in the challenge (and also finish the other challenges).

#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

The best result obtained for rover simulation identified three rocks and mapped 76.6% of the map with a fidelity of 62.7%. Then as happenned in all other simulations the program 'crashed', making the rover to gool along a circular parth or turning continuously in its axis.


![image7](https://github.com/gcrodriguez/RoboND-Rover-Project-/blob/master/autonomous.png)




