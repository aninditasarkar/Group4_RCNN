# Real-time object detection and tracking using Faster RCNN and DeepSORT

### Table of contents
- Project Abstract
- Methodology (How the project works)
- Experiment
- Result set (CSV format)
- References

## Abstract
Real-time object detection and tracking have become vital in various fields such as surveillance, autonomous vehicles, and human-computer interaction. In this project, we present a system that integrates Faster RCNN (Region-based Convolutional Neural Network) for object detection and DeepSORT (Deep Simple Online and Realtime Tracking) for object tracking. The system is capable of accurately detecting and tracking objects in real-time video streams, distinguishing between still and moving objects, and recording their bounding box coordinates along with unique IDs in a CSV (Comma-Separated Values) file.

The Faster RCNN model is employed for its high accuracy in detecting objects within images, utilizing a region-based approach to identify and classify objects. Once objects are detected, DeepSORT is utilized to track these objects across frames, maintaining consistency in identification even in complex scenarios such as occlusions and temporary disappearances. Additionally, the system incorporates functionality to differentiate between stationary and moving objects, providing valuable insights into object behavior over time.

The output of the system is stored in a CSV file, containing the bounding box coordinates of detected objects along with their corresponding IDs. This structured format enables easy retrieval and analysis of object trajectories and behaviors, facilitating applications such as crowd monitoring, traffic analysis, and anomaly detection.

The implementation of this system offers a flexible and efficient solution for real-time object detection and tracking tasks, with potential applications in diverse domains including security, retail, and transportation.

## Technologies and Algorithms used
- Languages and Libraries used:
    - Python
    - NumPy
    - OpenCV
    - PyTorch
    - TorchVision

- Algorithms Used:
    - Faster RCNN
    - DeepSORT

## Faster R-CNN

### Context:
Before Faster R-CNN (Region-based Convolutional Neural Network), traditional object detection methods relied on two-stage approaches where potential object regions were first proposed and then classified. However, these methods were often computationally expensive due to the need for external region proposal algorithms, such as Selective Search or EdgeBoxes.

### Introduction to Faster R-CNN:
Faster R-CNN, introduced by Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun in 2015, is a state-of-the-art object detection algorithm that integrates region proposal networks (RPNs) directly into the object detection pipeline. This eliminates the need for separate region proposal algorithms and significantly speeds up the detection process.

### Key Components of Faster R-CNN:

1. **Convolutional Backbone Network:**
   Faster R-CNN typically employs a convolutional neural network (CNN), such as VGG, ResNet, or similar architectures, as its backbone network. This network is responsible for extracting high-level features from the input image.

2. **Region Proposal Network (RPN):**
   The RPN is a lightweight neural network that operates on feature maps generated by the convolutional backbone. It generates region proposals, which are candidate bounding boxes likely to contain objects. These proposals are generated at various scales and aspect ratios across the feature map.

3. **Region of Interest (RoI) Pooling:**
   After generating region proposals, RoI pooling is applied to extract fixed-size feature vectors from each proposal. These feature vectors are then fed into a classifier and a bounding box regressor for object classification and localization.

4. **Classifier and Bounding Box Regressor:**
   The classifier assigns object class probabilities to each proposal, determining whether it contains an object and if so, which class it belongs to. Meanwhile, the bounding box regressor refines the coordinates of the proposed bounding boxes to better fit the object's true location.

### Workflow of Faster R-CNN:

1. **Feature Extraction:**
   The input image is passed through the convolutional backbone network, resulting in a feature map that captures hierarchical representations of the image.

2. **Region Proposal Generation:**
   The RPN operates on the feature map to generate a set of region proposals. Each proposal consists of a bounding box and a corresponding objectness score, indicating the likelihood of containing an object.

3. **Region Classification and Localization:**
   The proposed regions are subjected to RoI pooling, producing fixed-size feature vectors. These features are then fed into separate branches for object classification and bounding box regression.

4. **Post-processing:**
   Finally, non-maximum suppression (NMS) is applied to remove duplicate detections and refine the final set of detected objects based on their confidence scores.

### Advantages of Faster R-CNN:

- **Accuracy:** Faster R-CNN achieves high accuracy in object detection tasks due to its ability to learn discriminative features from both region proposals and the entire image.
- **Efficiency:** By integrating region proposal generation directly into the neural network, Faster R-CNN significantly reduces computational overhead compared to traditional two-stage methods.
- **Flexibility:** The modular architecture of Faster R-CNN allows for easy integration with various backbone networks and optimization techniques, making it adaptable to different domains and applications.


## DeepSORT

### Context:
Before DeepSORT (Deep Simple Online and Realtime Tracking), object tracking in video sequences often faced challenges such as maintaining identity consistency across frames, handling occlusions, and dealing with varying object appearances. Traditional tracking methods like Kalman filters or simple association techniques struggled with these complexities.

### Introduction to DeepSORT:
DeepSORT, introduced by Wojciech Zaremba and Alex Bewley in 2017, is an extension of the SORT (Simple Online and Realtime Tracking) algorithm that integrates deep learning techniques for object tracking. It combines the advantages of a deep appearance descriptor with the simplicity and efficiency of the SORT algorithm to achieve state-of-the-art performance in multi-object tracking.

### Key Components of DeepSORT:

1. **Detection Module:**
   DeepSORT begins by detecting objects in each frame of a video sequence using a pre-trained object detection model such as Faster R-CNN or YOLO. These detections provide bounding boxes and associated confidence scores for potential objects.

2. **Feature Extraction:**
   Once objects are detected, DeepSORT extracts appearance features from each object's bounding box using a deep neural network. These appearance features encode the visual characteristics of each object and are crucial for associating objects across frames.

3. **Data Association:**
   DeepSORT employs a data association algorithm to link object detections across consecutive frames and maintain identity consistency. It utilizes both motion information (e.g., predicted object positions based on Kalman filtering) and appearance features to match detections and assign unique IDs to tracked objects.

4. **Kalman Filtering:**
   To predict the state of each object (e.g., position and velocity) between frames and compensate for noisy detections, DeepSORT utilizes Kalman filters. Kalman filters provide estimates of object states based on previous observations and help maintain smooth and consistent trajectories.

5. **Track Management:**
   DeepSORT includes mechanisms for track initialization, termination, and updating. It initializes tracks for newly detected objects, removes tracks for objects that are no longer visible or reliably tracked, and updates existing tracks with new observations.

### Workflow of DeepSORT:

1. **Detection:**
   Object detections are obtained using a pre-trained object detection model, providing bounding boxes and confidence scores for objects in each frame.

2. **Feature Extraction:**
   Appearance features are extracted from the bounding boxes of detected objects using a deep neural network, encoding visual characteristics.

3. **Data Association:**
   Detections are associated across frames using a combination of motion prediction, appearance matching, and track management strategies to maintain identity consistency.

4. **Kalman Filtering:**
   Kalman filters predict the state of each tracked object between frames and help smooth out noisy detections.

5. **Track Management:**
   Tracks are initialized, updated, and terminated based on the availability and reliability of detections, ensuring consistent and accurate object tracking over time.

### Advantages of DeepSORT:

- **Robustness:** DeepSORT's combination of appearance features and motion information enhances robustness in tracking scenarios with occlusions, varying object appearances, and complex motion patterns.
- **Accuracy:** By leveraging deep learning techniques for appearance modeling, DeepSORT achieves high accuracy in multi-object tracking tasks, even in challenging environments.
- **Real-Time Performance:** DeepSORT maintains real-time performance, making it suitable for applications requiring fast and reliable object tracking in video streams.


## Project Workflow
This project uses a functional implementation where each tasks are enclosed within different functions

### Project Structure
| Main.py
| frcnn.py
| human-tracking.py 
| store-result.py
|

## Main.py
-----------

### Context:
Main.py is the core program in this project. This program demonstrates a pipeline for real-time human detection and tracking in a video stream using a combination of Faster R-CNN for initial detection and DeepSORT for subsequent tracking across frames. The project aims to provide a solution for monitoring crowded environments, such as public spaces or events, by accurately detecting and tracking individuals in real-time video footage.

### Code:
```python
   import cv2
   import frcnn as fr
   import human_tracking as ht
   from torchvision import transforms as T

   tensor_transform = T.ToTensor()
   frcnn = fr.Faster_Rcnn()
   human_track = ht.Human_Tracking()

   vidcap = cv2.VideoCapture('Crowd.mp4')

   while vidcap.isOpened():
      success,frame = vidcap.read()
      if not success:
         break
      frame_rs = cv2.resize(frame, (0, 0), fx=0.5, fy=0.5)
      frame_ten = tensor_transform(frame_rs)

      detection = frcnn.human_detection(frame_ten)
      reduced_detection = human_track.extract_features(detection)
      tracked_objects = human_track.track_human(frame_rs, reduced_detection)
      updated_frame = human_track.update_frame(frame_rs, tracked_objects)

      cv2.imshow('tracking', updated_frame)
      if cv2.waitKey(1) & 0xff == ord('q'):
         break

   vidcap.release()
   cv2.destroyAllWindows()
```

### Code Explanation:
---------------------

### Imports:
- `cv2`: Imports the OpenCV library for image and video processing.
- `frcnn`: Imports a custom module (`frcnn`) containing the Faster R-CNN implementation for object detection.
- `human_tracking`: Imports a custom module (`human_tracking`) containing the human tracking functionality.
- `transforms as T`: Imports the `transforms` module from the `torchvision` library for data transformation.

### Object Initialization:
- `tensor_transform = T.ToTensor()`: Initializes an instance of the `ToTensor()` transformation from `torchvision.transforms`.
- `frcnn = fr.Faster_Rcnn()`: Initializes an instance of the Faster R-CNN model for object detection.
- `human_track = ht.Human_Tracking()`: Initializes an instance of the custom human tracking module.

### Video Capture:
- `vidcap = cv2.VideoCapture('Crowd.mp4')`: Opens a video file named 'Crowd.mp4' for reading.

### Processing Frames:
- Processes each frame from the video
- `success, frame = vidcap.read()`: Reads the next frame from the video file.
- `frame_rs = cv2.resize(frame, (0, 0), fx=0.5, fy=0.5)`: Resizes the frame to half of its original size.
- `frame_ten = tensor_transform(frame_rs)`: Transforms the resized frame into a PyTorch tensor.

### Object Detection:
- `detection = frcnn.human_detection(frame_ten)`: Performs object detection using Faster R-CNN on the transformed frame to detect humans.

### Feature Extraction:
- `reduced_detection = human_track.extract_features(detection)`: Extracts features from the detected human objects to reduce the computational load for tracking.

### Human Tracking:
- `tracked_objects = human_track.track_human(frame_rs, reduced_detection)`: Tracks the detected human objects across frames using a custom human tracking algorithm.

### Frame Update:
- `updated_frame = human_track.update_frame(frame_rs, tracked_objects)`: Updates the original frame with bounding boxes and IDs for the tracked human objects.

### Displaying Results:
- `cv2.imshow('tracking', updated_frame)`: Displays the updated frame with tracked human objects in a window titled 'tracking'.
- `cv2.waitKey(0)`: Waits for a key press before continuing.
- `vidcap.release()`: Releases the video file.
- `cv2.destroyAllWindows()`: Closes all OpenCV windows.


## frcnn.py
------------

### Context:
frcnn.py defines a Python class `Faster_Rcnn` that encapsulates a pre-trained Faster R-CNN model provided by the torchvision library. The model is initialized with a ResNet-50 backbone pre-trained on the COCO dataset, making it capable of detecting various objects, including humans, in images. The `human_detection` method accepts an image frame as input and returns the detected objects along with their bounding boxes and confidence scores. This class can be integrated into a larger project for real-time object detection tasks, such as surveillance systems, autonomous vehicles, or video analytics applications.

### Code:
```python
   import torch
   import torchvision

   class Faster_Rcnn:
      def __init__(self):
         # defining and evaluating model
         self.model = torchvision.models.detection.fasterrcnn_resnet50_fpn(pretrained=True)
         self.model.eval()

      def human_detection(cls, frame):
         with torch.no_grad():
               rcnn_model = cls.model
               detection = rcnn_model([frame])
         # return the filtered detection
         return detection

```

### Code Explanation:
---------------------

### Importing Libraries:
- `import torch`: Imports the PyTorch library for deep learning.
- `import torchvision`: Imports the torchvision library, which provides popular datasets, model architectures, and image transformations for computer vision tasks.

### Defining Class `Faster_Rcnn`:
- `class Faster_Rcnn:`: Defines a Python class named `Faster_Rcnn` for handling Faster R-CNN object detection.

### Initializing the Faster R-CNN Model:
- `def __init__(self):`: Initializes the class constructor.
- `self.model = torchvision.models.detection.fasterrcnn_resnet50_fpn(pretrained=True)`: Initializes the Faster R-CNN model architecture using the ResNet-50 backbone pre-trained on COCO dataset. This line loads a pre-trained Faster R-CNN model provided by torchvision.
- `self.model.eval()`: Sets the model to evaluation mode, which disables gradient computation and dropout, ensuring consistent behavior during inference.

### Object Detection Method `human_detection`:
- `def human_detection(cls, frame):`: Defines a method named `human_detection` for performing object detection.
- `with torch.no_grad():`: Context manager to temporarily disable gradient computation, reducing memory consumption and speeding up inference.
- `rcnn_model = cls.model`: Retrieves the Faster R-CNN model from the class instance.
- `detection = rcnn_model([frame])`: Performs object detection on the input `frame` using the Faster R-CNN model. The `frame` is expected to be a tensor representing an image.
- `return detection`: Returns the detection results, which include bounding boxes, labels, and confidence scores for detected objects.


## human-tracking.py
--------------------

### Context:
human-tracking.py defines a Python class `Human_Tracking` that utilizes the `DeepSort` tracker for real-time human tracking in video streams. The class provides methods for extracting features from object detections, associating detections with existing tracks, updating frames with tracked objects, and tracking movement of objects. These functionalities can be integrated into a larger project for various applications such as surveillance, crowd monitoring, and behavior analysis in real-time video streams.

### Code:

```python
   import numpy as np
   import cv2
   from deep_sort_realtime.deepsort_tracker import DeepSort

   class Human_Tracking:
      def __init__(self):
         self.deepsort = DeepSort(max_age=5, embedder="mobilenet")

      # @classmethod
      def extract_features(cls, detection):
         '''
               :param:
               frame : single frame from the video
               detection : list of dictionaries from frcnn model
         '''

         # extract the bounding boxes, labels and scores
         boxes = detection[0]["boxes"].detach().numpy()
         labels = detection[0]["labels"].detach().numpy()
         scores = detection[0]["scores"].detach().numpy()

         # filter out detections less than 50% scores
         confidence = 0.5
         mask = scores >= confidence
         boxes = boxes[mask]
         labels = labels[mask]
         scores = scores[mask]

         # filter non-human detections
         mask = labels == 1
         boxes = boxes[mask]
         scores = scores[mask]

         # resultant detection list for tracking
         result_detection = []
         n = len(boxes)

         for i in range(n):
               xmin, ymin, xmax, ymax = boxes[i]
               result_detection.append(([int(xmin), int(ymin), int(xmax - xmin), int(ymax - ymin)], scores[i], 'person'))

         return result_detection

      
      def track_human(cls, frame, detections):

         deepsort_model = cls.deepsort

         # associate the detections with existing tracks
         tracked_objects = deepsort_model.update_tracks(detections, frame=frame)

         return tracked_objects
         

      def update_frame(self, frame, tracked_objects):
         for obj in tracked_objects:
               # if not obj.is_confirmed():
               #     continue
               bbox = obj.to_ltrb()
               track_id = obj.track_id
               cv2.rectangle(frame, (int(bbox[0]), int(bbox[1])), 
                           (int(bbox[2]), int(bbox[3])), (0, 255, 0), 2)
               cv2.putText(frame, "ID: " + str(track_id), (int(bbox[0]), int(bbox[1]) - 10), 
                           cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 2)
         
         return frame
      
      def track_movement(self, frame, tracked_objects):
         for obj in tracked_objects:
               xmin, ymin, xmax, ymax = obj[:4]
               x = (xmax + xmin) / 2
               y = (ymax + ymin) / 2

               obj_velocity = np.array([x[1] - x[0], y[1] - y[0]])

               # determine if the object is still moving
               if np.linalg.norm(obj_velocity) > 0.1:
                  obj_status = 1
               else:
                  obj_status = 0
               
               # update the status
               obj.append(obj_status)

         return tracked_objects
```

### Code Explanation:
---------------------

### Importing Libraries:
- `import numpy as np`: Imports the NumPy library for numerical computations.
- `import cv2`: Imports the OpenCV library for image and video processing.
- `from deep_sort_realtime.deepsort_tracker import DeepSort`: Imports the `DeepSort` class from a custom module for real-time object tracking.

### Defining Class `Human_Tracking`:
- `class Human_Tracking:`: Defines a Python class named `Human_Tracking` for handling human tracking tasks.

### Initializing the DeepSort Tracker:
- `def __init__(self):`: Initializes the class constructor.
  - `self.deepsort = DeepSort(max_age=5, embedder="mobilenet")`: Initializes an instance of the `DeepSort` tracker with maximum age set to 5 frames and using the MobileNet model for feature embedding.

### Feature Extraction Method `extract_features`:
- `def extract_features(cls, detection):`: Defines a method named `extract_features` for extracting features from object detection results.
  - Extracts bounding boxes, labels, and scores from the provided object detection results.
  - Filters out detections with confidence scores less than 50% and non-human detections.
  - Formats the detections into a list of tuples containing bounding boxes, scores, and labels for tracking.

### Object Tracking Method `track_human`:
- `def track_human(cls, frame, detections):`: Defines a method named `track_human` for tracking humans in frames.
  - Associates the detected objects with existing tracks using the `DeepSort` tracker.
  - Returns the tracked objects with updated track IDs.

### Frame Update Method `update_frame`:
- `def update_frame(self, frame, tracked_objects):`: Defines a method named `update_frame` for updating frames with tracked objects.
  - Draws bounding boxes and track IDs for each tracked object on the frame.
  - Returns the updated frame with visual annotations.

### Movement Tracking Method `track_movement`:
- `def track_movement(self, frame, tracked_objects):`: Defines a method named `track_movement` for tracking movement of objects.
  - Calculates the velocity of each tracked object based on its position in consecutive frames.
  - Determines if an object is still moving or stationary based on its velocity.
  - Appends the movement status to the tracked objects.

