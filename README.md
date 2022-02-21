# HandDetector
Hand Detection using Mediapipe Framework [1]. 

This repository contains code that is part of a Sign Language Recognition project. Main objective of the project is to extract hand ROIs from the frames of the video, extract features of hand and feed them to a Neural Network.

**Dataset** : Chicago FS Wild [2]

The "Chicago FS Wild" dataset contains 7304 sequences of which only 142 are accompanied by binding boxes containing the coordinates of the hand ROIs in the frames. This subset of 142 sequences is not enough to train a model for Sign Language Recognition, however it can be used to evaluate a hand tracking algorithm.


## Mediapipe

* pose landmark module: provides 33 2D landmarks for the whole body
* face landmark module: provides 468 3D face landmarks
* hand landmark module: provides 21 3D hand landmarks for each hand it locates.

Το extract hand ROIs, however, only the hand landmark module was needed. This returns the 21 3D hand keypoints for each hand -but does not return the bounding box for the immediate export of hand ROIs- as shown in the image below:

<img width="514" alt="Στιγμιότυπο 2021-07-30, 7 35 02 μμ" src="https://user-images.githubusercontent.com/36016401/132337471-db87bfb2-0ddb-4bba-bca8-60ab9d518b86.png">

Then, I used the predicted hand landmarks to predict the bounding box area for each hand. Here are some examples of images of the dataset with the predicted bounding boxes (blue boxes) and the ground truths (green boxes) provided by the dataset.


<img width="619" alt="Στιγμιότυπο 2021-07-30, 8 03 46 μμ" src="https://user-images.githubusercontent.com/36016401/132338108-0c0071af-df6c-4651-b4ce-53bbbfe35b63.png">
<img width="493" alt="Στιγμιότυπο 2021-07-30, 8 05 14 μμ" src="https://user-images.githubusercontent.com/36016401/132338314-99b21750-e469-4252-b331-638a98f93da4.png">
<img width="523" alt="Στιγμιότυπο 2021-07-30, 8 06 32 μμ" src="https://user-images.githubusercontent.com/36016401/132338331-a1e9a607-f68d-454e-9572-7d5448b41342.png">

### Webcam test 

To test the hand detector live using your webcam, run: 
```
python detect_hands.py --webcam yes
```


## Feature Extraction: 
In order to assign an input sequence to a feature sequence, deep learning-based architectures based on CNNs were used.
The Feature Extraction Model is based on the ResNet architecture and is pretrained using ImageNet. Because we want to export the features only, we will keep the feature layer, average pooling layer and a fully connected layer that extracts a 1024 d vector for each input image. Run: 

```
python get_features.py
```

## References 
[1] [Mediapipe Github page](https://github.com/google/mediapipe)

[2] [Chicago FS Wild Dataset](https://home.ttic.edu/~klivescu/ChicagoFSWild.htm#download)





