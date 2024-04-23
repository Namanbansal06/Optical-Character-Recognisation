# OCR Steps for improvising Text Extraction

There are 7 steps in OCR, we will follow each one of them step by step.

Those 7 steps are :-

1 Normalisation

2 Skew Correction

3 Gray Scale

4 Thinnig and skeletonisation

5 Noise Removal

6 Threshold or Binarisation

7 Image Scaling

My document shows the results based on the OCR confidence, calculated from the image data.
```
image_file = "-------"
img = cv.imread(image_file)
df = pytesseract.image_to_data(img, lang='eng', config='--psm 6', output_type='data.frame')
df[df['conf']>-1]['conf'].mean()
```

Result Format : 

| Parametre | OCR Confidence |
|----------------|----------------|
|With Parametre | Value|
|Without Parametre | Value |


# 1. Normalisation
In computer vision, the pixel normalization technique is often used to speed up model learning. The normalization of an image consists in dividing each of its pixel values by the maximum value that a pixel can take (255 for an 8-bit image, 4095 for a 12-bit image, 65 535 for a 16-bit image).

#### RESULTS :

| Normalization | OCR Confidence |
|----------------|----------------|
|With Normalization | 47.691 |
|Without Normalization | 46.685 |
****

# 2.  Skew Correction
The skew angle is obtained by searching for a peak in the histogram of the gradient orientation of the input grey- level image. The skewness of the document is corrected by a rotation at such an angle. The slant of characters can also be detected using the same technique, and can be corrected by a shear operation.

#### RESULTS :

| Skewness | OCR Confidence |
|----------------|----------------|
|With Skewness | 39.531 |
|Without Skewness | 50.423 |
****

# 3. Gray Scale image
A grayscale (or graylevel) image is simply one in which the only colors are shades of gray. The reason for differentiating such images from any other sort of color image is that less information needs to be provided for each pixel.

#### RESULTS :

| Skewness | OCR Confidence |
|----------------|----------------|
|With Gray | 50.423 |
|Without Gray | NaN |

****

# 4. Thinning and Skeletonization
The end points of the skeleton extend all the way to the edges of the input object. Thinning transforms objects on a binary image to a set of simple digital lines (or arcs), which lie roughly along the objects' medial axis (center line). The structure obtained is not influenced by small inflections on the image object.

##### IT has 2 types: 
1. Thin/ Eroded
2. Thick/ Dilated
   

#### Thin/Eroded
In this we make the image text thinner. example image is shown below.
![alt text](image.png)

#### RESULTS :

| Thin/Eroded | OCR Confidence |
|----------------|----------------|
|With Thin/Eroded | 45.243 |
|Without Thin/Eroded | 50.423 |

****

#### Thick/Dilated
In this we make the image text thicker. example image is shown below.
![alt text](image-1.png)

#### RESULTS :

| Thick/Dilated | OCR Confidence |
|----------------|----------------|
|With Thick/Dilated | 33.242 |
|Without Thick/Dilated | 50.423 |

****

# 5. Noise Removal
Noise reduction is a common task in digital image processing, where you try to remove unwanted or random variations in pixel values from an image. Noise can degrade the quality and clarity of an image, and affect its usefulness for analysis or display.

#### RESULTS :

| Noise Removal | OCR Confidence |
|----------------|----------------|
|With Noise Removal | 44.010 |
|Without Noise Removal | 50.423 |

****

# 6. Thresholding and Binarisation

Image thresholding is a simple, yet effective, way of partitioning an image into a foreground and background. This image analysis technique is a type of image segmentation that isolates objects by converting grayscale images into binary images.

#### RESULTS :

| Thresholding Types | OCR Confidence | 
|--------------------|----------------|
| To_Zero | 50.423 |
| Binary_INV + OTSU | 46.862 |
| Binary + OTSU | 45.373 |
| OTSU | 45.373 |
| Binary Thresh | NaN |
| Binary_INV | NaN |

****

# 7. Image Scaling

An image with a higher DPI has more dots per inch and the image quality is better compared to another image. If we convert the DPI to 300 or 330, there will be more dots per inch in the image and the quality will also increase.

#### RESULTS :

|  Image Scaling | OCR Confidence |
|----------------|----------------|
|With DPI (>=300) | 54.586 |
|With DPI (<300) | 50.423 |

****

# OTHER IMPORTANT OBSERVATIONS / RESULTS

| Parametres | OCR Confidence |
|------------|----------------|
| Inverted Image | 47.465 |
| Gray + OTSU + Binary_INV + Noise | 35.375 |
| Gray + Noise + DPI | 44.494 |
| Inverted + Noise | 40.044 |

****

### CONCLUSION :

```
Most Optimised extraction of text from image we will get from an image with DPI (>=300).
```