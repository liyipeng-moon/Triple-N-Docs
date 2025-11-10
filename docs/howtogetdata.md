# Download Data

Our raw data are hosted on Science Data Bank and can be accessed via the following (temporary) link. You may download individual files directly through your browser, or use FTP (e.g., FileZilla) for batch downloading. Hostname, port, and login information are provided in the **Data File Download** panel on the platform.

[**Triple-N Dataset at Science Data Bank**](https://www.scidb.cn/en/)

### Raw Session Folder
Due to the platform's file number limitations, each session folder has been compressed into a `.tar.gz` archive. For example:  
```
    Example files:  
    /Raw/SesFolder/240629.tar.gz
```

### Raw GoodSUnit
In our analysis pipeline, spiking data are stored in the *GoodUnit* files. You can download the sessions and directly load these files in MATLAB to inspect processed spike waveforms, raster data, and PSTHs.  
A detailed description is provided in the **ProcessedFiles** section.  
```
    Example files:  
    Raw/GoodStruct/GoodUnit_YYMMDD_Subject_NSD1000_LOC_gx.mat
```  

### Raw H5 and info.mat
For figure generation in the NNN paper, the GoodUnit files were converted into `.h5` format for faster loading, with additional metadata saved in corresponding `*_info.mat` files. Instructions for working with these files can be found in the **code** section.

```
    Example files:  
    **Raw/H5FILES/ses01_240629_M1_2.h5**  
    **Raw/H5FILES/ses01_240629_M1_2_info.mat**
```