 Real Time Retinal Image Enhancement (ReTIRE)

This is a project we tried to enhance low quality retinal images (blurred / noisy / bad contrast) using deep learning models like **CycleGAN** and **Vision Transformer**. The idea is to make mobile-captured retina images look like proper clinical ones so they can be used for diagnosis or telemedicine.

---

 Dataset Info

We used a mix of datasets from public sources and our own mobile captured ones using a +20D lens. Here's a quick summary:

- **HRF (High-Res Fundus):** really high quality images, often used in research.
- **EyePACS:** has a large collection of diabetic eye images, some are high quality, some aren’t.
- **Mobile captured:** these were taken with a smartphone using +20D lens. These are low-res, real-world images (kinda bad quality sometimes).

We divided them into **Low-Quality** and **High-Quality** sets for training the GAN.

 ⚙️ Preprocessing Done

To get the images ready for training, we did:
- Resize to 256x256 and 512x512 (depend on model)
- Histogram equalization + CLAHE (for better contrast)
- Augmentations: flip, rotate, blur, etc.
- Simulated noise on HQ images to make more LQ examples

 🧠 Model Pipeline

We tried multiple models but mainly used:

1. **CycleGAN** – for unsupervised image-to-image translation
2. **Vision Transformer (ViT)** – focused on fine structures like vessels, optic disc
3. **Super-Resolution network** – to upscale and sharpen images even more

All of this was run mostly in **Google Colab**, using T4 GPU or just CPU sometimes.

---

## 📈 Results

We saw solid improvements in image quality after enhancement. Some technical metrics:

- **PSNR** went up (means better image quality)
- **SSIM** also improved (better structure and detail)

### Visuals:

#### 🖼️ Fig. 3 (T4 GPU)
- Panel A: Low-Quality input image
- Panel B: High-Quality reference
- Panels C-F: Outputs from different models (CycleGAN, Transformer, etc.)

#### 🖼️ Fig. 4 (Colab CPU)
- Same setup but on CPU, still shows good improvements

We saw better vessel clarity, sharpness, and contrast overall. The models worked well even with noisy images.

---

## 😐 Limitations

- If image is **too blurry** or contrast is almost zero, results aren't great.
- Some mobile images are **too distorted**, and models can’t fully fix them.
- Heavily depend on initial image quality.

Still, it does **much better** than plain filters or traditional tools, especially for smartphone eye screening.

---

## 🛠️ Tech Used

- Python
- TensorFlow / PyTorch
- OpenCV
- Google Colab
- CycleGAN, ViT, ESRGAN

---

## 💡 Applications

- Mobile eye checkups in rural areas
- Diabetic retinopathy screening
- Telemedicine diagnostics
- Datasets cleaning for medical AI

---

## 🔧 How to Run

1. Clone the repo
```bash
git clone https://github.com/yourusername/ReTIRE.git
cd ReTIRE
