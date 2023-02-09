Segmentation of Intraprostate Gold Fiducial Markers from Quantitative Susceptibility Mapping (OSM)

# Flow of data
The available data must first be processed through two notebooks. Before running the notebooks, directories for the results need to be created first. TorchIO needs to be installed before running the notebooks. It will be installed as a dependency when installing `fastMONAI`.

## mask-image.ipynb
This notebook mask the images in `ImgTr` directory with masks in the  `maskTr` directory. This notebook also combines the different images such as QSM, T2*map, and Magnitude into one image that can be used in training/inference.

## adjust-labels.ipynb
This notebook adjusts the labels in the `labelsTr` directory to remove the original prostate tissue segmentation, and also create a FM-only segmentation label file for training. To simplify the model training, we are only using the flattened labels in `labelsTrGm`.

## Source Data directory structure

```
bidsmonai-data
│ 
├── ImgTr
│   │   # imaging data from extra_data, qsm, t2starmap, and magnitude combined
│   ├── ...
│   ├── sub-z3278008_ses-20211109_run-01_magnitude_combined.nii.gz
│   ├── sub-z3278008_ses-20211109_run-01_qsm-even-echoes.nii
│   └── sub-z3278008_ses-20211109_run-01_t2starmap.nii.gz
├── labelsTr
│   │   # ground truth clean segmentation/label
│   ├── ...
│   └── sub-z3278008_ses-20211109_run-01_segmentation_clean.nii.gz
├── maskTr
│   │   # segmentation mask of the prostate area
│   ├── ...
│   └── sub-z3278008_ses-20211109_run-01_prostate-manual-seg.nii.gz
│   # Directories below need to be created before running adjust-labels and mask-image
├── ImgTrCmb
├── ImgTrCmbMag
├── ImgTrMsk
├── ImgTrMskCmb
├── ImgTrMskCmbMag
├── labelsTrGm
└── labelsTrGmCl
```

# Training notebook
`fastMONAI` and its requirements are needed to be installed before running the training notebook.

You can directly run the notebook to train a model.
