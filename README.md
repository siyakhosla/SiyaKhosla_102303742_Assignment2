# Learning Probability Density Functions using GAN

This repository contains the implementation for **Assignment 2**, where the objective is to learn the **probability density function (PDF)** of a transformed random variable using only data samples, without assuming any parametric form of the underlying distribution.

A **Generative Adversarial Network (GAN)** is employed to implicitly model the unknown probability distribution of the transformed data.

---

## Dataset

- **Dataset:** India Air Quality Data  
- **Source:** Kaggle  
- **Feature Used:** NO₂ concentration  

### Data Preprocessing

The dataset is preprocessed by:
- Removing missing values  
- Removing invalid or negative NO₂ readings  

The cleaned NO₂ samples are then used for transformation and distribution learning.

---

## Transformation Parameters

Each NO₂ sample \( x \) is transformed using the following function:

$$z = T_r(x) = x + a_r \sin(b_r x)$$

where the parameters depend on the university roll number $$\( r \).$$

### Parameter Definitions

$$a_r = 0.5 \times (r \bmod 7)$$

$$b_r = 0.3 \times ((r \bmod 5) + 1)$$

### Parameters for the Given Roll Number

- **Roll Number (r):** 102303742  

**Computed Parameters:**
$$a_r = 1.0$$
$$b_r = 0.89999$$

These parameters are computed programmatically and applied to all valid NO₂ samples to obtain the transformed variable \( z \).

---

## GAN Architecture Description

A **one-dimensional Generative Adversarial Network (GAN)** is designed to learn the unknown distribution of the transformed variable \( z \).

---

### Generator

- **Input:** Gaussian noise sampled from a standard normal distribution  
- Fully connected layer with **32 units** and **ReLU** activation  
- Fully connected layer with **32 units** and **ReLU** activation  
- Fully connected output layer with **1 unit**  

The generator maps noise samples to synthetic transformed samples:

$$z_f = G(\epsilon)$$

---

### Discriminator

- **Input:** Scalar value \( z \)  
- Fully connected layer with **32 units** and **LeakyReLU** activation  
- Fully connected layer with **32 units** and **LeakyReLU** activation  
- Fully connected output layer with **Sigmoid** activation  

The discriminator outputs the probability that a given sample is real.

---

## Training Details

- **Loss Function:** Binary Cross-Entropy  
- **Optimizer:** Adam  
- **Learning Rate:** 0.001  
- **Noise Distribution:** Standard normal distribution  

The GAN is trained using only samples of the transformed variable \( z \), without assuming any analytical or parametric form of the underlying probability density function.

---

## PDF Plot Obtained from GAN Samples

After training, a large number of samples are generated from the trained generator.

The probability density function \( p_h(z) \) is estimated using:
- Histogram-based density estimation  
- Kernel Density Estimation (KDE)  

The learned PDF plot obtained from GAN samples demonstrates the ability of the GAN to approximate the underlying data distribution.

---

## Observations

### Mode Coverage

The generator successfully captures the dominant mode of the transformed data distribution. The learned density exhibits a clear primary peak, indicating that the main structure of the distribution is preserved without severe mode collapse.

---

### Training Stability

During training, the generator and discriminator losses show oscillatory behavior, which is characteristic of adversarial learning. Over successive epochs, the losses stabilize, indicating balanced training dynamics between the two networks.

---

### Quality of Generated Distribution

The histogram and KDE obtained from generated samples closely match the empirical distribution of the transformed data. The learned PDF is smooth and continuous, demonstrating that the GAN can effectively approximate a complex, non-linear density without assuming any parametric form.

---

## Conclusion

This assignment demonstrates the use of **Generative Adversarial Networks** for learning an unknown probability density function directly from data samples.

Without assuming any parametric distribution, the GAN successfully approximates the transformed data distribution, highlighting the effectiveness of adversarial learning for density estimation tasks.
