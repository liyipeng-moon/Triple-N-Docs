# Raw Data Structure and Preprocessing

The raw data are saved at `/Raw`, with each session organized by recording day and session index (if one day with multiple sessions).  
Raw session folder are compressed into a tar.gz file dur to limitations of the platform. You can extract them by tools like 7-zip.
  
Within each session folder, there are:

- **NPX_XXDDDDDD_exp_gx Folder** – Raw electrophysiology data recorded using SpikeGLX, with XX denotes the subject name and DDDDDD denotes the recording date.
- **.bhv file** – Behabioral data recorded with MonkeyLogic (ML) software  
- **kilosort_def_5block_97** – Contains the output of Kilosort4  
- **LFPprep** – Contains the preprocessed LFP signals  
- **processed** – Processed and converted data formats for downstream analyses.

---

## **NPX_ folder contents**
The `NPX_` directory contains the raw neuronal signal recordings acquired using SpikeGLX, separated into three data streams. Each stream consists of a `.bin` file and a corresponding `.meta` file that stores acquisition metadata (e.g., sampling rate, gain, channel map).

**Streams:**  
  1. **ap** – Active potential (spike) datam, ~30 kHz sampling.  
  2. **lf** – Local field potential (LFP) data, 2.5 kHz.  
  3. **ni** – Auxiliary task-related inputs (~10 kHz), recorded via a National Instruments card PXI6341, such as event codes sent from the stimulus computer, and analog input from the photodiode. Sampling at 10000Hz.  

**Inspecting Neuropixel Data**  
You can download SpileGLX [here](https://billkarsh.github.io/SpikeGLX/App/Release_v20250915-api4.zip), and direct open the `.bin` file with `Open File Viewer`. Detailed info can be found [here](https://billkarsh.github.io/SpikeGLX/Sgl_help/UserManual.html#offline-file-viewer). If you don't have a NI drive in your PC, you need to use `SpikeGLX_NISiM.exe` instead of `SpikeGLX.exe`

---

## **.bhv file**

- Recorded with MonkeyLogic (ML) software, containing stimuli order, eye position, reward time..  
- Can be loaded using the `mlread` function provided by ML, for convenience, a converted `.mat` version is also provided in the `processed` folder
- When loaded into MATLAB, the data are stored as a structure indexed by ML trial. Note that multiple stimulus onsets (Stimulus Trials) occur within a single ML Trial.
- Official document of bhv file can be found [here](https://monkeylogic.nimh.nih.gov/docs_GettingStarted.html#FormatsSupported).

## **processed**

- Within each processed folder, there are:
1. **BC** – A Folder containing result of quality metric computed by [BombCell](https://github.com/Julie-Fabre/bombcell).
2. **fscale.mat** - A scaling factor transform int16 value into microvolt.
3. **ML_YYMMDD_Subject_.mat** – Converted MonkeyLogic bhv file into mat.
4. **META_YYMMDD_Subject_NSD1000_LOC** – Metadata about trial order, image onset time, eye monitor data and metadata from SpikeGLX .meta file. This file is the output of preprocessing script step1.
5. **GoodUnitRaw_YYMMDD_Subject_NSD1000_LOC.mat** - The raw spike time, quality metric and necessary meta data. This file is the output of preprocessing script step2.
6. **GoodUnit_YYMMDD_Subject_NSD1000_LOC_g2** - Goodunit file, the output if preprocessing step3, you can find detailed info [here]().
7. **GoodLFP__YYMMDD_Subject_NSD1000_LOC_g2** - Processed file of local field potential data.
8. Some figure for quality accessment during pre-processing pipeline.