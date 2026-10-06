# ComfyUI Kaggle

A reproducible ComfyUI + SDXL image-generation environment designed to run on Kaggle GPUs.

## Project Status

🚧 In development.

## Architecture

- **GitHub** — workflows, configuration, scripts, and documentation
- **Kaggle** — GPU compute and ComfyUI runtime
- **Local machine** — persistent inputs and generated outputs

## Pipeline

```text
RealVisXL
    ↓
Character LoRA
    ↓
DWPose + ControlNet
    ↓
Base Generation
    ↓
FaceDetailer
    ↓
Final Image
