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
|   |-- dataset_url   - link to download the dataset
|   |-- outputs/
|       |-- A_scratch_noROI_best.pt
|       |-- B_pretrained_noROI_best.pt
|       |-- C_pretrained_ROI_best.pt
|       |-- dataset_index.csv
|       |-- train_ids.txt
|       |-- val_ids.txt
|       |-- test_ids.txt

|   |-- outputs/
|       |-- A_scratch_noROI_best.pt        - best model trained from scratch
|       |-- B_pretrained_noROI_best.pt     - best pretrained model (no ROI)
|       |-- C_pretrained_ROI_best.pt       - best pretrained model with ROI
|       |
|       |-- dataset_index.csv              - dataset split index
|       |-- train_ids.txt                  - training image IDs
|       |-- val_ids.txt                    - validation image IDs
|       |-- test_ids.txt                   - test image IDs

|-- notebooks/
|   |-- EDA.ipynb          # dataset validation + visuals
|   |-- training.ipynb     # training + evaluation + plots
|
|-- src
|   |-- build_dataset_index.py  - builds dataset index and data splits
|        
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
