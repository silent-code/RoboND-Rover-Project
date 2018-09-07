## Project: Search and Sample Return

 

[//]: # (Image References)

[image1]: ./test_dataset/IMG/robocam_2018_08_31_17_32_07_777.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg 


### Here I briefly review the stages and steps of the project.  

**The stages of this project were as follows:**  

**Stage 1 of the RoboND Rover Project: Training / Calibration**  

Steps taken include:
* Downloaded the simulator and took data in "Training Mode"
* Tested out the functions in the Jupyter Notebook provided
* Added functions to detect obstacles and samples of interest (gold-colored rocks)
* Filled in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` test created in this step demonstrated that my mapping pipeline worked.
* Finally I used the `moviepy' module to process the images in my saved test dataset with the `process_image()` function.  The final video, test_mapping.mp4', can be found in the output folder of this repository.

**Stage 2 of the RoboND Rover Project: Autonomous Navigation / Mapping**

Steps taken include:
* Filled in the `perception_step()` function located inside the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()`, the rover state class instantiation. 
* Filled in the `decision_step()` function located in the `decision.py` script with conditional statements that utilize the outputs of the `perception_step()` to decide how to issue throttle, brake and steering commands. 
* Iterated on the perception and decision function steps until the rover satisfied the autonomous navigation and mapping objectives of 40% environment mapping at 60% ground truth fidelity. 

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Next I consider the rubric points individually and describe how I addressed each point in my implementation.

### Notebook Analysis
#### 1. I executed the functions provided in the notebook on test images: first with the test data provided, and then on data that I with recorded in the simulator training mode. Next I added/modified functions to allow for color selection of obstacles and rock samples. The next image shows the data I used to calibrate color selection functions for obstacles, navigable terrain and rock sample features. The image below shows a calibration image with each of the three types of features. The image includes the rover tracks which are calibrated to be included as a navigable terrain feature.

![alt text][image1]



#### 2. In step 2 of the Notebook Analysis, I populated the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Next, I ran `process_image()` on the test data I collected using the `moviepy` functions provided to create video output of the result. These steps were helpful in developing and debugging the auxiliary functions for the perception step.  


### Autonomous Navigation and Mapping

#### 1. Code modifications: As part of the project completion, I  `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scaffold scripts provided in the project. and an explanation is provided in the writeup of how and why these functions were modified as they were.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your graphics settings (2880x1800 native resolution at 220 ppi)  and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  

Ideas for improvement: better navigable terrain indicator, obstacle avoidance, use map for expedited coverage OA and rock dropoff, 



