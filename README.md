custom_workflows

A central repository for ComfyUI workflows and custom nodes developed for the EmAySee AI Ecosystem (TUFGUY, PHANTOM, and SPECTRE). This collection is optimized for high-performance generation and LoRA training on NVIDIA 16GB VRAM architectures (RTX 4070 Ti SUPER and 5060 Ti).

🚀 Key Components

Custom Nodes

All custom nodes are prefixed with EmAySee_ for easy identification within the ComfyUI search menu.

EmAySee_MultiMaskToBBOX: Converts up to 10 input masks into a single, unified bounding box based on the farthest points of all detected regions. Useful for complex inpainting and regional conditioning.

Workflows

EmAySee_Qwen_Pose_Controlnet_2511: A specialized workflow utilizing Qwen-based vision models for precise pose estimation and ControlNet application.

Z-Image Turbo (ZIT) Training: Workflows tailored for training distilled SDXL LoRAs using natural language captioning.

🛠 Installation

For Custom Nodes

Navigate to your ComfyUI custom nodes directory:

cd /path/to/ComfyUI/custom_nodes/


Clone this repository:

git clone [https://github.com/EmAySee/custom_workflows.git](https://github.com/EmAySee/custom_workflows.git)


Restart ComfyUI.

For Workflows

Simply drag and drop the .json files from the workflow folders directly into your ComfyUI interface.

🖥 Hardware Integration

These workflows are designed to run across a networked environment:

PHANTOM: Primary generation and LoRA training (RTX 4070 Ti SUPER).

SPECTRE: Secondary generation and LLM inference (RTX 5060 Ti).

TUFGUY: Central orchestration and management hub.

📜 License

Personal use / MIT.
