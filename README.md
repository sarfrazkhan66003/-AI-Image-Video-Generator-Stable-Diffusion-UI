# -AI-Image-Video-Generator-Stable-Diffusion-UI

  An advanced Google Colab–based interface built using Stable Diffusion v1.5 for generating:
  - 📷 High-quality AI images
  - 🎬 Cinematic AI videos with smooth camera motion
  - 🖼 Multiple aspect ratios
  - ⚙️ Complete UI controls (steps, seed, guidance, batch, negative prompt)
  This project combines image generation + anime cinematic video generation using prompt-based diffusion.

## ⭐ Overview

  This project provides an interactive AI media generation tool built on top of the Diffusers library.
  
  It includes:
    - A powerful UI using ipywidgets
    - High-quality image generation
    - Video generation using frame-by-frame motion prompts
    - Options for negative prompts, guidance scale, inference steps
    - Customizable aspect ratios (1:1, 4:3, 9:16, 21:9, etc.)
    - Save & download images/videos directly from Colab
  🎯 Designed for creators, researchers, and developers who want Stable Diffusion + cinematic video without complex code.

## 🚀 Features

1. 🎨 Image Generation
  - Custom prompt & negative prompt
  - Adjustable steps (5–80)
  - Adjustable guidance scale (1–20)
  - Batch image generation (1–6)
  - Custom aspect ratios:
        - 1:1
        - 3:4
        - 4:3
        - 9:16
        - 21:9
  - Seed control for reproducibility
  - GPU optimized (FP16 + Xformers)

2. 🎬 Video Generation
  - Creates multi-frame cinematic videos
  - Smooth zoom-based motion
  - Frame interpolation using dynamic prompt variation
  - Adjustable video resolution
  - Exports MP4 using FFmpeg backend

3. 🧰 UI + Controls
  - Text boxes for prompts
  - Sliders for steps, guidance, batch
  - Aspect ratio dropdown
  - Real-time gallery preview
  - Image download links
  - Video download link

## 📁 Project Structure

  ├── cinematic_video_sd.py      # Cinematic video generator
  ├── sd_image_video_ui.ipynb    # Main Colab interface (UI + video)
  ├── video_frames/              # Auto-generated video frames
  ├── generated_video.mp4        # Final video output
  └── README.md                  # Documentation

##🧠 System Architecture

   User Input
       ↓
  ( Prompts / Settings / Resolution )
       ↓
  Stable Diffusion Pipeline (Diffusers)
       ↓
   Text Encoder → UNet → VAE Decoder
       ↓
  Generated Images
       ↓
  Gallery Display & Downloads
       ↓
  [ OPTIONAL ]
   Motion Prompt Generator
       ↓
   Frame-by-Frame Rendering
       ↓
   ImageIO Video Stitcher
       ↓
   Final Cinematic Video (MP4)

## 🔁 Workflow Diagram

                 ┌────────────────────┐
                 │  User Inputs (UI)  │
                 └─────────┬──────────┘
                           │
                           ▼
               ┌────────────────────────┐
               │ Stable Diffusion 1.5   │
               │ (DiffusionPipeline)    │
               └─────────┬──────────────┘
                         │
                ┌────────┴─────────┐
                ▼                  ▼
     ┌─────────────────┐   ┌─────────────────┐
     │ Image Generation │   │ Video Generator │
     └───────┬─────────┘   └────────┬────────┘
             │                      │
             ▼                      ▼
  ┌────────────────────┐   ┌────────────────────┐
  │ Image Gallery UI   │   │ Frame Rendering     │
  └─────────┬──────────┘   └────────┬───────────┘
            │                       │
            ▼                       ▼
   ┌───────────────────┐   ┌─────────────────────┐
   │  Save / Download  │   │ Video Stitch (MP4)   │
   └───────────────────┘   └─────────────────────┘

## 🧮 Algorithm Explanation

  1. Stable Diffusion Image Generation
     Input Prompt → Tokenizer → Text Embedding
          ↓
          U-Net Denoising Loop (Steps 5–80)
          ↓
      Latent → VAE Decoder → RGB Image
  
  2. Video Generation Algorithm
     for each frame (0 → N):
      t = normalize(frame_index)
      motion_prompt = base_prompt + zoom_factor(t)
      img = stable_diffusion(motion_prompt)
      save img
  combine frames → MP4

## 🖥️ UI Components

| Component       | Description                  |
| --------------- | ---------------------------- |
| Prompt          | Main text description        |
| Negative Prompt | Avoid unwanted outputs       |
| Steps Slider    | Controls detail level        |
| Guidance Scale  | Strength of prompt adherence |
| Seed            | Same seed → same output      |
| Batch           | Number of images             |
| Aspect Ratio    | Changes width × height       |
| Generate Button | Runs image generation        |
| Video Button    | Creates cinematic video      |
| Save Button     | Export PNG files             |

## ⚠️ Limitations
  - SD 1.5 cannot produce physically perfect motion between frames
  - UI performance depends on GPU
  - Xformers not available on all Colab runtimes
  - Higher resolution = slower generation
