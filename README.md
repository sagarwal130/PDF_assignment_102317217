# PDF_assignment_102317217
# Learning Probability Density Functions using Data Only

## 1. Transformation Parameters

The original NO₂ concentration values (x) are transformed using the nonlinear function:

z = x + a_r sin(b_r x)

The parameters are derived from the university roll number r = 102317217.

- r mod 7 = 6  →  a_r = 0.5 × 6 = 3.0  
- r mod 5 = 2  →  b_r = 0.3 × (2 + 1) = 0.9  

These parameters are fixed throughout the experiment.

---

## 2. GAN Architecture Description

A Generative Adversarial Network(GAN) is used to learn the unknown distribution of the transformed variable z using samples only.

### Generator
- Input: Random noise sampled from N(0, 1)
- Architecture:
  (i) Fully connected layers: 8 → 32 → 16 → 1
  (ii) ReLU activation in hidden layers
- Output: One-dimensional fake z value

The generator learns to map random noise to samples resembling the real transformed data.

### Discriminator
- Input: One-dimensional z value
- Architecture:
  (i) Fully connected layers: 1 → 32 → 16 → 1
  (ii) ReLU activation in hidden layers
  (iii) Sigmoid activation in the output layer
- Output: Probability indicating whether the input is real or fake

Binary Cross Entropy loss is used, and both networks are trained using the Adam optimizer.

---

## 3. PDF Estimation from GAN Samples

After training, a large number of samples are generated using the trained generator.  
Since GANs do not explicitly provide a probability density function, Kernel Density Estimation(KDE) is applied to the generated samples to approximate the PDF.

The resulting plot represents the learned probability density of the transformed variable z.
<img width="708" height="470" alt="download" src="https://github.com/user-attachments/assets/a5dafd31-82f5-4160-8270-c651fac8bd72" />

---

## 4. Observations

### Mode Coverage
The GAN is able to capture the major modes of the transformed distribution. No severe mode collapse was observed, indicating adequate diversity in generated samples.

### Training Stability
Training remained stable after the initial epochs. Both generator and discriminator losses showed oscillatory but bounded behavior, which is typical in GAN training.

### Quality of Generated Distribution
The estimated PDF from generated samples closely resembles the empirical distribution of the transformed data. Minor smoothing effects are observed due to KDE, but overall distribution shape is preserved.

---

## Conclusion

This experiment demonstrates that GANs can successfully learn an unknown probability distribution using data samples alone, without assuming any parametric form of the underlying PDF.
