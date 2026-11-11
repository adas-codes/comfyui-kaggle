# ComfyUI + RealVisXL on Kaggle

A Kaggle notebook that sets up ComfyUI with the RealVisXL V4.0 SDXL checkpoint, pose-control assets, and an interactive browser-based GUI. The notebook starts ComfyUI in a Kaggle GPU runtime and exposes it through a temporary, email-protected Cloudflare Quick Tunnel.

## Notebook

Open [`comfyui-realvisxl-public.ipynb`](comfyui-realvisxl-public.ipynb) in GitHub or import it into Kaggle.

## What it installs

- ComfyUI and the RealVisXL V4.0 SDXL checkpoint
- ComfyUI Manager, Impact Pack, Impact Subpack, and ControlNet Aux
- OpenPose SDXL ControlNet, DWPose, and YOLOX assets
- Dependencies and checks for downloaded files, registered nodes, and pipeline health
- An email-authenticated Cloudflare Quick Tunnel for access to the ComfyUI GUI

## Run the notebook

1. Start a Kaggle notebook session with **Internet enabled** and a compatible **GPU accelerator**.
2. Run cells **01–07 in order**. These install ComfyUI and its assets, launch the server, and validate the files and required nodes.
3. Run cell **08** manually. Enter the email address that should be allowed to access the GUI; the input is requested privately.
4. Open the temporary `trycloudflare.com` URL printed by the cell and complete Cloudflare email one-time PIN authentication.
5. Keep the Kaggle session running while using ComfyUI. Cell **09** runs a final health check.

## Important notes

- This notebook is intended for interactive use. The GUI, tunnel, and temporary URL are not expected to persist after the Kaggle runtime ends.
- Keep the tunnel's email access restriction enabled. Do not publish a live tunnel URL or personal data in notebook outputs.
- The notebook downloads third-party software and model files. Review and follow each upstream project's licenses and terms.
- Upstream repositories and package versions may change. If an update breaks setup, inspect the logs and pin compatible versions as needed.
- The notebook sets up the ComfyUI environment; it does not include a prebuilt image-generation workflow.
