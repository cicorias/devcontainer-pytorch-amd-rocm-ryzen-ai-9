# ROCm PyTorch Development Container

This is a template devcontainer for PyTorch development using AMD ROCm on Ryzen AI systems.

## Background

This devcontainer was created specifically for the following hardware and software configuration:

- **Laptop**: [Framework 13 with AMD Ryzen AI 9 HX 370](https://frame.work/products/laptop-13-gen-amd-ryzen-ai-9-hx-370)
- **OS**: [Omarchy.org 3.2](https://omakub.org/)
- **CPU**: AMD Ryzen AI 9 HX 370 (8+16) @ 5.16 GHz
- **GPU**: AMD Radeon 890M Graphics [Integrated]

## Features

- **Base Image**: `rocm/pytorch:rocm7.1_ubuntu24.04_py3.12_pytorch_release_2.8.0`
- **Python**: 3.12
- **PyTorch**: 2.8.0 with ROCm 7.1 support
- **GPU Access**: Configured for AMD GPU access via `/dev/kfd` and `/dev/dri`

## Included Tools

### VS Code Extensions
- Python
- GitHub Copilot Chat
- Jupyter

### Python Packages
- JupyterLab 4.5.0
- matplotlib 3.10.7
- pandas 2.3.3
- dlai-grader 2.2.0
- scikit-learn 1.6.1

### Shell
- Zsh with Oh My Zsh

## Prerequisites

1. **Docker** with GPU support
2. **AMD ROCm drivers** installed on the host system
3. **VS Code** with the Dev Containers extension

## Usage

1. Open this folder in VS Code
2. When prompted, click "Reopen in Container" (or use Command Palette: "Dev Containers: Reopen in Container")
3. Wait for the container to build and install dependencies
4. Start coding with PyTorch and ROCm!

> [!IMPORTANT] 
When choosing a Jupyter Kernel pick `/opt/venv/bin/python` 

## GPU Configuration

The container is configured with:
- Access to AMD GPU devices (`/dev/kfd`, `/dev/dri`)
- Video group membership for GPU access
- Shared IPC namespace for multi-process support
- `HSA_OVERRIDE_GFX_VERSION=11.0.0` for Ryzen AI compatibility

## Verifying GPU Access

After the container starts, verify GPU access with:

```bash
rocm-smi
```

Or in Python:

```python
import torch
print(f"PyTorch version: {torch.__version__}")
print(f"ROCm available: {torch.cuda.is_available()}")
print(f"GPU device: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'N/A'}")
```

## Customization

- Modify `requirements.txt` to add additional Python packages
- Edit `.devcontainer/devcontainer.json` to customize VS Code settings or add extensions
- Adjust `HSA_OVERRIDE_GFX_VERSION` if needed for your specific GPU

## Notes

- The container runs as `root` for easier GPU access management
- Dependencies are installed automatically via `postCreateCommand`
- GPU devices must be accessible on the host system
