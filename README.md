OWAFNet Anonymous Reproducibility Package

This repository contains the anonymous code package associated with OWAFNet for music emotion recognition. The package is organized to separate model implementation, dataset configuration, preprocessing, training, evaluation, analysis utilities, reference-only verification artifacts, documentation, and automated tests.

Repository Contents

OWAFNet_Anonymous_Reproducibility_Package/
├── .github/
│   └── workflows/
│       └── ci.yml
├── configs/
│   ├── datasets/
│   │   ├── deam.yaml
│   │   └── pmemo.yaml
│   ├── models/
│   │   ├── bilstm.yaml
│   │   ├── cnn.yaml
│   │   ├── owafnet.yaml
│   │   ├── resnet18.yaml
│   │   └── transformer.yaml
│   ├── ablations.yaml
│   ├── hyperparameter_grid.yaml
│   └── pretrained.yaml
├── data/
│   ├── manifests/
│   │   ├── deam.example.csv
│   │   └── pmemo.example.csv
│   └── README.md
├── docs/
│   ├── EXPERIMENT_PROTOCOL.md
│   └── OUTPUT_SCHEMA.md
├── logs/
│   └── reference_only/
├── results/
│   └── reference/
├── scripts/
├── splits/
│   └── README.md
├── src/
│   └── owafnet/
└── tests/

Core Source Code

The src/owafnet/ directory contains the main Python implementation.

models.py — OWAFNet and comparison-model definitions, including the convolutional, attention, recalibration, fusion, local-representation, and classification components used by the package.

training.py — training, validation, checkpoint selection, prediction export, and run-level output handling.

data.py — dataset and manifest loading utilities for processed log-Mel features.

preprocessing.py — audio loading, resampling, cropping or padding, and log-Mel spectrogram extraction.

augmentation.py — training-time rolling and spectrogram masking operations.

metrics.py — multitask classification metrics, calibration metrics, and related evaluation utilities.

analysis.py — shared statistical and run-analysis functions.

pretrained.py — wrappers for pretrained audio encoders used in comparison experiments.

config.py — YAML configuration loading and configuration-merging utilities.

reproducibility.py — random-seed control, deterministic execution settings, worker initialization, and environment capture.

__init__.py — package initialization.

Configuration Files

The configs/ directory contains experiment definitions.

Dataset configurations

configs/datasets/pmemo.yaml — PMEmo preprocessing, partition, augmentation, and training settings.

configs/datasets/deam.yaml — DEAM preprocessing, windowing, partition, augmentation, and training settings.

Model configurations

configs/models/owafnet.yaml — OWAFNet architecture and optimization configuration.

configs/models/cnn.yaml — CNN comparison configuration.

configs/models/bilstm.yaml — BiLSTM comparison configuration.

configs/models/transformer.yaml — Transformer comparison configuration.

configs/models/resnet18.yaml — ResNet-18 comparison configuration.

Additional experiment configurations

configs/ablations.yaml — ablation variants for fusion, recalibration, context modeling, augmentation, and component removal.

configs/hyperparameter_grid.yaml — hyperparameter search-space definitions.

configs/pretrained.yaml — configurations for Wav2Vec2, HuBERT, and AST based comparison experiments.

Data Interface Files

The data/ directory contains data-interface documentation and example manifests.

data/README.md — expected dataset-manifest organization and data-preparation requirements.

data/manifests/pmemo.example.csv — example PMEmo manifest format.

data/manifests/deam.example.csv — example DEAM manifest format.

The repository does not include redistributed raw audio files.

Split Documentation

The splits/README.md file documents the expected frozen item-level split files and their organization. Split generation is handled by the scripts included in the package.

Experiment and Utility Scripts

The scripts/ directory contains command-line utilities for data preparation, training, analysis, auditing, and verification.

preprocess_audio.py — converts source audio into the feature representation used by the models.

make_splits.py — creates deterministic item-level dataset partitions and associated audit information.

train.py — trains and evaluates OWAFNet or configured comparison models.

train_pretrained.py — runs experiments based on supported pretrained audio encoders.

run_local_seed_sweep.sh — launches the configured multi-seed experiment sequence.

run_ablation_suite.sh — launches configured ablation variants.

sample_search_grid.py — generates or samples configurations from the conventional-model search grid.

sample_pretrained_grid.py — generates or samples pretrained-model configurations.

prepare_boundary_split.py — prepares label-boundary sensitivity split definitions.

run_boundary_sensitivity.sh — launches boundary-sensitivity experiments.

benchmark.py — measures model-forward timing and memory-related execution information.

bootstrap_differences.py — performs paired bootstrap comparisons from prediction files.

attention_analysis.py — analyzes exported attention-related quantities.

representation_analysis.py — analyzes exported learned representations.

arousal_valence_analysis.py — performs arousal- and valence-specific auxiliary analyses.

export_model_outputs.py — exports internal model outputs required by downstream analysis scripts.

summarize_runs.py — aggregates run-level output files into summary records.

audit_parameters.py — audits documented and implemented parameter counts.

verify_reference_results.py — checks reference-only metric fixtures against the package's verification definitions.

generate_reference_fixtures.py — creates reference-only files used by verification utilities.

smoke_test_core.py — performs a lightweight executable check of core package components.

anonymity_audit.py — scans repository text files for configured identity, local-path, credential, and token patterns.

Documentation

The docs/ directory contains protocol-level documentation.

docs/EXPERIMENT_PROTOCOL.md — defines dataset handling, target construction, preprocessing, augmentation, optimization, evaluation, uncertainty analysis, and timing procedures.

docs/OUTPUT_SCHEMA.md — defines the files and fields produced by an experiment run.

Automated Tests

The tests/ directory contains tests for the main reproducibility utilities.

test_configs.py — validates configuration files.

test_preprocessing.py — checks preprocessing behavior.

test_metrics.py — checks metric calculations.

test_seed_statistics.py — checks seed-level statistical utilities.

test_parameter_audit.py — checks parameter-audit logic.

test_reference_values.py — checks reference-only verification values.

conftest.py — shared test configuration.

Reference-Only Artifacts

The package contains two directories reserved for reference and verification material:

results/reference/ — structured reference definitions, reference prediction fixtures, and verification metadata.

logs/reference_only/ — reference-only log and protocol files used for package inspection and automated checks.

These files are separated from empirical run outputs and are identified as reference-only artifacts within the package.

Continuous Integration

.github/workflows/ci.yml defines automated checks for core tests, reference-file verification, and anonymous-text auditing.

Task Coverage

The package contains code and configuration support for:

OWAFNet model construction.

PMEmo and DEAM data interfaces.

Arousal and valence prediction.

Audio preprocessing and log-Mel feature extraction.

Deterministic dataset splitting.

Training and validation.

Multi-seed execution.

Conventional neural-network comparison models.

Pretrained audio-encoder comparisons.

Ablation experiments.

Hyperparameter configuration.

Label-boundary sensitivity analysis.

Bootstrap-based comparison utilities.

Attention and representation analysis.

Runtime benchmarking.

Parameter auditing.

Reference-only consistency verification.

Automated testing and anonymous-repository checks.
