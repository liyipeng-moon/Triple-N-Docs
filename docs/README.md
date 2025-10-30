# Triple-N Dataset Documentation

Non-human Primate Neural Responses to Natural Scenes

Ref: https://www.biorxiv.org/content/10.1101/2025.05.06.652408v1
Contact: moonl@pku.edu.cn

This document is currently under development to ensure clarity and ease of understanding. Your feedback is invaluable—please feel free to raise an issue or email me with any suggestions or points needing clarification.

## File Structure
For each recording session, three file types are provided:

---

### 1. GoodUnit Files
Contains processed spike information and some meta-data.

**Example Filename**:  
`GoodUnit_240629_JianJian_NSD1000_LOC_g2.mat`

### Key File Contents
| Component | Description |
|-----------|-------------|
| `global_params.pre_onset` | Time (ms) prior to stimuli onset (here: 50) |
| `global_params.post_onset` | Time (ms) after stimuli onset (here: 400) |
| `global_params.PsthRange` | Time points  for raster and PSTH below <br> Here: -50:1:400 |
| `meta_data` | Recording metadata and processed behavior |
| `meta_data.trial_valid_idx` | Stimuli indices for each trial <br> - 0: failed trial <br>- 1-1000: NSD Shared 1000 <br> - 1001-1072: Localizer stimuli |
| `GoodUnitStrc` | Organized sturcture for each units |

### GoodUnitStrc Structure Key Field
| Field | Format | Description |
|-------|--------|-------------|
| `Raster` | [trial_idx × time_point] | Spike raster matrix <br> typically 0 1, where 1 is one spike <br> could be 2 or lager for some MUA |
| `response_matrix_img` | [image_idx × time_point] | PSTH matrix with a 20ms box bin |
| `qm` | [1 × n_metric] | Quality metric from BombCell |
| `spiketime_ms` | [1 × n_spikes] | Spike train time point relative to stimuli train |
| `waveform` | [7 Chan × 61 Sample] | Spike waveform |

note: `trial_idx` here correspond to all valid trials (i.e. `meta_data.trial_valid_idx(meta_data.trial_valid_idx~=0)`)

---

### 2. H5 Files
Better format for faster data access relative to matlab GoodUnitStrc. Fetch with matlab:
```
    h5read('xxx', '/field')
```

**Example Filename**:  
`ses01_240629_M1_2.h5`

### Contents
| Field | Format | Description |
|-------|--------|-------------|
| `raster_matrix_img` | [unit_num × trial_idx × time_point] | Same as GoodUnitStrc
 |
| `response_matrix_img` | [unit_num × image_idx × time_point] | Same as GoodUnitStrc |



---

## 3. Processed Files
Contains unit-wise processed information.

**Example Filename**:  
`Processed_ses01_240629_M1_2.mat`

### Key Variables
| Variable | Format | Description |
|----------|--------|-------------|
| `B_SI`, `F_SI`, `O_SI` | [1 × unit_num] | d-prime for body, face, object categories from localizer |
| `best_t_time` | [1 × unit_num] | Time window with highest reliability |
| `mean_psth` | [unit_num × time_point] | Averaged PSTH across images |
| `pos` | [1 × unit_num] | Spike position along the Electrode shank |
| `reliability_basic/best` | [1 × unit_num] | Split-half reliability <br> - basic: calculated from fixed time window <br> - best: calculated from best time window |
| `response_basic/best` | [unit_num × 1072] | Averaged firing rates  <br> - basic: calculated from fixed time window <br> - best: calculated from best time window |
| `snr`, `snr_max` | [1 × unit_num] | Signal-to-noise ratios <br> - max: calculated by most preferred stimuli|
| `UnitType` | [1 × unit_num] | Unit type from BombCell: <br>1: Single Unit<br>2: MUA<br>3-4: Non-somatic |

---

### ROI Definition File: `exclude_area.xls`
Contains manually defined Regions of Interest (ROIs) for each session.

- One row = one ROI
- Single session may contain multiple ROIs (e.g., session 11 has object area at tip + unknown areas)

### File Columns
| Column | Description | Example Values |
|--------|-------------|----------------|
| `SesIdx` | Session number | 11, 12, 13... |
| `y1` | ROI start position (shank coordinate) | 1200 (μm) |
| `y2` | ROI end position (shank coordinate) | 1800 (μm) |
| `arealabel` | Area Label | See full list below, with number corresponding to subject idx |
| `ROIIndex` | ROI identifier | Links to 3D coordinates in another file |

### Area Label Key
**Body Face Object**:
- `MB`: Middle body (MSB)
- `AB`: Anterior body (ASB)
- `MF`: Middle face (ML)
- `AF`: Anterior face (AL)
- `MO`: Middle object (MLO)
 - `MO1s1` and `MO1s2` correspond 2 subregions of MO1
- `AO`: Anterior object (ALO)

**Other Areas**:
- `LPP`: Lateral place patch
- `PITP`: Posterior inferotemporal place patch
- `CLC`: Central lateral color area
- `AMC`: Anterior medial color area

---

## Code

### script
code for analyze and generate figures in the paper

### demo code
not related to paper, just a going-through demo
 - demo1, generating single unit raster plot for several images
 - demo2, generating populational preference of interested ROI