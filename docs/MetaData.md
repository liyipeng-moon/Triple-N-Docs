# MetaData about each session

We have some meta-data about each session, mainly 

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