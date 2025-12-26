# EEG Backward Linear Decoding for Speech Envelope Reconstruction

This repository contains the code and materials for a seminar project on **EEG-based speech envelope reconstruction** using a **backward linear decoding model (ridge regression)**.  
The project investigates whether **delta-band EEG (1–4 Hz)** contains sufficient temporal information to reconstruct the speech envelope of continuous natural speech.

## Project Overview

- **Task**: Reconstruct the speech amplitude envelope from EEG recordings  
- **Approach**: Backward (decoding) linear model with time-lagged EEG features  
- **EEG Band**: Delta band (1–4 Hz)  
- **Evaluation**: Pearson correlation with matched vs. mismatched (null) conditions  
- **Focus**:
  - Subject-specific decoding performance
  - Stability of reconstruction across different decision window lengths (1–20 s)

This work is based on established EEG–speech decoding frameworks (e.g. Broderick et al., 2019).

## Dataset

- **Subjects**: 15 participants  
- **Stimuli**: English audiobook recordings  
- **Recording length**: ~15 trials per subject, ~2 minutes per trial  
- **Total data**: ~7.5 hours of EEG  
- **Sampling rate**: 1000 Hz  

Processed EEG, speech envelopes, and synchronization signals are stored in **HDF5** format.

> ⚠️ Raw EEG data are not included due to data protection and course regulations.

## Methods

### EEG Preprocessing
- Notch filtering (power-line noise)
- Bad-channel interpolation
- ICA for ocular and muscle artifact removal
- Band-pass filtering (1–4 Hz)
- Downsampling to 1000 Hz
- EEG–audio alignment via cross-correlation using StimTrak

### Speech Envelope Extraction
- Audio denoising and amplitude normalization
- Envelope extraction
- Delta-band filtering (1–4 Hz)
- Resampling to match EEG sampling rate

### Backward Decoding Model
- Linear ridge regression
- Time-lag window: 0–250 ms
- Multi-channel EEG input
- Regularization parameter optimized via cross-validation

### Evaluation
- Pearson correlation between predicted and true envelopes
- Mismatched (time-shifted) speech envelopes used to estimate chance-level performance
- Analysis of different decision window lengths (1, 2, 5, 10, 20 s)


