# Raw Data Structure and Preprocessing

The raw data are saved at `'xxx'`, with each session organized by recording day and session index(if one day with multiple sessions). Within each session folder, there are:

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

---

## **.bhv file**

- Recorded with MonkeyLogic (ML) software, containing stimuli order, eye position, reward time..  
- Can be loaded using the `mlread` function provided by ML, for convenience, a converted `.mat` version is also provided in the `processed` folder
- When loaded into MATLAB, the data are stored as a structure indexed by ML trial. Note that multiple stimulus onsets (Stimulus Trials) occur within a single ML Trial.

## **processed**

- Within each processed folder, there are: