# CT Scan Simulator

## Repository  

[IwM](https://github.com/onyxcherry/IwM)

## Team Members

- [**Tomasz Wiśniewski**](https://github.com/onyxcherry)
- **Me [(Bartosz Operacz)](https://github.com/Bordomir)**

## Project Overview

This project is a simulation of a computed tomography (CT) system, implemented in Python. 
It models the process of acquiring scan data from a parallel beam emitter-detector setup and reconstructs cross-sectional images using a sinogram-based approach. 
The program also includes tools for DICOM file handling and quality evaluation using MSE.

## Technology Stack

- **Programming Language**: Python  
- **Development Environment**: Jupyter Notebook  
- **Libraries Used**:
  - Pillow
  - NumPy
  - SciPy
  - Matplotlib
  - Pydicom

## Emitter/Detector Model

- **Type**: Parallel beam model  

## Core Features

### Sinogram Acquisition

- Rays are simulated as passing through pixels in the image.
- For each detector, the sinogram is constructed using the average pixel value (`np.mean()`).
- Additive attenuation is used to simulate ray absorption.

### Sinogram Filtering

- A convolution filter is applied using a 1D mask of size 161 to enhance reconstruction quality.
- Filtering is optional and can be enabled by the user.

### Image Reconstruction

- Back-projection is used to reconstruct the final image from the filtered or unfiltered sinogram.
- Post-processing involves light blurring and value clipping to improve visual clarity.

### DICOM Support

- Ability to read and write DICOM files using the `Pydicom` library.
- Includes examples of exporting reconstructed images to DICOM format.

### Quality Assessment

- **Mean Squared Error (MSE)** is used as an objective metric to compare original and reconstructed images.
- Subjective visual comparisons are also discussed, especially in cases where MSE and visual quality diverge.

## Example Results

### Test Case 1

- **Parameters**:
  - 720 scans
  - 0.5° angle step
  - 720 detectors
  - 180° Beam spread
- **Execution Time**:
  - Without filtering: 48.1 seconds
  - With filtering: 45.8 seconds

**Original image**  
![image](https://github.com/user-attachments/assets/1856f045-6819-4bec-8c44-9eb953b5449c)  

**Reconstructed image without filter**  
![image](https://github.com/user-attachments/assets/749d9729-23ef-4823-9e39-64a0d20e7ce8)  

**Reconstructed image with filter**  
![image](https://github.com/user-attachments/assets/7f90f986-9188-4db3-8366-2e0e75c751c7)  

### Test Case 2

- **Parameters**:
  - Same setup
- **Execution Time**:
  - Without filtering: 1 min 3.8 sec
  - With filtering: 1 min 13.1 sec

**Original image**  
![image](https://github.com/user-attachments/assets/59a695f8-33e6-46f5-811a-50daed2db114)

**Reconstructed image without filter**  
![image](https://github.com/user-attachments/assets/39c70d96-fc6b-4d50-9db5-1ca068a6ffee)

**Reconstructed image with filter**  
![image](https://github.com/user-attachments/assets/12d170d0-e26d-4a70-a973-d5d529e0cee4)

## Parameter Sensitivity Experiment

- **Parameters**:
  - 180 scans
  - 2° angle step
  - 180 detectors
  - 180° Beam spread
  - No filter

**Image for Experiment**  
![image](https://github.com/user-attachments/assets/1856f045-6819-4bec-8c44-9eb953b5449c)  

### Number of Detectors

- Tested from 90 to 720 (step size of 90).
- Increased number of detectors improved image quality.
- MSE and visual inspection confirmed this trend.

**Image for 90**  
![image](https://github.com/user-attachments/assets/e5f53eee-cbbd-4c98-bf9c-1e16a9396da7)

**Image for 360**  
![image](https://github.com/user-attachments/assets/5f935098-5057-443e-a25a-686e502d30dc)

**Image for 720**  
![image](https://github.com/user-attachments/assets/ca788d69-81e2-47f6-b5c7-2462e66aee08)

**Chart**  
![image](https://github.com/user-attachments/assets/2805efb3-3ce5-4d6d-a57c-f2dc3cebe4ce)

### Number of Scans

- Tested from 90 to 720 scans.
- Significant improvement up to 360 scans; marginal improvement beyond that.

**Image for 90**  
![image](https://github.com/user-attachments/assets/efed8a8c-88c1-452e-8e7c-38c0f890da37)

**Image for 360**  
![image](https://github.com/user-attachments/assets/57679fd1-5bb9-4d07-ba15-ae1eac178c51)

**Image for 720**  
![image](https://github.com/user-attachments/assets/c5865681-cdaa-4ada-b74f-01013803a164)

**Chart**  
![image](https://github.com/user-attachments/assets/f409a9f0-d0b6-41da-82b8-53a7fbc99dbd)

### Beam Spread

- Tested from 45° to 270°.
- Highest visual quality was achieved with 180°.
- Wider spreads led to reduced reconstruction accuracy in the image center due to edge-focused ray distribution.

**Image for 45**  
![image](https://github.com/user-attachments/assets/7300b2ba-657f-4944-a9d4-e9a8bdf1b4ad)

**Image for 180**  
![image](https://github.com/user-attachments/assets/8efe8dcf-aafc-4f8c-83ba-d7a9d0ab1298)

**Image for 270**  
![image](https://github.com/user-attachments/assets/de63fc3d-b013-46a9-9af7-9092aa7720b1)

**Chart**  
![image](https://github.com/user-attachments/assets/f0a0dee8-d4ca-4751-a67b-05a94ce9a81b)

### Filter Usage

- **Parameters**:
  - 360 scans
  - 1° angle step
  - 360 detectors
  - 180° Beam spread 

- Filtering generally improved **visual** detail through contrast enhancement.
- However, filtered images occasionally scored worse in MSE due to higher pixel intensity variance.
- This discrepancy occurs because MSE penalizes high-contrast areas more heavily, even though they improve visual detail.

#### Test Case 1  

**Original image**   
![image](https://github.com/user-attachments/assets/5091bd9d-9e9d-4bfc-a99f-5c95649ead54)

**Reconstructed image without filter**  
![image](https://github.com/user-attachments/assets/fc857624-e217-4fc5-b74b-df5dd4ead7a0)

**Reconstructed image with filter**  
![image](https://github.com/user-attachments/assets/70f580e4-fc6d-4f7a-a1f8-a301e372044a)

**Chart**  
![image](https://github.com/user-attachments/assets/4e3b3f52-18b4-4467-98e1-17fe4dddf33a)

#### Test Case 2  

**Original image**  
![image](https://github.com/user-attachments/assets/d6a9e2d0-c480-4fdb-a22b-4668938175bb)

**Reconstructed image without filter**  
![image](https://github.com/user-attachments/assets/425e2185-209d-480a-8913-a31a3f35e0ce)

**Reconstructed image with filter**  
![image](https://github.com/user-attachments/assets/8c269e13-9b62-45ff-890a-6d2b478f50a0)

**Chart**  
![image](https://github.com/user-attachments/assets/5644b422-6992-4a9e-b807-d695e6cfb317)

## Observations

- Filtering often enhances subjective image quality by increasing contrast.
- However, it may degrade MSE due to higher edge sharpness and intensity changes.
- Optimal setup involves a balance between detector count, scan count, and beam spread.

## Conclusion

The CT scan simulator successfully replicates core CT reconstruction principles, including sinogram generation, filtering, and back-projection. 
It offers flexibility in experiment configuration and supports both visual and numerical image quality evaluation. 
DICOM integration broadens its applicability to real-world medical imaging workflows.
