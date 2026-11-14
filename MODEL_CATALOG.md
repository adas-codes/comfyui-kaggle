# Runtime Model & Asset Catalog

This catalog reflects the downloads and installations defined in [`comfyui-realvisxl-public.ipynb`](comfyui-realvisxl-public.ipynb). The notebook downloads assets into the Kaggle runtime; it does not bundle the model weights in this repository. URLs that use an upstream `main` branch or `latest` release can change over time.

## Model weights and inference assets

| Asset | File downloaded | Source | Runtime destination | Purpose |
|---|---|---|---|---|
| RealVisXL V4.0 (SDXL checkpoint) | `RealVisXL_V4.0.safetensors` | [SG161222/RealVisXL_V4.0](https://huggingface.co/SG161222/RealVisXL_V4.0/resolve/main/RealVisXL_V4.0.safetensors) | `/kaggle/working/ComfyUI/models/checkpoints/RealVisXL_V4.0.safetensors` | Base image-generation checkpoint |
| OpenPose SDXL ControlNet | `diffusion_pytorch_model.safetensors` (saved as `xinsir_openpose_sdxl_1.0.safetensors`) | [xinsir/controlnet-openpose-sdxl-1.0](https://huggingface.co/xinsir/controlnet-openpose-sdxl-1.0/resolve/main/diffusion_pytorch_model.safetensors) | `/kaggle/working/ComfyUI/models/controlnet/xinsir_openpose_sdxl_1.0.safetensors` | Pose-conditioned SDXL generation |
| DWPose estimator | `dw-ll_ucoco_384_bs5.torchscript.pt` | [hr16/DWPose-TorchScript-BatchSize5](https://huggingface.co/hr16/DWPose-TorchScript-BatchSize5) | `/kaggle/working/ComfyUI/custom_nodes/comfyui_controlnet_aux/ckpts/dw-ll_ucoco_384_bs5.torchscript.pt` | Pose estimation used by ControlNet Aux |
| YOLOX-L detector | `yolox_l.onnx` | [hr16/yolox-onnx](https://huggingface.co/hr16/yolox-onnx) | `/kaggle/working/ComfyUI/custom_nodes/comfyui_controlnet_aux/ckpts/yolox_l.onnx` | Auxiliary detection model used by ControlNet Aux |

The DWPose and YOLOX files are downloaded through `huggingface_hub.hf_hub_download`; Hugging Face caches the downloads and the notebook copies them into the custom node's `ckpts` directory when needed.

## Runtime software and other downloaded assets

These are installed or fetched by the notebook but are not model weights:

| Item | Source | Runtime use |
|---|---|---|
| ComfyUI | [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI) | Cloned into `/kaggle/working/ComfyUI` if absent; its `requirements.txt` is installed with pip. |
| ComfyUI-Manager | [ ltdrdata/ComfyUI-Manager](https://github.com/ltdrdata/ComfyUI-Manager) | Custom-node manager extension. |
| ComfyUI Impact Pack | [ltdrdata/ComfyUI-Impact-Pack](https://github.com/ltdrdata/ComfyUI-Impact-Pack) | Impact nodes. |
| ComfyUI Impact Subpack | [ltdrdata/ComfyUI-Impact-Subpack](https://github.com/ltdrdata/ComfyUI-Impact-Subpack) | Companion nodes; its `install.py` is run when present. |
| ControlNet Aux | [Fannovel16/comfyui_controlnet_aux](https://github.com/Fannovel16/comfyui_controlnet_aux) | Auxiliary preprocessing and model support, including DWPose and YOLOX. |
| Python packages | Custom-node `requirements.txt` files plus `ultralytics` and `segment-anything` | Installed with pip for custom nodes and auxiliary/detection workflows. |
| `aria2` | System package manager (`apt-get`) | Resumable downloads for the large checkpoint and ControlNet files, when not already installed. |
| `cloudflared` | [Cloudflare cloudflared latest release](https://github.com/cloudflare/cloudflared/releases/latest) | Downloaded for the Kaggle machine architecture by notebook cell 08, if the binary is absent; used to create the temporary email-protected tunnel. |

Custom-node repositories are cloned with `git clone --depth 1` when missing, so the notebook follows their current default branch rather than pinning a specific revision. The cloudflared URL likewise selects the latest release.

## Config entries not downloaded by this notebook

[`configs/models.yaml`](configs/models.yaml) also names `my_influencer_face.safetensors` (a character LoRA) and `face_yolov8m.pt` (a face detector). The notebook does **not** download either file. Do not treat those config names as assets provisioned by this runtime without adding explicit download steps.

## Licensing and reproducibility

Model weights, custom nodes, and binaries are third-party assets. Check each upstream project's license and terms before use or redistribution. Because the notebook uses moving upstream branches/releases, the exact content may change between runs.
