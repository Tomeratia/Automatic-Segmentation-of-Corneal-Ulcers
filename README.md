# Automatic Segmentation of Corneal Ulcers (SUSTech-SYSU)

Segmentation of corneal ulcers using a U-Net style decoder with a ResNet34 encoder.
Project includes three experiments:
1) Train from scratch (no ROI)
2) Pretrained encoder (no ROI)
3) Pretrained + ROI (mask everything outside the cornea using corneaLabels)

## Repo structure
```
repo/
|-- data/
|   |-- rawImages/         # input images (jpg/png)
|   |-- ulcerLabels/       # ulcer masks (png)
|   |-- corneaLabels/      # cornea masks (png)
|   |-- outputs/
|       |-- dataset_index.csv
|       |-- *.pt           # saved checkpoints
|
|-- notebooks/
|   |-- EDA.ipynb          # dataset validation + visuals
|   |-- training.ipynb     # training + evaluation + plots
|
|-- src/                   # optional scripts (split/index creation)
|-- README.md

```

## How to run (Colab)
1) Mount Google Drive and `cd` into the project folder.
2) Ensure `data/outputs/dataset_index.csv` exists.
3) Run `notebooks/training.ipynb` to train and compare all 3 experiments.

## Test results
| Method | Test Dice | Test IoU |
|---|---:|---:|
| Scratch (no ROI) | 0.6381 | 0.5364 |
| Pretrained (no ROI) | 0.6870 | 0.5817 |
| Pretrained + ROI | 0.7442 | 0.6429 |

## Notes
- Loss: 0.5 * BCEWithLogits + 0.5 * Dice loss
- Metrics: Dice, IoU
- ROI here means masking outside the cornea (not crop), using corneaLabels.
