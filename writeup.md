## Project: Search and Sample Return

 

[//]: # (Image References)

[image1]: ./test_dataset/IMG/robocam_2018_08_31_17_32_07_777.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg 


### Here I briefly review the stages and steps of the project.  

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
#### 1. In step 1 of the Notebook Analysis I executed the functions provided in the notebook on test images: first with the test data provided, and then on data that I with recorded in the simulator training mode. Next I added/modified functions to allow for color selection of obstacles and rock samples. The next image shows the data I used to calibrate color selection functions for obstacles, navigable terrain and rock sample features. The image below shows a calibration image with each of the three types of features. The image includes the rover tracks which are calibrated to be included as a navigable terrain feature.

![alt text][image1]



#### 2. In step 2 of the Notebook Analysis I populated the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Next, I ran `process_image()` on the test data I collected using the `moviepy` functions provided to create video output of the result. These steps were helpful in developing and debugging the auxiliary functions for the perception step.  


### Autonomous Navigation and Mapping

#### 1. Code modifications: As part of the project completion, I modified the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions provided in the autonomous mapping scaffold scripts. In the `perception_step()` I added a function to threshold on gold-colored rock samples and add these to the rover vision image and then added a similar image processing pipeline like that in the 2nd step of the Notebook Analysis above. This time however, I kept track of obstacles, navigable terrain and rocks at each step. One improvement that was required to obtain improved map fidelity was to only add  to the Rover.worldmap attribute if the vehicle's pitch and roll was less than +/- 1 degree with respect to horizontal. The `decision_step()` function worked as given and required no changes to meet the autonomous mode specifications of 40% terrain covered, 60% ground truth mapping fidelity and locating at least 2 rocks. However, to improve time efficiency, I included a behavior for the rover to get unstuck whenever it's throttle was positive and its measured ground speed was non-zero.


#### 2. Autonomous mode:  
The project goal was to map terrain while avoiding obstacles and locating rocks. The approach I used to accomplish the objective utilized the technique of modifying code and simulating the rover behavior. This iterative technique worked best for cases where the modified behavior was more likely to arise quickly, e.g., modifying obstacle avoidance behavior so that code change effects could be observed more immediately. However in cases such as the rover getting stuck, the simulation approach was less efficient since this behavior was rarely observed.

In the perception pipeline, the weakest assumption in a real world situation is the thresholding based on color differences. Some type of template matching for rock identification could be used in situations where color was not a reliable feature. Stereo vision could be used to extract left-right and height estimates of terrain to identify navigable paths when color thresholding fails for monochromatic terrain.

Ideas for improvement include developing more sophisticated navigable terrain, obstacle and rock detection algorithms as previously described. Also, instead of using the length of the navigable angles vector to estimate whether to continue or stop, it would be more accurate and efficient to path plan in the rover-centric image space, for example, moving in the direction of the longest ray trace in the rover-centric navigable terrain image. Using the world map to decide where to navigate would expedite coverage and improve obstacle avoidance and rock dropoff and eliminate the observed circling behavior at the map center.

**Note: My graphics settings were 2880x1800 native resolution at 220 ppi and my frames per second was 40.**

