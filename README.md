# Zhuang Dialect Analysis

## Project Overview
This project applies MIR techniques to analyze tonal variation between Du'an and Wuming Zhuang dialects.

### Roadmap
* **Phase 1 (Feb):** Visualization & Filtering. Build a notebook to inspect waveforms/spectrograms by speaker and tone.
* **Phase 2 (Mar):** Quantitative Analysis. Implement DTW (Dynamic Time Warping) and clustering to measure inter-dialect distance and tonal stability.

## Data Setup
The data for this project is hosted on Google Drive in the `Zhuang` folder. The primary metadata file is `FileInfoForRIPA.csv`.
Description of attributes in the metadata file:
Note all words are one syllable and take the form CV(C).
Filename format: All .wav files and associated text annotations (.TextGrid) are named according to this format: AABB_C_DDD_E
  where AA = the dialect code: either 'DZ' or 'WZ',
    BB == speaker number, sequenced from 01 to 15, independent of dialect
    C = dictionary tone for the token (there are 10 tones, numbered 0 to 9; NA means dictionary tone is unknown)
    DDD = Word ID (from 1 to 197)
    E = repetition number (from 1 to 5 usually; with a few specific words repeated up to 15 times)
DictionaryIPA: The IPA form given by our dictionary source, with tone number appended at the end
DictionaryTone: The word's tone according to the dictionary (NOTE: we used a different convention from the original dictionary)
VowelLength: The vowel length according to the dictionary
IPA: Same as DictionaryIPA but removed ambiguities (some dictionary words could correspond to more than one possible IPA output; we chose the actual output manually in this column)
Coda: The final consonant type (coda) according to the dictionary. Takes 4 values: ('obstruent', 'nasal', 'nocoda', or NA for words with 2 syllables or those not in the dictionary)
ReclassifiedTone: The word's tone according to expert classification (the three co-authors); same as DictionaryTone in most cases
ReclassifiedVowelLength: The word's vowel length according to expert classification (the three co-authors); same as VowelLength in most cases
VowelQuality: The vowel in IPA according to the dictionary
PhonemicIPA: IPA for the actual word produced as classified by the first author, using only phonemes known to exist in sources on the language
ReclassifiedIPA: IPA for the actual word produced as classified by the first author, with narrow phonetic transcription, capturing variations
ReclassifiedCoda: The final consonant type (coda) according to expert classifiction (the first author); same as Coda in most cases
Exclude: Filter for data exclusion in analysis; levels encode the reason for exclusion:
  2S: There are two syllables, rather than one syllable.
  Exclude (Mandarin): The word was identified as a Mandarin Chinese word (by native Mandarin speakers), not a Zhuang word
  Exclude Item: There was no internal consistency for a given speaker in producing the same word for each repetition (fewer than 4 tokens in agreement); all tokens of the word are marked
  Exclude Token: The token is not consistent with the majority of other tokens for this word by this speaker and should be excluded.
  Extra: More than the usual five repetitions were recorded for this word by this speaker; only the first five are kept; others are marked "Extra"
  Keep: This token is kept in the data set.
  Octave Error: F0 profile has discontinuities indicative of an octave error in the STRAIGHT algorithm
  Short Duration: The vowel's duration doesn't contain enough samples to reliably measure f0
  Skipped: The audio file doesn't exist because the speaker did not know the Zhuang word corresponding to the Chinese word shown on screen and elected to skip the stimulus
  Straight Error: The STRAIGHT algorithm to measure f0 failed or gave an error
DictionaryMatch: Binary (yes/no) filter for data exclusion that can be applied if we only want those tokens we are sure match the intended dictionary form
Onset: The initial consonant (onset) according to the first author (corresponding to ReclassifiedIPA)
OnsType: Onset consonant grouped by place of voicing & manner, useful for analysis (onset type can affect f0 locally)

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
