# Dialogue Summarization with PyTorch Lightning & Hydra

A modular, production-ready dialogue summarization system built with PyTorch Lightning and Hydra configuration management.

## 🚀 Quick Start

1.  **Create Environment**
    ```bash
    # Create a minimal environment with Python
    micromamba env create -f environment.yml
    micromamba activate dialogue-summarization
    ```
<<<<<<< HEAD
    **Remove Environment**
    ```bash
    micromamba env list
    rm -rf /opt/conda/envs/dialogue-summarization
    or
    micromamba remove -n dialogue-summarization --all
    ```
2.  **Install Dependencies**
    ```bash
    # Install PyTorch with CUDA support (nightly, specific version)
    pip3 install --pre torch==2.6.0.dev20241112+cu121 torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121 --no-cache-dir

    # All other dependencies are installed via environment.yml automatically.
    # If you need extras, add them to environment.yml under pip: section.
=======

2.  **Install Dependencies**
    ```bash
    # Install PyTorch with CUDA support
    pip install torch torchvision torchaudio --index-url [https://download.pytorch.org/whl/cu121](https://download.pytorch.org/whl/cu121)

    # Install remaining packages
    pip install -r requirements.txt
>>>>>>> Fixed critical error in evaluate.py and kobart_model.py. Evaluate method
    ```

3.  **Train Model**
    ```bash
    python scripts/train.py train --config-name config
<<<<<<< HEAD
    python scripts/train.py train --config-name kobart-base-v2
    python scripts/train.py train --config-name config
    python scripts/train.py train --config-name config-baseline-centralized
    # Use minimal postprocessing for debugging
    python scripts/train.py train --config-name config --override postprocessing=minimal


    python scripts/train.py train --config-name config-baseline-centralized --experiment swap_regular_names --max-epochs 1
    python scripts/train.py train --config-name config-baseline-centralized --experiment swap_unbiased_speaker --max-epochs 1

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
    /home/wb2x/workspace/dialogue-summarizer/outputs/models/best-epoch=03-val_rouge_f=val/rouge_f=0.6118.ckpt \
    data/test.csv \
    emergency_fix.csv

    # (DEPRECATED) For prediction (before using centralized config)
    python scripts/inference.py predict \
    /home/wb2x/workspace/dialogue-summarizer/outputs/models/best-epoch=01-val_rouge_f=val/rouge_f=0.1384.ckpt \
    data/dev.csv \
    test_summary_fix.csv \
    --config-name config-baseline-centralized
=======
>>>>>>> Fixed critical error in evaluate.py and kobart_model.py. Evaluate method
    ```

4.  **Generate Predictions**
    ```bash
    python scripts/inference.py submission /path/to/best/model.ckpt
<<<<<<< HEAD

    python scripts/inference.py submission \
    'outputs/models/best-epoch=00-val_rouge_f=val/rouge_f=0.5597.ckpt' \
    --output-file submission13.csv
    ```
**Wandb login**
```bash
export WANDB_API_KEY="YOUR_API_KEY"
source ~/.bashrc
wandb login
```
=======
    ```

>>>>>>> Fixed critical error in evaluate.py and kobart_model.py. Evaluate method

```markdown
## 📁 Project Structure

```

dialogue\_summarization/
├── configs/          \# Hydra configuration files
├── src/              \# Source code
│   ├── data/         \# Data processing
│   ├── models/       \# Model implementations
│   ├── evaluation/   \# Evaluation metrics
│   ├── inference/    \# Inference pipeline
│   └── utils/        \# Utilities
├── scripts/          \# Entry point scripts
├── notebooks/        \# Jupyter notebooks
└── tests/            \# Unit tests

```markdown

## 🛠️ Configuration

This project uses Hydra for configuration management. Key config groups:

- `model`: Model architecture (kobart, solar_api)
- `dataset`: Data processing settings
- `training`: Training hyperparameters
- `inference`: Generation parameters

## 📊 Performance

Current baseline: **ROUGE-F1: 47.1244**

## 🔬 Models

- **KoBART**: Korean BART model for dialogue summarization
- **Solar API**: Alternative approach using Solar Chat API

## 📈 Experiment Tracking

Integration with Weights & Biases for experiment tracking and model versioning.
```



-----
