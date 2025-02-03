---
title: Digital Image Processing Basics
type: blog
sidebar:
  open: true
date: 2023-11-26
comments: true
---
### Introduction
Digital image processing is the acquisition, analysis, and performing of a wide range of operations on an image.

In digital image processing, there are three types of images:
- Binary
- Grayscale
- RGB
The digital image can be represented within the two-dimensional array.

A binary image is represented by a dimensional array where each cell stores 0 (black) and 1 (white) values.

A grayscale image is a two-dimensional array where values in the array lay in a range from 0 to 255

The RGB has the same range of values as grayscale but has 3 two-dimensional arrays representing each color — Red, Green, and Blue.

With this knowledge, we can, therefore, calculate how many bits are required to store an image:
For binary images, width * height, since each pixel requires 1 bit, we can omit it.
For grayscale image: width * height * 8, since each pixel is represented by 8 bits
For RGB image: width * height * 8 * 3, because it has 3 planes, each plane contains values in a range from 0 to 255

Let’s start with image acquisition. In this article, I will be using Python and the OpenCV library.
We can use the method `imread` from the OpenCV library for image acquisition.

```python {filename="main.py"}
import cv2 as cv

img = cv.imread('gray.jpg')

cv.imshow('Grayscale image', img)
cv.waitKey()
cv.destroyAllWindows()
```

Now, you should see the image.

It’s time for more exciting things. We can do the following mathematical operations on an image:

- Addition — blend two images together
- Subtraction — find the absolute differences between two images
- Multiplication — adding color to line drawing
- Division — find the relative differences between two images.

### Addition
```python {filename="addition.py"}
mport cv2 as cv

img_one = cv.imread('img/image1.png')
img_two = cv.imread('img/image2.png')
img_sum = img_one + img_two

cv.imshow('Sum', img_sum)
cv.waitKey()
cv.destroyAllWindows()
```

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/digital-image-processing-basics-58d572cf5df4" >}}
{{< /cards >}}
