
# Edge Detection of Crop Images to detect germination of pollen grains
## Authors

- [@Siri-7](https://www.github.com/Siri-7)


## Installation and Code

```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
import glob
import os

images = []
filename = []
for file in glob.glob("pollen/*.jpg"):
    image = cv2.imread(file)
    images.append(image)
    filename.append(file[7:])
 
 
length = len(images)
for i in range(length):
    gray = cv2.cvtColor(images[i], cv2.COLOR_BGR2GRAY)
    edges = cv2.Canny(gray, threshold1=40, threshold2=40)
    output_file = str(filename[i]) 
    path = r'C:\Users\siris\pollen_saves'
    save_images=cv2.imwrite(os.path.join(path,output_file),edges)

```
    