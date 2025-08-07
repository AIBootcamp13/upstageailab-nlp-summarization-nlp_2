# Dialogue Summarization with PyTorch Lightning & Hydra

A modular dialogue summarization system for Korean text built with PyTorch Lightning and Hydra configuration management.

## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박패캠](https://github.com/UpstageAILab)             |            [이패캠](https://github.com/UpstageAILab)             |            [최패캠](https://github.com/UpstageAILab)             |            [김패캠](https://github.com/UpstageAILab)             |            [오패캠](https://github.com/UpstageAILab)             |
|                            팀장, 담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |

## 🚀 Quick Start

### 1. Environment Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install PyTorch with CUDA support
pip3 install --pre torch==2.6.0.dev20241112+cu121 torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121 --no-cache-dir
```

### 2. Weights & Biases Setup
```bash
export WANDB_API_KEY="YOUR_API_KEY"
wandb login
```

### 3. Training
```bash
# Basic training
python scripts/train.py train --experiment baseline

# Experiment variations
python scripts/train.py train --experiment baseline --override experiment_name=swap_unbiased_speaker
python scripts/train.py train --experiment baseline --override experiment_name=swap_regular_names
```

### 4. Inference
```bash
# Generate submission file
python scripts/inference.py submission /path/to/best/model.ckpt --output-file submission.csv
```

## 📁 Project Structure

```
dialogue-summarization/
├── configs/          # Hydra configuration files
├── src/              # Source code
│   ├── data/         # Data processing
│   ├── models/       # Model implementations
│   └── utils/        # Utilities
├── scripts/          # Entry point scripts
└── requirements.txt  # Dependencies
```

## 🔬 Models

**KoBART**: Korean BART model optimized for dialogue summarization with configurable generation parameters and speaker anonymization support.

## 📊 Performance

Current baseline: **ROUGE-F1: 0.5025**

## 🛠️ Configuration

Uses Hydra for configuration management with key config groups:
- **model**: Model architecture settings
- **training**: Training hyperparameters  
- **generation**: Text generation parameters
- **postprocessing**: Output cleaning strategies

## Environment Requirements

- Python 3.10+
- PyTorch 2.6+ with CUDA support
- Transformers 4.41+
- PyTorch Lightning
- Hydra Core
- Weights & Biases
