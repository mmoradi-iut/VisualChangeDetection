# VisualChangeDetection
A graph-based AI method for context-aware visual change detection in software user interfaces

In this repository, you can find information, results, data, and source codes of the context-aware visual change detection method. The method and experiments are described and discussed in the paper titled "Artificial intelligence for context-aware visual change detection in software test automation".

<h2>The context-aware visual change detection method</h2>
<p>The following image illustrates the overal architecture of our visual change detection method:</p>
<br>
<img width="800" src="https://github.com/mmoradi-iut/VisualChangeDetection/blob/main/Figure-1.jpg">

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
<img width="800" src="https://github.com/mmoradi-iut/VisualChangeDetection/blob/main/Table-1.jpg">
