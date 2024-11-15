---
title: "Project5: Fun With Diffusion Models!"
date: 2024-11-05
url: "/CS180/5"
authors:
  - admin
tags:
    
math: true

type: report
---

## Part A: The Power of Diffusion Models!

### Setup

For this project, I set the random seed to 180 manually to ensure reproducibility of the results. The DeepFloyd diffusion pipeline utilizes a multi-stage inference process. In Stage 1, images are generated at a resolution of 64x64, which results in lower quality. However, in Stage 2, the resolution is increased to 256x256, resulting in a significant improvement in quality. Each generated image accurately represents the description provided in the prompt, although there are slight imperfections in the eye area of the generated people. Additionally, I experimented with varying the number of inference steps. Increasing the inference steps leads to enhanced detail quality, but it also requires a trade-off with the substantially increased runtime.

#### Stage1 with 20 steps
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/1_64.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of a snowy mountain village</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/2_64.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a man wearing a hat</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/3_64.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
</div>

#### Stage2 with 20 steps

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/1_256.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of a snowy mountain village</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/2_256.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a man wearing a hat</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/3_256.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
</div>

#### Stage1 with 100 steps
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/1_64_100.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of a snowy mountain village</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/2_64_100.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a man wearing a hat</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/3_64_100.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
</div>

#### Stage2 with 100 steps

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/1_256_100.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of a snowy mountain village</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/2_256_100.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a man wearing a hat</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/setup/3_256_100.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
</div>


## Sampling Loops

### Implementing the Forward Process

Firstly, we need to implement the forward process:

$$ x_t = \sqrt{\bar{\alpha_t}}x_0 + \sqrt{1-\bar{\alpha_t}}\epsilon$$

The following shows the results after adding noise at timesteps 250, 500, and 750.
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/clean.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/250_noisy.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">t = 250</p>
    </div>
</div>
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/500_noisy.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 500</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/750_noisy.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 750</p>
    </div>
</div>

### Classical Denoising

Here, I applied the classic denoising method, Gaussian Blur, with a kernel size of 3 and a sigma of 0.8.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/250_noisy.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">t = 250</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/500_noisy.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 500</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/750_noisy.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 750</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/250_gau.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">t = 250</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/500_gau.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 500</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/750_gau.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 750</p>
    </div>
</div>

It can be observed that the images remain very blurred after applying Gaussian Blur, with no improvement in quality.

### One-Step Denoising

To retrieve the original image \( x_0 \) from the noisy image, we need to predict the noise \( \epsilon \) using DeepFloyd and then apply the transformation formula to reconstruct the original image:


$$ x_0 = \dfrac{x_t - \sqrt{1-\bar{\alpha_t}}\epsilon}{\sqrt{\bar{\alpha_t}}} $$

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/clean.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/250_clean.png" alt="First Image" style="width: 100%;">
        <p style="text-align: center;">one-step t = 250</p>
    </div>
</div>
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/500_clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">one-step t = 500</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/750_clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">one-step t = 750</p>
    </div>
</div>

### Iterative Denoising

For iterative denoising, the first step is to create a series of strided timesteps. Here, I opted to start at 990 with a stride of 30, progressively decreasing until reaching 0.

$$
x_{t'} = \frac{\sqrt{\overline{\alpha}_{t'} \beta_t}}{1 - \overline{\alpha}_t} x_0 + \frac{\sqrt{\alpha_t (1 - \overline{\alpha}_{t'})}}{1 - \overline{\alpha}_t} x_t + v_{\sigma}
$$

Following the formula above, we progressively denoise the noisy image in steps. Below is a visualization of the iterative denoising process, showing the results at every fifth step.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 690</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 540</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 390</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/4.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 240</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">t = 90</p>
    </div>
</div>

#### Comparison when t=690
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Iterative Denoised</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/onestep.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">One-Step Denoised</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/iter/gau.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Gaussian Blurred</p>
    </div>
</div>

From the results above, it's evident that iterative denoising significantly outperforms one-step denoising in terms of image quality, albeit at the cost of increased processing time.

### Diffusion Model Sampling

Here, I generated five random images using pure random noise with the prompt "a high quality photo".

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/DM/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/DM/2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/DM/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/DM/4.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/DM/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
</div>

Judging from the results, these five images lack significant semantic information and have relatively poor quality.

### Classifier Free Guidance

In CFG, we compute both a noise estimate conditioned on a text prompt, and an unconditional noise estimate. We denote these $\epsilon_c$ and $\epsilon_u$. Then, we let our new noise estimate be

$$\epsilon = \epsilon_u + \gamma (\epsilon_c - \epsilon_u)$$

Here, I used $\gamma=7$.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/CFG/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/CFG/2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/CFG/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/CFG/4.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/CFG/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;"></p>
    </div>
    
</div>

Compared to the previous Diffusion Model Sampling, the image quality here has improved significantly, with each image carrying distinct semantic information.

### Image-to-image Translation

In diffusion, adding varying levels of noise to an image enables image-to-image translation. As the noise level increases, the generated image diverges more from the original, allowing us to control the degree of translation. This approach provides flexible adjustment for the extent of transformation applied to the image.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/sample/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

#### Editing Hand-Drawn and Web Images

##### Web Image
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/web/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

##### Hand-Drawn 1
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd1/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

##### Hand-Drawn 2

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/i2i/hd2/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

#### Inpainting

Image inpainting can be achieved by denoising only one patch at a time while keeping the rest of the image unchanged. This approach allows us to modify specific areas while maintaining the style of the original image, enabling targeted edits that blend seamlessly with the original content.

#### Campanile
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/test/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/test/mask.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">mask</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/test/replace.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">to replace</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/test/result.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">inpainted</p>
    </div>
</div>

#### Hand-Drawn Image
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/hd/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/hd/mask.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">mask</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/hd/replace.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">to replace</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/hd/result.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">inpainted</p>
    </div>
</div>

#### Web Image
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/web/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/web/mask.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">mask</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/web/replace.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">to replace</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/web/result.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">inpainted</p>
    </div>
</div>

### Text-Conditional Image-to-image Translation

In the denoising process, adding a semantic condition can guide the content of the output. As the amount of added noise decreases, the results are increasingly controlled by the input image rather than the prompt. This allows for fine-tuning the influence of the input image versus the prompt, enabling more precise content manipulation based on the original image.

#### Campanile with prompt "a rocket ship"
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/inpainting/test/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

#### Hand-Drawn 1 with prompt "an oil painting of people around a campfire"

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd1/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

#### Hand-Drawn 2 with prompt "an oil painting of a snowy mountain village"
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">1</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">3</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">5</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/7.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">7</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">10</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">20</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/prompt/hd2/clean.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">raw image</p>
    </div>
</div>

### Visual Anagrams

To generate visual anagrams, we input two prompts simultaneously. One prompt guides the regular denoising of the image, while the other applies denoising to a flipped version of the image. Finally, we average the two noise predictions and denoise the image accordingly, achieving a result that carries semantic information from both the normal and flipped perspectives.

$$\epsilon_1 = \text{UNet}(x_t, t, p_1) $$
$$\epsilon_2 = \text{flip}(\text{UNet}(\text{flip}(x_t), t, p_2))$$
$$\epsilon = \frac{\epsilon_1 + \epsilon_2}{2}$$



<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of an old man</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/1_flip.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of people around a campfire</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/2_flip.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a pencil</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a lithograph of a skull</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/anagram/3_flip.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a man wearing a hat</p>
    </div>
</div>

### Hybrid Images

To generate hybrid images, we perform frequency separation on the noise predicted for each of the two prompts. This approach allows us to embed distinct semantic information in the high-frequency and low-frequency noise components. As a result, the generated image simultaneously contains both types of semantic information—one conveyed through high-frequency details and the other through low-frequency features.

$$\epsilon_1 = \text{UNet}(x_t, t, p_1)$$
$$\epsilon_2 = \text{UNet}(x_t, t, p_2) $$
$$\epsilon = f_{\text{lowpass}}(\epsilon_1) + f_{\text{highpass}}(\epsilon_2)$$


<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a lithograph of waterfalls</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/1_low.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a lithograph of a skull</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of people around a campfire</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/2_low.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">an oil painting of an old man</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/3.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a rocket ship</p>
    </div>
    <div style="flex: 1; padding: 10px;">
        <img src="./A/hybrid/3_low.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">a pencil</p>
    </div>
</div>

### Bells & Whistles

An interesting observation is that DeepFloyd seems to have a bias toward generating human faces or bodies. In scenarios with no conditions or weak conditions, it frequently produces images of faces, likely due to an overrepresentation of faces in the dataset distribution.

I designed a course logo with prompt "Generate a high quality course logo. There is a rectangle sci-fi bounding box in the outermost, a robot eye in the right and fancy style text "CS180" in the left."

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./A/output.jpg" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">CS180 course logo</p>
    </div>
</div>

-------

## Part B: Diffusion Models from Scratch!

### Part 1: Training a Single-Step Denoising UNet

#### Implementing the UNet

In this project, we implement the denoiser as a UNet. It consists of a few downsampling and upsampling blocks with skip connections.
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/unet.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Unconditional UNet</p>
    </div>
</div>

The diagram above uses a number of standard tensor operations defined as follows:
<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/unet_cond.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">UNet Operations</p>
    </div>
</div>

-  Conv doesn't change the image resolution, only the channel dimension.
-  DownConv downsamples the tensor by 2.
-  UpConv upsamples the tensor by 2.
-  Flatten flattens a 7x7 tensor into a 1x1 tensor. 7 is the resulting height and width after the downsampling operations.
-  Unflatten unflattens a 1x1 tensor into a 7x7 tensor.
-  Concat is a simple channel-wise concatenation between tensors with the same 2D shape. This is simply torch.cat.
- D is the number of hidden channels and is a hyperparameter that we will set ourselves.

We define composed operations using our simple operations in order to make our network deeper. This doesn't change the tensor's height, width, or number of channels, but simply adds more learnable parameters.

-  ConvBlock, is similar to Conv but includes an additional Conv. Note that it has the same input and output shape as (1) Conv.
-  DownBlock, is similar to DownConv but includes an additional ConvBlock. Note that it has the same input and output shape as (2) DownConv.
-  UpBlock, is similar to UpConv but includes an additional ConvBlock. Note that it has the same input and output shape as (3) UpConv.

Within the simple operations:
- Conv2d(kernel_size, stride, padding) is nn.Conv2d(kernel_size, stride, padding)
- BN is nn.BatchNorm2d
- GELU is nn.GELU()
- Conv2d⁻¹(kernel_size, stride, padding) is nn.ConvTranspose2d(kernel_size, stride, padding)
- AvgPool(kernel_size) is nn.AvgPool2d(kernel_size)


#### Using the UNet to Train a Denoiser

Recall from equation 1 that we aim to solve the following denoising problem: Given a noisy image $z$, we aim to train a denoiser $D_\theta$ such that it maps $z$ to a clean image $x$. To do so, we can optimize over an $L2$ loss

$$
L = \mathbb{E}_{z,x} \|D_\theta(z) - x\|^2.
$$

To train our denoiser, we need to generate training data pairs of $(z, x)$, where each $x$ is a clean MNIST digit. For each training batch, we can generate $z$ from $x$ using the following noising process:

$$
z = x + \sigma \epsilon, \quad \text{where} \quad \epsilon \sim N(0, I).
$$

Visualize the different noising processes over $\sigma = [0.0, 0.2, 0.4, 0.5, 0.6, 0.8, 1.0]$, assuming normalized $x \in [0, 1]$. It should be similar to the following plot:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/noise.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Visiualization of image with noise</p>
    </div>
</div>

#### Training
- We train a denoiser to denoise noisy image $z$ with $\sigma=0.5$ applied to a clean image $x$.
- I trained this UNet for 5 epochs
- I used the Unconditional UNet network with 128 hidden dims
- I set the learning rate 1e-4

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/uncond_loss.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Training Loss Curve</p>
    </div>
</div>

The following are the result in training process:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/uncond_epoch1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Results on epoch 1</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/uncond_epoch5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Results on epoch 5</p>
    </div>
</div>

#### Out-of-Distribution Testing

Our denoiser was trained on MNIST digits noised with $\sigma=0.5$. Let's see how the denoise performs on different $\sigma$'s that it wasn't trained for.

Visualize the denoiser result on test set digits with varying levels of noise $\sigma=[0.0, 0.2, 0.4, 0.5, 0.6, 0.8, 1.0]$

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/ood.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Results on digits from the test set with varying noise levels</p>
    </div>
</div>

### Part 2: Training a DDPM Denoising UNet

#### Refactoring Your Unconditional UNet for DDPM

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/unet_condition.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Conditional UNet</p>
    </div>
</div>

#### Implementing DDPM Forward and Reverse Process

Specifically, each forward step adds Gaussian noise in a variance-preserving way for some variance schedule $\{\beta_t\}_{t=1}^T$:

$$
q(\mathbf{x}_{1:T}|\mathbf{x}_0) := \prod_{t=1}^T q(\mathbf{x}_t|\mathbf{x}_{t-1}), \quad q(\mathbf{x}_t|\mathbf{x}_{t-1}) := \mathcal{N}(\mathbf{x}_t; \sqrt{1 - \beta_t} \, \mathbf{x}_{t-1}, \beta_t \mathbf{I}).
$$

Using the reparameterization trick presented in section 2 of the DDPM paper, we can compute effective one-step noising function, since a Gaussian convolved with a Gaussian is still Gaussian.

Concretely, let $\alpha_t := 1 - \beta_t$ and $\bar{\alpha}_t := \prod_{s=1}^t \alpha_s$, then we can sample a noisy $\mathbf{x}_t$ for an arbitrary $t$:

$$
q(\mathbf{x}_t|\mathbf{x}_0) = \mathcal{N}(\mathbf{x}_t; \sqrt{\bar{\alpha}_t} \, \mathbf{x}_0, (1 - \bar{\alpha}_t) \mathbf{I}).
$$

The ddpm_forward() function is implemented by following algorithm 1:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/algo1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">DDPM Forward Process</p>
    </div>
</div>

The ddpm_sample() is implement by following algorithm 2:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/algo2.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">DDPM Sampling Process</p>
    </div>
</div>

#### Putting It All Together

- I trained the model for 20 epochs
- With a learning rate 1e-4

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/cond_loss.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Training Loss Curve</p>
    </div>
</div>

Below is the images of the test result of some epochs:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/epoch1.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Epoch 1</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/epoch5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Epoch 5</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/epoch10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Epoch 10</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/epoch20.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">Epoch 20</p>
    </div>
</div>

In epoch 1, the results for the digit "1" appear as pure noise. One possible explanation is that the digit "1" has a simple linear structure, making it harder for the model to learn from limited data. However, as training progresses, subsequent epochs demonstrate significant improvement in the results.

At the same time, we can observe that as the number of training epochs increases, the quality of the generated images improves significantly, and the control over the categories becomes more precise.

The following shows the results we use different guidance_scale:

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/gs0.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">guidance scale 0</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/gs5.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">guidance scale 5</p>
    </div>
</div>

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/gs10.png" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">guidance scale 10</p>
    </div>
</div>

As the guidance scale increases, the characteristic features of the resulting images become more pronounced (e.g., the strokes of the digits appear thicker). In this case, the CFG amplifies the feature vector of each digit by a certain factor, enhancing the distinct features of each digit to better differentiate between categories.


### Bells & Whistles

I create a sampling gif below.

<div style="display: flex; justify-content: space-around; align-items: flex-start;">
    <div style="flex: 1; padding: 10px;">
        <img src="./B/output.gif" alt="Second Image" style="width: 100%;">
        <p style="text-align: center;">denoise gif</p>
    </div>
</div>
