# DeepLabCut_Notes

DeepLabCut
DeepLabCut has been used to extract user-defined, key body part locations from animals 

Why DeepLabCut

* Due to transfer learning it requires little training data for multiple, challenging behaviors
* The feature detectors are robust to video compression
* It allows 3D pose estimation with a single network and camera
* It allows 3D pose estimation with a single network trained on data from multiple cameras together with standard triangulation methods

DeepLabCut is embedding in a larger open-source eco-system, providing behavioral tracking for neuroscience, ecology, medical, and technical applications.


￼

#Notes: 

- Human pose estimation has been utilized in a wide range of applications, including human-computer interaction, action recognition, motion analysis, augmented reality, sports and fitness, and robotics.

- Transfer learning, the ability to take a network that was trained on a task with a large supervised dataset and utilize it for another task with a small supervised dataset.

- Gait analysis is an assessment of the way the body moves, usually by walking or running, from one place to another. The purpose of gait analysis is to detect any abnormalities in locomotion.



Abstract:
Source: https://www.nature.com/articles/s41596-019-0176-0

Extracting the poses of animals without using markers is often essential to measuring behavioral effects in biomechanics, genetics, ethology, and neuroscience. However, extracting detailed poses without markers in dynamically changing backgrounds has been challenging. 

DeepLabCut that builds on a state-of-the-art human pose-estimation algorithm to allow a user to train a deep neural network. Developed as a Python package, that includes new features such as graphical user interfaces (GUIs), performance improvements, and active- learning-based network refinement. A tailored, reusable analysis pipeline with a graphical processing unit (GPU) in 1–12 h (depending on frame size). 

Provided Docker environments and Jupyter Notebooks that can be run on Google collaboratory.

The toolbox is aimed to solve the problem of detecting body parts in dynamic visual environments in which varying background, reflective walls, or motion blur hinder the performance of common techniques such as thresholding or regression based on visual features.

Specifically, DeepLabCut is best suited to behaviors that can be consistently captured by one or multiple cameras with minimal occlusions. DeepLabCut performs frame-by-frame prediction and thereby can also be used for analysis of behaviors with intermittent occlusions. 

The DeepLabCut Python toolbox is versatile, easy to use, and does not require extensive programming skills. With only a small set of training images, a user can train a network to within human-level labeling accuracy, thus expanding its application to not only behavior analysis in the laboratory, but potentially also to sports, gait analysis, medicine, and rehabilitation studies.


Overview of using DeepLabCut :

1. The user starts by creating a new project based on a project name and username 
2. As well as some (initial) videos, which are required to create the training dataset, additional videos can also be added
3. Next, DeepLabCut extracts frames that reflect the diversity of the behavior with respect to, e.g., postures and animal identities 
4. Then the user can label the points of interest in the extracted frames 
5. These annotated frames can be visually checked for accuracy and corrected, if necessary 
6. Eventually, a training dataset is created by merging all the extracted labeled frames and splitting them into subsets of test and train frames 
7. Then a pre-trained network (ResNet) is refined end-to-end to adapt its weights in order to predict the desired features (i.e., labels supplied by the user )
8. The performance of the trained network can then be evaluated on the training and test frames 
9. The trained network can be used to analyze videos, yielding extracted pose files 
10. If the trained network does not generalize well to unseen data in the evaluation and analysis step (Stages 8 and 9), then additional frames with poor results can be extracted (optional ), and the predicted labels can be manually corrected. 

This refinement step, if needed, creates an additional set of annotated images that can then be merged with the original training dataset. This larger training set can then be used to re-train the feature detectors for better results.

This active-learning loop can be done iteratively to robustly and accurately analyze videos with potentially large variability, i.e., experiments that include many individuals and run over long time periods. Furthermore, the user can add additional body parts/labels at later stages during a project, as well as correct user-defined labels. 


￼


Comparison with other models:

The removal of the pairwise refinement, as well as integer linear programming on top of the part detectors, substantially increased the inference speed.

* If a user aims to track (adult) human poses, many other excellent options exist, including DeeperCut, ArtTrack, DeepPose, OpenPose, and OpenPose-Plus.
* Another neural network–based package for animals, called LEAP, was described36. LEAP excels at rapidly training a network on a specific behavior, but because it is a shallow network without any pre-training, it is probably not as robust to changes in the environment and requires more training data to match the performance of DeepLabCut, i.e., human-level accuracy. These advantages seem to be due to transfer learning12, whereas LEAP is trained from scratch. 

* DeepLabCut was shown to need <150 frames of human-labeled data for even challenging 3D hand movements of a mouse.
* For similarly sized videos, DeepLabCut runs at 90 FPS with a batch size of 1 and ~350 FPS with a batch size of 32, and accelerates substantially (up to 1,000 FPS) for larger batch sizes27. 


Advantages:

DeepLabCut also allows for 3D pose estimation via multi-camera use. A user can train a network for each camera view, or combine multiple camera views and train one network that generalizes across all views (see Fig. 7 below and ref. 27) and then use standard camera calibration techniques37 to resolve 3D locations. DeepLabCut does not require images to have a fixed frame size, as the feature detectors are not sensitive (within bounds) to the size because of automatic rescaling during train- ing12. There are also no specific camera requirements. Color and grayscale images captured from scientific cameras or consumer-grade cameras such as a GoPro can be used (and the package supports multiple video types, such as .mp4 and .avi). Also, we recently showed that DeepLabCut is robust to video compression, potentially saving users >500-fold on data storage space27, making multi-camera use potentially more feasible. 

The toolbox provides different frame-extraction methods to accommodate the analysis of videos from varying recording sessions. The toolbox is modular, and by changing desired parameters at execution, the user can, for instance, utilize different frame-extraction methods or identify frames that require further inspection. Reliably defining the user-defined labels across different frames is of paramount importance for supervised learning approaches such as DeepLabCut. 

Limitation:

* One main limitation is that the toolbox requires modern computational hardware to produce fast and efficient results (namely, GPUs5). 
* Another consideration is that deep convolutional networks scale with the size of pixels; therefore, larger images will be processed more slowly. Thus, for applications that would benefit from rapid analysis of the input, images should be downsampled to achieve high rates 
* Another limitation is that DeepLabCut, because it is designed to be of general purpose, does not rely on heuristics such as a body model, and therefore occluded points cannot be tracked. However, DeepLabCut outputs a confidence score, which reports if a body part is actually visible. 









