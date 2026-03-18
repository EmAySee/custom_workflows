# Qwen Pose ControlNet NPG Workflow

## Overview

This workflow is a specialized ComfyUI pipeline that utilizes the native multimodal capabilities of **Qwen2-VL** to perform precise pose transfers without relying on traditional external ControlNet modules or OpenPose preprocessors. 

Because Qwen-VL has "built-in" visual comprehension, the workflow bypasses standard ControlNet routing. Instead, it feeds multiple image references directly into a specialized text encoder. The model natively analyzes **Image 1** for the subject's identity, attire, and details, and maps them directly onto the structural pose extracted from **Image 2**. Finally, the output is routed through a **SeedVR2** upscaling subgraph, providing a superior, artifact-free high-resolution finisher.

---

## Key Components

* **Native Vision-Language Conditioning:** Uses the `TextEncodeQwenImageEditPlus` node to ingest multiple images simultaneously alongside the text prompt, bypassing the need for independent ControlNet units.
* **EmAySee Resolution Optimization:** Employs custom `EmAySee_QwenResolutionOptimizer` nodes to ensure input images are perfectly cropped and scaled to match Qwen's optimal aspect ratios and latent dimensions.
* **AuraFlow Sampling:** Utilizes `ModelSamplingAuraFlow` for refined diffusion steps tailored to the loaded checkpoint.
* **SeedVR2 Finisher (Upscaler Subgraph):** Passes the initial generation through a dedicated SeedVR2 DiT and VAE pipeline. This acts as a high-fidelity "Down2Upscaler," effectively replacing older methods like Ultimate SD Upscale for a cleaner, more cohesive final render.

---

## How to Use

### 1. Prerequisites
Ensure you have the following custom node suites installed:
* **ComfyUI-Qwen2-VL** (for the main model and text encoders).
* **ComfyUI-SeedVR2** (for the upscaling finisher).
* **ComfyUI_EmAySee_CustomNodes** (for the resolution optimizers and saving logic).

### 2. Configuration
1. **Load Checkpoints:** * Select your base Qwen model in the `CheckpointLoaderSimple` node.
   * Ensure your SeedVR2 DiT and VAE models are correctly loaded inside the "Upscaler" subgraph.
2. **Assign Images:**
   * **Image 1 (Source):** Upload the image containing your target subject, including their face, outfit, and accessories.
   * **Image 2 (Pose):** Upload the image containing the structural pose you want the subject to mimic.
3. **Prompting:** * Locate the `Set_str_prompt` multiline text node. 
   * Enter your instructions (e.g., *"put the woman in image 1 in pose from image 2. use the exact woman, same outfit and accessories from image 1. Zoom, rotate and pan as needed to fit the pose."*).

### 3. Execution
* Click **Queue Prompt**.
* The workflow will optimize the image resolutions, encode the visual data natively through Qwen-VL, generate the base pose transfer, and finally pipe the result through the SeedVR2 upscaler for the finished, high-resolution output.