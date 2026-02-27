# Zhuang Dialect Analysis

## Project Overview
This project applies MIR techniques to analyze tonal variation between Du'an and Wuming Zhuang dialects.

### Roadmap
* **Phase 0 (finished) (Basic):** Set up this repository.
* **Phase 1 (early March) (Expected):** Visualization & Filtering. Build a notebook (the deliverable) to inspect waveforms/spectrograms by speaker and tone.
* **Phase 2 (late March) (Advanced):** Quantitative Analysis. Implement DTW (Dynamic Time Warping) and clustering to measure inter-dialect distance and tonal stability.

## Data Setup
The data for this project is hosted on Google Drive in the `Zhuang` folder. The primary metadata file is `FileInfoForRIPA.csv`.

> **Data Dictionary:** For a detailed explanation of the filename formats, metadata attributes, and exclusion criteria, please see [metadataDetails.md](metadataDetails.md).

> **Linguistic Article on Zhuang:** JIPA_DZArticle.pdf was published in 2025 on the tonal system in one of the two dialects (DZ). It outlines the tone system and how f0 contour and duration are involved in both the tone contrasts and also in a vowel length contrast. The statistical analysis was done in R with the script and data file available on GitHub here: https://github.com/jerperkins/DZData.

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
