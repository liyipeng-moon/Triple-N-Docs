# Raw Data Structure and Preprocessing

The raw data are saved at `'xxx'`, with each session organized by recording day and session index(if one day with multiple sessions). Within each session folder, there are:

- **kilosort_def_5block_97** – Contains the output of Kilosort 4  
- **LFPprep** – Contains the preprocessed LFP signals  
- **NPX_XXDDDDDD…** – `XX` corresponds to the subject name, and `DDDDDD` corresponds to the recording day  
- **processed** – Contains processed data and converted files  
- One `.bhv` file – Recorded with MonkeyLogic (ML) software

---

## **NPX_ folder contents**

The `NPX_` folder, recorded with SpikeGLX, contains multiple files organized into three streams. Each stream includes a `.bin` file and its corresponding `.meta` file, which stores metadata such as sampling rate and gain.  

- **Streams:**
  1. **ap** – Active potential (spike) data  
  2. **lf** – Local field potential (LFP) data  
  3. **ni** – Additional task-related inputs (named `ni` because the data are recorded via a National Instruments card), such as event codes sent from the stimulus computer to the electrophysiology computer, and analog input from the photodiode.

---

## **.bhv file**

- Recorded with MonkeyLogic (ML) software  
- Can be loaded using the `mlread` function provided by ML, for convenience, a converted `.mat` version is also provided in the `processed` folder

## **processed**

- Within each processed folder, there are: