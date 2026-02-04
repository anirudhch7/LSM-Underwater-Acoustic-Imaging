# LSM-Underwater-Acoustic-Imaging

## Overview

This project implements the **Linear Sampling Method (LSM)** for underwater acoustic imaging and target detection. LSM is a powerful computational technique for solving inverse acoustic scattering problems, enabling the reconstruction and localization of underwater objects using sensor array measurements and acoustic signals.
The implementation provides both 2D and 3D reconstruction capabilities, utilizing multi-frequency acoustic data and advanced sparse recovery algorithms to detect and image underwater targets in noisy environments.

## What is LSM?

The **Linear Sampling Method** is a mathematical technique for solving inverse acoustic problems. Instead of simulating how acoustic waves propagate (forward problem), LSM uses actual sensor measurements to determine where objects are located in space. The method is based on:

- **Green's function** from acoustic wave theory
- **Hankel functions** for 2D wave propagation modeling
- **Spherical harmonics** for 3D wave propagation
- **FISTA optimization** for sparse signal recovery

## Key Features

- **Multi-Frequency Imaging**: Processes multiple acoustic frequencies (e.g., 2000, 3000, 4000 Hz) simultaneously with frequency weighting for improved resolution.
- **2D and 3D Reconstruction**: Supports both planar and volumetric imaging of underwater targets.
- **Noise-Robust Detection**: Includes SNR-controlled noise simulation and robust reconstruction algorithms.
- **Sparse Recovery**: Implements FISTA (Fast Iterative Shrinkage-Thresholding Algorithm) for efficient sparse inversion.
- **Performance Evaluation**: Includes ROC curve analysis for detection performance assessment.
- **Flexible Sensor Arrays**: Configurable circular (2D) and spherical (3D) sensor array geometries.

## Methodology

### 1. Acoustic Simulation
The `AcousticSimulator2D` class generates synthetic measurement sensitivity responses (MSR) by:
- Positioning sensors in a circular array around the imaging region
- Computing acoustic wave propagation using Hankel functions
- Accounting for multi-scattering effects between targets
- Adding controlled Gaussian noise at specified SNR levels

### 2. Image Reconstruction
The reconstruction process:
- Creates a spatial grid (2D or 3D) covering the region of interest
- For each grid point, solves an inverse problem using FISTA
- Computes an indicator function that measures the likelihood of a target at each location
- Generates a heatmap/volume showing target locations

### 3. Target Detection
- Applies thresholding to the reconstructed images
- Evaluates detection performance using ROC curves
- Tests robustness across various noise levels and target configurations

## Technical Details

### Algorithms

**FISTA (Fast Iterative Shrinkage-Thresholding Algorithm)**
- Solves the optimization problem: minimize ||A·g - b||^2 + λ||g||_1
- Uses soft thresholding for sparsity enforcement
- Provides fast convergence for compressive sensing problems

**Multi-Frequency Weighting**
- Higher frequencies receive greater weight in reconstruction due to shorter wavelengths providing better spatial resolution
- Combines information across frequency bands for improved imaging quality and robustness

### Physics Model

**2D Wave Propagation**: Uses Hankel function of the first kind (order 0) to model cylindrical wave propagation

**3D Wave Propagation**: Uses spherical Green's function for realistic 3D acoustic fields

## Usage

The main workflow involves:

1. **Define targets**: Specify locations of underwater objects
2. **Simulate measurements**: Generate sensor data using the acoustic simulator
3. **Reconstruct image**: Apply LSM with FISTA to recover target positions
4. **Visualize results**: Plot reconstructed images showing detected targets
5. **Evaluate performance**: Analyze detection accuracy using ROC curves

See the Jupyter notebook `LSM_Underwater_Acoustic_Imaging.ipynb` for detailed implementation and examples.

## Applications

- Underwater robotics and autonomous vehicles
- Sonar and acoustic imaging systems
- Marine survey operations
- Underwater target detection and classification
- Acoustic detection systems for oceanographic research

## Requirements

- Python 3.x
- NumPy
- Matplotlib
- SciPy (for Hankel functions and special functions)

## References

The Linear Sampling Method is based on well-established inverse problem theory used in acoustic imaging, radar, and medical imaging applications.
