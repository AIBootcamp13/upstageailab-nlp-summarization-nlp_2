# Command Line Usage Guide

This guide covers all available command line options for training, validation, and data analysis.

## 1. Basic Experiment Usage

Use predefined experiment configurations for different training scenarios:

```bash
# Use baseline experiment (recommended starting point)
python scripts/train.py train --experiment baseline

# Use aggressive experiment (higher learning rate, longer training)
python scripts/train.py train --experiment aggressive

# Use debug experiment (fast, small batches for testing)
python scripts/train.py train --experiment debug

# Use production experiment (optimized for final model)
python scripts/train.py train --experiment production
```

## 2. Parameter Overrides

### Quick Parameter Flags
```bash
# Override max_epochs and batch_size
python scripts/train.py train --experiment baseline --max-epochs 12 --batch-size 32

# Combine with advanced overrides
python scripts/train.py train \
    --experiment baseline \
    --max-epochs 10 \
    --batch-size 24 \
    --override training.optimizer.lr=8e-6
```

### Common Configuration Overrides
```bash
# Generation parameters
python scripts/train.py train \
    --experiment baseline \
    --override generation.max_length=80 \
    --override generation.repetition_penalty=1.4

# Model and training settings
python scripts/train.py train \
    --experiment baseline \
    --override model.compile.enabled=false \
    --override training.optimizer.weight_decay=0.02

# Weights & Biases settings
python scripts/train.py train \
    --experiment baseline \
    --override wandb.offline=true \
    --override wandb.tags=[test,experiment]
```

## 3. Debugging and Development

```bash
# Quick debug run (1 batch only)
python scripts/train.py train --experiment debug --fast-dev-run

# Debug with offline logging
python scripts/train.py train \
    --experiment debug \
    --max-epochs 1 \
    --batch-size 2 \
    --override wandb.offline=true

# Test config without full training
python scripts/train.py train \
    --experiment baseline \
    --override training.fast_dev_run=true \
    --override training.limit_train_batches=0.01
```

## 4. Model Validation

```bash
# Basic validation
python scripts/train.py validate \
    --experiment baseline \
    --checkpoint-path outputs/models/best-epoch=05-val_rouge_f=0.1234.ckpt

# Validation with custom generation settings
python scripts/train.py validate \
    --experiment baseline \
    --checkpoint-path path/to/model.ckpt \
    --override generation.num_beams=6
```

## 5. Resume Training

```bash
# Resume with same settings
python scripts/train.py train \
    --experiment baseline \
    --resume-from outputs/models/last.ckpt

# Resume with modified settings
python scripts/train.py train \
    --experiment baseline \
    --resume-from outputs/models/last.ckpt \
    --override training.optimizer.lr=3e-6 \
    --override training.early_stopping.patience=1
```

## 6. Production Training

```bash
# Standard production run
python scripts/train.py train \
    --experiment production \
    --max-epochs 20 \
    --override wandb.tags=[production,final,v1]

# Custom production configuration
python scripts/train.py train \
    --experiment production \
    --batch-size 64 \
    --override training.optimizer.lr=2e-6 \
    --override generation.max_length=45 \
    --override training.early_stopping.patience=5
```

## 7. Comparison Experiments

```bash
# Compare generation lengths
python scripts/train.py train \
    --experiment baseline \
    --override generation.max_length=40 \
    --override experiment_name=baseline_short_summaries

python scripts/train.py train \
    --experiment baseline \
    --override generation.max_length=80 \
    --override experiment_name=baseline_long_summaries

# Compare learning rates
python scripts/train.py train \
    --experiment baseline \
    --override training.optimizer.lr=3e-6 \
    --override wandb.name=baseline_lr3e6

python scripts/train.py train \
    --experiment baseline \
    --override training.optimizer.lr=1e-5 \
    --override wandb.name=baseline_lr1e5
```

## 8. Data Analysis Scripts

```bash
# Analyze dataset statistics
python scripts/analyze_data.py analyze --split val
python scripts/analyze_data.py analyze --split train

# Inspect sample data
python scripts/analyze_data.py sample --split train --index 4
python scripts/analyze_data.py sample --split val --index 0
```

## Tips and Best Practices

1. **Start with `--experiment debug`** for initial testing
2. **Use `--experiment baseline`** for standard training runs
3. **Use `--experiment production`** for final model training
4. **Always specify experiment name** for tracking: `--override experiment_name=my_experiment`
5. **Use `--override wandb.offline=true`** for local testing without logging

