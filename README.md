# ComfyUI + RealVisXL on Kaggle

A Kaggle notebook that sets up ComfyUI with the RealVisXL V4.0 SDXL checkpoint, pose-control assets, and an interactive browser-based GUI. The notebook starts ComfyUI in a Kaggle GPU runtime and exposes it through a temporary Cloudflare tunnel.

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

## Cell-by-cell breakdown

Below is the step-by-step flow the notebook follows. Each numbered cell is designed to build up a working ComfyUI environment and then expose it safely through a temporary tunnel.

### 01 — Bootstrap ComfyUI

- Creates the working directory structure for ComfyUI in the Kaggle session.
- Downloads or prepares the base ComfyUI project and required runtime dependencies.
- Ensures the environment is ready before the model and custom-node setup begins.

### 02 — Download RealVisXL V4.0

- Downloads the RealVisXL V4.0 SDXL checkpoint into the ComfyUI model directory.
- Prepares the checkpoint path so it can be used by ComfyUI workflows.
- Verifies the model file is present before moving on to setup and validation.

### 03 — Install custom nodes and dependencies

- Installs the key ComfyUI extensions that expand functionality and workflow support.
- This commonly includes ComfyUI Manager, Impact Pack, Impact Subpack, and ControlNet Aux.
- Installs Python dependencies needed by those nodes so the editor can discover them properly.

### 04 — Download auxiliary models

- Pulls in pose and control assets needed for image workflows, such as OpenPose SDXL, DWPose, and YOLOX files.
- Places the supporting models into the expected ComfyUI folders so ControlNet and pose-based tools can load them.
- Prepares the environment for more advanced conditioning and helper nodes.

### 05 — Validate files and repositories

- Checks that the expected files, model folders, and repositories exist.
- Confirms the expected custom nodes and asset directories are in the right locations.
- Fails early if a required installation step is missing, which helps avoid confusing runtime issues later.

### 06 — Launch ComfyUI

- Starts the ComfyUI backend in the notebook environment.
- Usually runs the server in the background on the local Kaggle port, exposing the web UI endpoint.
- Keeps the service alive so the GUI can be reached from the browser via the tunnel.

### 07 — Validate registered nodes

- Calls the local ComfyUI API to confirm the UI/server is responding.
- Checks that the loaded node registry includes the expected custom nodes and extensions.
- Validates that the installation has actually been recognized by ComfyUI before the tunnel is opened.

### 08 — Start email-protected Cloudflare Quick Tunnel

- Verifies that ComfyUI is responding locally before exposing it externally.
- Prompts for an email address privately using `getpass`, so it is not echoed into the notebook output.
- Downloads `cloudflared` if needed and starts a temporary tunneled public URL.
- Uses Cloudflare's email authentication to restrict access to the generated `trycloudflare.com` URL.
- Prints the public tunnel URL that you open in the browser.

### 09 — Final pipeline health check

- Runs a final server/API check after the tunnel setup is ready.
- Confirms the environment is still healthy and ComfyUI is available for interactive use.
- Helps catch issues that may happen only after the service is fully started and exposed.

## Important notes

- This notebook is intended for interactive use. The GUI, tunnel, and temporary URL are not expected to persist after the Kaggle runtime ends.
- Keep the tunnel's email access restriction enabled. Do not publish a live tunnel URL or personal data in notebook outputs.
- The notebook downloads third-party software and model files. Review and follow each upstream project's licenses and terms.
- Upstream repositories and package versions may change. If an update breaks setup, inspect the logs and pin compatible versions as needed.
- The notebook sets up the ComfyUI environment; it does not include a prebuilt image-generation workflow.

