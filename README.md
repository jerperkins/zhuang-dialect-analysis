# Zhuang Dialect Analysis

## Project Overview
This project applies MIR techniques to analyze tonal variation between Du'an and Wuming Zhuang dialects.

### Roadmap
* **Phase 1 (Feb):** Visualization & Filtering. Build a notebook to inspect waveforms/spectrograms by speaker and tone.
* **Phase 2 (Mar):** Quantitative Analysis. Implement DTW (Dynamic Time Warping) and clustering to measure inter-dialect distance and tonal stability.

## Data Setup
The data for this project is hosted on Google Drive in the `Zhuang` folder. The primary metadata file is `FileInfoForRIPA.csv`.

> **Note:** All words in the dataset are one syllable and take the form CV(C).

### Filename Format
All `.wav` files and associated text annotations (`.TextGrid`) are named according to the format: `AABB_C_DDD_E`

* **AA:** The dialect code (either `DZ` or `WZ`)
* **BB:** Speaker number (sequenced `01` to `15`, independent of dialect)
* **C:** Dictionary tone for the token (`0` to `9`; `NA` means dictionary tone is unknown)
* **DDD:** Word ID (`1` to `197`)
* **E:** Repetition number (usually `1` to `5`; specific words repeated up to `15` times)

### Metadata Attributes (`FileInfoForRIPA.csv`)

| Attribute | Description |
| :--- | :--- |
| **DictionaryIPA** | The IPA form given by our dictionary source, with tone number appended at the end. |
| **DictionaryTone** | The word's tone according to the dictionary. *(Note: Convention differs from original dictionary).* |
| **VowelLength** | The vowel length according to the dictionary. |
| **IPA** | Same as *DictionaryIPA* but with ambiguities removed (manually selected actual output). |
| **Coda** | Final consonant type according to dictionary (`obstruent`, `nasal`, `nocoda`, or `NA`). |
| **ReclassifiedTone** | Tone according to expert classification; usually matches *DictionaryTone*. |
| **ReclassifiedVowelLength** | Vowel length according to expert classification; usually matches *VowelLength*. |
| **VowelQuality** | The vowel in IPA according to the dictionary. |
| **PhonemicIPA** | IPA for the actual word produced as classified by the first author (using known phonemes). |
| **ReclassifiedIPA** | IPA for the actual word produced as classified by the first author (narrow transcription capturing variations). |
| **ReclassifiedCoda** | Final consonant type according to expert classification; usually matches *Coda*. |
| **DictionaryMatch** | Binary (`yes`/`no`) filter. Use to select tokens that definitely match the intended dictionary form. |
| **Onset** | The initial consonant according to the first author (corresponding to *ReclassifiedIPA*). |
| **OnsType** | Onset consonant grouped by place of voicing & manner (useful for f0 analysis). |

### Exclusion Criteria (`Exclude` Column)
Levels encode the reason for data exclusion:

* **2S:** There are two syllables rather than one.
* **Exclude (Mandarin):** Identified as a Mandarin Chinese word by native speakers, not a Zhuang word.
* **Exclude Item:** No internal consistency for a given speaker (fewer than 4 tokens in agreement). All tokens marked.
* **Exclude Token:** Token is inconsistent with the majority of other tokens for this word by this speaker.
* **Extra:** Only the first five repetitions are kept; subsequent repetitions are marked "Extra".
* **Keep:** This token is valid and kept in the dataset.
* **Octave Error:** F0 profile has discontinuities indicative of an octave error in the STRAIGHT algorithm.
* **Short Duration:** Vowel duration is insufficient to reliably measure f0.
* **Skipped:** Audio file does not exist (speaker did not know the word and skipped the stimulus).
* **Straight Error:** The STRAIGHT algorithm failed or gave an error.
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
