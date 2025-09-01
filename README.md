# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
```
#Workshop
#Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
**Name:** PRASHANTH K   **Reg No** 212223230152
```
```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread(r"C:\Users\admin\Downloads\img.jpg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="522" height="563" alt="image" src="https://github.com/user-attachments/assets/496d981e-c290-4e9b-8101-9cf1070abc32" />

```
faceImage.shape
(531, 413, 3)
```

```
#resized_faceImage.shape
faceImage.shape
(531, 413, 3)
```
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread(r"C:\Users\admin\Downloads\sunglass-png-aviator-sunglass-png-pic-627.png",-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="766" height="380" alt="image" src="https://github.com/user-attachments/assets/3325cca8-eeb6-4f22-b070-42787f2ee621" />

```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(210,90))
print("image Dimension ={}".format(glassPNG.shape))
image Dimension =(90, 210, 4)
```

```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

```
<img width="1391" height="346" alt="image" src="https://github.com/user-attachments/assets/e35e3603-bab2-4307-b532-7273c65a91d0" />

```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[210:300,110:320]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

```
<img width="516" height="560" alt="image" src="https://github.com/user-attachments/assets/ab38189c-79ab-4bf1-8c7e-015a7052e76a" />

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[210:300,110:320]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

```
<img width="1367" height="269" alt="image" src="https://github.com/user-attachments/assets/14588f42-618a-44b0-be13-4edf5f9fbe8d" />

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[210:300,110:320]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");

```
<img width="1271" height="739" alt="image" src="https://github.com/user-attachments/assets/3e91a866-0a60-499d-a999-6bde8d48c634" />

## Result:
Thus Adding Sunglasses to Your Passport Photo Using OpenCV is executed successfully





