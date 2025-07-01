# VisualChangeDetection
A graph-based AI method for context-aware visual change detection in software user interfaces

In this repository, you can find information, results, data, and source codes of the context-aware visual change detection method. The method and experiments are described and discussed in the paper titled "Artificial intelligence for context-aware visual change detection in software test automation".

<h2>The context-aware visual change detection method</h2>
<p>The following image illustrates the overal architecture of our visual change detection method:</p>
<br>
<img width="400" src="https://github.com/mmoradi-iut/VisualChangeDetection/blob/main/Figure-1.jpg">

Our visual change detection model consists of four main steps:
1) control detection
2) graph building
3) graph matching (or graph comparison)
4) change detection and visualization

The proposed visual change detection method operates through a four-stage pipeline. First, we apply a deep learning object detection model to identify UI controls in the input screenshots. Second, the detected controls are used to build graph representations of the UI layouts, capturing both spatial and contextual relationships between controls. Third, we match the graphs using a recursive similarity algorithm that compares nodes based on visual, textual, and neighborhood features. Finally, unmatched elements are interpreted as UI changes, which are visualized as heatmaps. This architecture enables the detection of both subtle and structural UI changes in a robust and layout-aware manner.

<h2>User interface control detection</h2>
<p>For detecting UI controls from software screenshots, we utilize an object detection machine learning model, i.e. YOLOv5, specifically trained and tested on a user interface control detection dataset containing 14,155 training and 2,000 test samples we created from software screenshots.</p>
<p>The following table presents the performence scores obtained by the YOLOv5 model on the UI control detection dataset.</p>
<br>
<img width="500" src="https://github.com/mmoradi-iut/VisualChangeDetection/blob/main/Table-1.jpg">

In order to have access to the dataset and get the permision, send an email to m.moradi-vastegani@tricentis.com.

<h2>Visual change detection datasets</h2>
<p>We created three different datasets in order to test the performance of our graph-based change detection method in various scenarios. Two datasets were created for change detection within desktop images in two different scenarios. One dataset were created to detect changes between desktop and mobile images.</p>

<p><b>- Desktop screenshots</b></p>
<p>We collected an initial set of images of 250 websites by taking screenshots of the desktop browser in the maximized mode with a screen size of 1,920 by 1,080 pixels. The first dataset was created by automatically applying eight different types of changes to the initial set of images. A maximum of four changes were applied to every image, with a minimum of one change. The number of changes and the type of changes were automatically selected in a random manner.</p>

<p>- Desktop screenshots–cut images</p>
<p>We created the second dataset to increase the difficulty of detecting changes and evaluate the accuracy of the visual change detection method in a more complicated scenario. We again generated changed images by applying the eight change methods we already introduced, but we also cut a region of every image and shifted the remaining part to the center. In this way, some user interface controls no longer appear in the changed image. Moreover, controls in the changed image do not appear in the same coordinates as in the target (or original) image.</p>
<p>This dataset simulates those scenarios where the active window of the application under test is resized and some controls may not appear anymore in the screenshot. Furthermore, the user interface controls do not appear in the same coordinates as the original screenshot taken before resizing the window. Detecting changes in this scenario can be very challenging, because pixel by pixel comparison easily fails in finding correspondence between controls in the target and changed images.</p>
<p>We created this dataset by applying a maximum of four changes (introduced in the previous subsection), with a minimum of one, to every original screenshot and then cutting a random area of the image in left, right, top, or bottom. The number of changes per image and the type of changes were selected in a random manner. The location of the area that must be cut was selected randomly from the set (left, right, top, bottom), and the number of pixels to cut was also selected randomly from the set (100, 200, 300, 400, 500). Seven changed versions were generated for every image in the dataset by applying different change methods. Therefore, the second dataset contains a total number of 1,750 images, every pair is represented by an original image and a corresponding changed image.</p>

<p>- Desktop–mobile screenshots</p>
<p>The goal of the third dataset is to evaluate the performance of the visual change detection method in detecting differences between screenshots of an application under test in different platforms. We created this dataset by taking screenshots of 180 pairs of different web applications, each pair consisting of one desktop and one mobile screenshot of the same application with the same Graphical User Interface (GUI). The size of images is 1,920 by 1,080 pixels in desktop and 576 by 832 pixels in mobile platform. We also generated ground-truth annotations for every pair of desktop and mobile screenshots by manually annotating user interface controls and correspondence between the controls in the images.</p>

In order to have access to the dataset and get the permision, send an email to m.moradi-vastegani@tricentis.com.

<h2>Hyperparameter tuning</h2>
<p>Our visual change detection method has four hyperparameters that control how the method creates a graph, identifies correspondence between UI controls within images, and detects changes. We designed and conducted a set of experiments to investigate the impact of these hyperparameters on the performance of change detection. We used 70 percent of each dataset for tuning the hyperparameters and the remaining 30 percent for testing the change detection method against the baseline change detectors.</p>
<p>Based on the tuning experiments across all three datasets, we selected the following final hyperparameter values for the comparative evaluations:
  
<p>•	Number of nearest neighbors 𝐾=8 for desktop screenshots, 𝐾=6 for cut images, and 𝐾=5 for desktop–mobile pairs;</p>
<p>•	Maximum hash difference 𝐻=10;</p>
<p>•	Minimum text similarity threshold 𝑇𝑆=0.7;</p>
<p>•	Minimum neighbor similarity threshold 𝑁𝑆=0.8.</p>

These values consistently resulted in high F-scores and a good trade-off between precision and recall across varying IOU thresholds. Notably, adjusting 𝐾 per dataset improved robustness when layout or platform changes altered neighborhood structures. All comparative results were obtained using these tuned parameters.</p>
