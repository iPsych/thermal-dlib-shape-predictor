# Compare dlib shape detector on images in diferent spectrums

In this project we train dlib shape predictor to predict face shapes on thermal images. We want to compare our predictor with common using face shape prediction which was train on normal images (visible spectrum).

For face detection we use simple Haar-like features cascade.

## Runing scripts
Dependencies:
```
pip install numpy
pip install opencv-python
pip install imutils
pip install dlib
```
For dlib installation you may need to install several additional tools, like `cmake` and `Visual Studio build tools`.

Runing:
```
py .\run.py
```

## Images dataset
Inside folder `/images` we assume exist several folders for different models. On each folder may exist various pair images - Thermal and RGB, in the same size. The name for each images consist of 4-letter image identiefier, and suffix indicating image type.

## Results
The scripts for each image Pari return following summary:
```
#004 #003 [3.5686937077518217, 0.0, 13.0]
```
It means, in folder `#004`, comparing images `#003`, face shape prediction has:
-mean distance `3.5686937077518217`,
-`0.0` minimum distance,
-`13.0` maximum distance,
between two corresponding shape points. Distance is expressed in pixels.

## Inside scirpts

### `scripts/draw_shape.py`
Function `draw_shape` gets:
```
img,          - image in grayscales to detect and predict face shape
cascade,      - xml with Haar like feature cascade detector
predictor,    - trained dlib shape predictor
show          - flag, toggle display image in window (default set to false)
```
Function return `shape` object as numpy array of 68 facial feature points, or empty array, when there is no face detection.

### `scripts/compare_files.py`
For pair of thermal and visual images, function `compare_files` calculates distances (in pixels) between shapes predicted in `draw_shape` function.