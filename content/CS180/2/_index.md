---
title: "Project2: Fun with Filters and Frequencies!"
date: 2024-09-19
url: "/CS180/2"
authors:
  - admin
tags:
    
math: true
---

## Part 1: Fun with Filters

### Finite Difference Operator

In this section, I first applied differential filters in the x and y directions separately and visualized them accordingly. For the gradient magnitude, I computed $\sqrt{dx^2+dy^2}$ for each pixel. Then, I set a threshold of 100 to binarize the high-gradient edge areas. The resulting image clearly showed the contours, but some overly high-frequency information caused noise.


<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/gradient_x.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">x direction gradient</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/gradient_y.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">y direction gradient</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/gradient.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">all direction gradient</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/threshhold_image.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">threshhold image</p>
    </div>
</div>

### Derivative of Gaussian (DoG) Filter

Therefore, I applied a low-pass filter with a Gaussian kernel of (12, 2) to the image, followed by binarization using a threshold of 15. The threshold was lowered because the gradient decreases after the low-pass filtering. However, this helps filter out a lot of noise, resulting in smoother and more continuous contours.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/gradient_blurred.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">blurred image gradient</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./filters/threshhold_image_blurred.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">blurred image threshhold</p>
    </div>
</div>

## Part 2: Fun with Frequencies!

### Image "Sharpening"

Blur the image using a Gaussian filter: $I_{blurred}=I * G$, where $I$ is the original image, $G$ is the Gaussian filter.

The result of a sharpened image:
$$I_{sharpened}=(1+\alpha)\cdot I-\alpha\cdot(I*G)$$

You can control the sharpening intensity of the image by adjusting the value of $\alpha$. Here, I have chosen values of 0.5, 1.5, and 3.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/taj.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/sharpened_alpha0.5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">$\alpha=0.5$</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/sharpened_alpha1.5.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">$\alpha=1.5$</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/sharpened_alpha3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">$\alpha=3$</p>
    </div>
</div>

#### Another cases
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/result_avatar/avatar_blur.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/result_avatar/sharpened_alpha3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">$\alpha=3$</p>
    </div>
</div>


<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/result_photo/photo_blur.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./sharpen/result_photo/sharpened_alpha3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">$\alpha=3$</p>
    </div>
</div>

### Hybrid Images

To make the image blending more realistic, we first need to align the feature points of the two images. To achieve the effect where different content is seen at varying distances, we should separate the low-frequency and high-frequency components of each image. When viewed from a distance, the low-frequency part of the image is visible, while the high-frequency part is visible up close.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/derek_aligned.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">aligned derek</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/nutmeg_aligned.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">aligned nutmeg</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/low_pass_derek.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">low-pass derek</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/high_pass_nutmeg.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">high-pass nutmeg</p>
    </div>
</div>

<div style="text-align: center;">
  <img src="./hybrid/hybrid_image_derek_nutmeg.jpg" alt="Image description" style="display: block; margin: 0 auto;" width="50%"/>
  <p>hybrid image</p>
</div>

<div style="text-align: center;">
  <img src="./hybrid/hybrid_image_derek_nutmeg_fft.png" alt="Image description" style="display: block; margin: 0 auto;" width="100%"/>
  <p>image spectrum</p>
</div>

#### Another 2 cases (with one failure)


<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/Berkeley_aligned.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">aligned Berkeley logo</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/Stanford_aligned.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">aligned Stanford logo</p>
    </div>
</div>

<div style="text-align: center;">
  <img src="./hybrid/hybrid_image_Stanford_Berkeley.jpg" alt="Image description" style="display: block; margin: 0 auto;" width="50%"/>
  <p>hybrid image</p>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/cat_aligned.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">aligned cat</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./hybrid/dog_aligned.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">aligned dog</p>
    </div>
</div>

<div style="text-align: center;">
  <img src="./hybrid/hybrid_image_cat_dog.jpg" alt="Image description" style="display: block; margin: 0 auto;" width="50%"/>
  <p>hybrid image</p>
</div>

However, this is a failure case because too much of the cat's high-frequency information was lost, making it difficult to recognize the cat from a distance. The hybrid parameters need to be adjusted based on this case.

### Gaussian and Laplacian Stacks

Gaussian and Laplacian Stacks are multi-scale image representations commonly used in image processing and blending techniques.

Gaussian Stack: This is a set of progressively blurred versions of an image, created by applying Gaussian filters with increasing levels of smoothing. Each level in the stack captures the image at a lower resolution, preserving only low-frequency information.

Laplacian Stack: Derived from the Gaussian stack, the Laplacian stack highlights the high-frequency information (edges and fine details) by subtracting consecutive levels of the Gaussian stack. Each layer in the Laplacian stack represents the details lost between the blurred levels, allowing precise control over image blending and sharpening.


Here, I selected a Gaussian low-pass filter with a kernel size of 31 and a sigma of 7, using a six-level pyramid.

<div style="text-align: center;">
  <img src="./hybrid/gaussian_pyramids_derek_nutmeg.png" alt="Image description" style="display: block; margin: 0 auto;" width="100%"/>
  <p>gaussian pyramid</p>
</div>

<div style="text-align: center;">
  <img src="./hybrid/laplacian_pyramids_derek_nutmeg.png" alt="Image description" style="display: block; margin: 0 auto;" width="100%"/>
  <p>laplacian pyramid</p>
</div>


### Multiresolution Blending (a.k.a. the oraple!)

To blend the two images more smoothly, I used a Laplacian stack combined with a progressively blurred mask. Here, I applied a Gaussian kernel with a size of 11 and a sigma of 3 in the Laplacian pyramid, and for the blurred mask, I used a Gaussian kernel with a size of 51 and a sigma of 11.

<div style="text-align: center;">
  <img src="./spline/apple_orange_blended.png" alt="Image description" style="display: block; margin: 0 auto;" width="75%"/>
  <p>oraple</p>
</div>


<div style="text-align: center;">
  <img src="./spline/apple_orange_pyramid.png" alt="Image description" style="display: block; margin: 0 auto;" width="100%"/>
  <p>Column1, 2: the Laplacian stack for apple and orange. Column3: gradually blurred mask</p>
</div>

#### Another 2 cases (with one irregular mask)

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/biden.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">Biden</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/trump.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Trump</p>
    </div>
</div>

<div style="text-align: center;">
  <img src="./spline/biden_trump_blended.png" alt="Image description" style="display: block; margin: 0 auto;" width="50%"/>
  <p>splined image</p>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/face.jpg" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">face</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/palm.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">palm</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/mask.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">mask</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./spline/face_palm_blended.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">splined image</p>
    </div>
</div>
