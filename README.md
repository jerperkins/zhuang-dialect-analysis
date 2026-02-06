# Zhuang Dialect Analysis

## Project Overview
This project applies MIR techniques to analyze tonal variation between Du'an and Wuming Zhuang dialects.

### Roadmap
* **Phase 1 (Feb):** Visualization & Filtering. Build a notebook (the deliverable) to inspect waveforms/spectrograms by speaker and tone.
* **Phase 2 (Mar):** Quantitative Analysis. Implement DTW (Dynamic Time Warping) and clustering to measure inter-dialect distance and tonal stability.

## Data Setup
The data for this project is hosted on Google Drive in the `Zhuang` folder. The primary metadata file is `FileInfoForRIPA.csv`.

> **Data Dictionary:** For a detailed explanation of the filename formats, metadata attributes, and exclusion criteria, please see [metadataDetails.md](metadataDetails.md).

### How to Access Data in Colab
To run the notebooks in this repository, you must mount the project Google Drive. Use the following code snippet at the start of your notebook:

```python
from google.colab import drive
import os

# Mount the drive
drive.mount('/content/drive')

# Verify the file is accessible
file_path = '/content/drive/MyDrive/Zhuang/FileInfoForRIPA.csv'
if os.path.exists(file_path):
    print("✅ Data found!")
else:
    print("❌ Data not found. Please ensure the Zhuang folder is in 'MyDrive'.")
