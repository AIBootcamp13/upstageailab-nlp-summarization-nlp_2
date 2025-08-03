# Dialogue Summarization with PyTorch Lightning & Hydra
A modular, production-ready dialogue summarization system built with PyTorch Lightning and Hydra configuration management.

## 🚀 Quick Start

1.  **Create Environment**
    ```bash
    # Create a minimal environment with Python
    micromamba env create -f environment.yml
    micromamba activate dialogue-summarization
    ```
    **Remove Environment**
    ```bash
    micromamba env list
    rm -rf /opt/conda/envs/dialogue-summarization
    or
    micromamba remove -n dialogue-summarization --all
    ```
2.  **Install Dependencies**
    ```bash
    # Install PyTorch with CUDA support
    pip3 install --pre torch==2.6.0.dev20241112+cu121 torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121 --no-cache-dir
    # Install remaining packages
    pip install -r requirements.txt
    ```

3.  **Train Model**
    ```bash
    python scripts/train.py train --config-name config
    python scripts/train.py train --config-name kobart-base-v2
    python scripts/train.py train --config-name config

    # Use minimal postprocessing for debugging
    python scripts/train.py train --config-name config --override postprocessing=minimal

    ```

    **Debug training run**
    ```bash
    python scripts/train.py train --override training=production
    python scripts/train.py train --override experiment=production
    python scripts/train.py train --experiment production --override
    python scripts/train.py train --override experiment=production
    ```
3.  **Custom Postprocesssing**
    ```bash
    # Use default postprocessing
    python scripts/train.py train --config-name config 

    # Use aggressive postprocessing
    python scripts/train.py train --config-name config --override postprocessing=aggressive
    
    # Use minimal postprocessing for debugging
    python scripts/train.py train --config-name config --override postprocessing=minimal

    # Use custom postprocessing settings via command line
    python scripts/train.py train --config-name config --override postprocessing.remove_tokens=["<usr>","<pad>"] postprocessing.text_cleaning.strip_whitespace=true

    # For inference
    python scripts/inference.py submission /path/to/model.ckpt --override postprocessing=aggressive
    python scripts/inference.py submission /path/to/best/model.ckpt --override postprocessing=aggressive
    
    # For prediction
    python scripts/inference.py predict \
    *0.1384*.ckpt \
    data/dev.csv \
    test_summary_fix.csv

    # (DEPRECATED) For prediction (before using centralized config)
    python scripts/inference.py predict \
    /home/wb2x/workspace/dialogue-summarizer/outputs/models/best-epoch=01-val_rouge_f=val/rouge_f=0.1384.ckpt \
    data/dev.csv \
    test_summary_fix.csv \
    --config-name config-baseline-centralized
    ```

4.  **Generate Predictions**
    ```bash
    python scripts/inference.py submission /path/to/best/model.ckpt

    python scripts/inference.py submission \
    '/home/wb2x/workspace/dialogue-summarizer/outputs/models/best-epoch=06-val/rouge_f=0.4226.ckpt' \
    --output-file submission1.csv
    ```
**Wandb login**
```bash
export WANDB_API_KEY="YOUR_API_KEY"
source ~/.bashrc
wandb login
```

```markdown
## 📁 Project Structure

```
## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박패캠](https://github.com/UpstageAILab)             |            [이패캠](https://github.com/UpstageAILab)             |            [최패캠](https://github.com/UpstageAILab)             |            [김패캠](https://github.com/UpstageAILab)             |            [오패캠](https://github.com/UpstageAILab)             |
|                            팀장, 담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |

## Quick Start

### 1. Environment Setup
```bash
# Create environment
micromamba env create -f environment.yml
micromamba activate dialogue-summarization

# Install PyTorch with CUDA support
pip3 install --pre torch==2.6.0.dev20241112+cu121 torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121 --no-cache-dir
```

### 2. Weights & Biases Setup
```bash
export WANDB_API_KEY="YOUR_API_KEY"
source ~/.bashrc
wandb login
```

### 3. Training
```bash
# Basic training
python scripts/train.py train --config-name config-baseline-centralized

# Experiment variations
python scripts/train.py train --config-name config-baseline-centralized --experiment swap_unbiased_speaker
python scripts/train.py train --config-name config-baseline-centralized --experiment swap_regular_names

# Custom postprocessing
python scripts/train.py train --config-name config --override postprocessing=aggressive
python scripts/train.py train --config-name config --override postprocessing=minimal
```

### 4. Inference
```bash
# Generate submission file
python scripts/inference.py submission /path/to/best/model.ckpt --output-file submission.csv

# Custom prediction
python scripts/inference.py predict /path/to/model.ckpt data/test.csv output.csv
```

## 📁 Project Structure

```
dialogue-summarization/
├── configs/          # Hydra configuration files
├── src/              # Source code
│   ├── data/         # Data processing
│   ├── models/       # Model implementations
│   ├── evaluation/   # Evaluation metrics
│   ├── inference/    # Inference pipeline
│   └── utils/        # Utilities
├── scripts/          # Entry point scripts
├── notebooks/        # Jupyter notebooks
└── tests/            # Unit tests
```

## 🛠️ Configuration

This project uses Hydra for configuration management. Key config groups:

- **model**: Model architecture (KoBART, Solar API)
- **dataset**: Data processing settings  
- **training**: Training hyperparameters
- **inference**: Generation parameters
- **postprocessing**: Output cleaning strategies

## 🔬 Models

### KoBART
- Korean BART model optimized for dialogue summarization
- Supports token swapping for speaker anonymization
- Configurable generation parameters (beam search, repetition penalty, etc.)

### Solar API
- Alternative approach using Solar Chat API
- Useful for comparison and ensemble methods

## 📊 Performance

Current baseline(final): **ROUGE-F1: 0.5025**

Key metrics tracked:
- ROUGE-1, ROUGE-2, ROUGE-L F1 scores
- Generation length statistics
- Training convergence metrics

## 📈 Experiment Tracking

- **Weights & Biases** integration for experiment tracking
- **Hydra** configuration versioning
- **Model checkpointing** with best validation score
- **Early stopping** based on ROUGE-F1 validation score

## 🎯 Key Features

- **Modular Architecture**: Easy to extend and modify
- **Korean Language Support**: Optimized for Korean dialogue summarization
- **Flexible Postprocessing**: Multiple strategies for output cleaning
- **Production Ready**: Comprehensive logging, monitoring, and error handling
- **Reproducible**: Seed management and configuration tracking

## Environment Requirements

- Python 3.10+
- PyTorch 2.6+ with CUDA support
- Transformers 4.41+
- PyTorch Lightning
- Hydra Core
- Weights & Biases

## Cleanup Commands

```bash
# Remove environment
micromamba remove -n dialogue-summarization --all
# or
rm -rf /opt/conda/envs/dialogue-summarization
```
```
## Clear PyCache
```bash
find . -type d -name "__pycache__" -exec rm -rf {} +
```

