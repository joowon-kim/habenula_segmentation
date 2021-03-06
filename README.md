# Habenula Segmentation
---
Semi-automated Human Habenula Segmentation Program

---
## Requirements
* Python: version 2.7
* Python libraries: numpy, scipy

---
## Input Files
* Currently, only nifti1 is the only supported file format.
* AC-PC aligned T1w image
* T2w image that is registered to T1w image
* Myelin map: T1w/T2w which can be generated using fslmaths in FSL: `fslmaths T1w -div T2w Myelin`
* Habenula center positions: a nifti1 file containing two markers - a voxel in the right habenula as 1 and a vxoel in the left habenula as 2
* Note: The PreFreeSurfer in Human Connectome Project (HCP) Pipelines (https://github.com/Washington-University/Pipelines) is  recommended for the AC-PC alignment and T2w-to-T1w registration.

---
## How to Run
```
import segment
segment.segment_hb(
        'T1w_filename',
        'T2w_filename',
        'myelin_filename',
        'hb_center_filename',
        'output_filename',
        min_volume = 80,
        t1min = None,
        t1max = None,
        t2min = 10,
        t2max = None,
        sig_factor = 0.9,
        growth = 5,
        verbose = False,
        return_volume=True,
        return_step_volume=False,
        return_center_of_mass=False,
        return_hb_index=False,
        return_hb_neighbor_index=False
        )
```

### input:
*  t1, t2, myelin: T1w, T2w, Myelin Nifti1 images
*  hb_center: mask Nifti1 file indicating Hb centers (1: right Hb, 2: left Hb)

### output:
*  out_filename: output (segmentation) Nifti1 image file name

### parameters:
*  min_volume: minimum ROI volume (mm^3) for each Hb. Default 80.
*  t1min, t1max, t2min, t2max: first thresold values for T1w, T2w.
*  sig_factor: Factor of sigma for myelin threshold for Hb segmentation. Default 0.9. The higher factor, the smaller Hb.
*  growth: Number of iteration for region growth method. 0 for disable it. Default 5.
*  verbose: If True, Display details. Default False.

### return:
*  [color1 Hb volume, color2 Hb volume], [color1 Hb partial volume, color2 Hb partial volume], [list(left Hb index), list(right Hb index)]

Reference: http://www.ncbi.nlm.nih.gov/pubmed/26826517

THIS PAGE IS UNDER CONSTRUCTION
