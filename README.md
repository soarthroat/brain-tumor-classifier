# Brain Tumor Classifier

Classifies brain MRI slices as glioma, meningioma, or pituitary tumor,
using a patient-level data split and heatmaps that show what the model looks at.

**Status:** in progress

## Dataset

Brain tumor dataset by Jun Cheng (Southern Medical University, Guangzhou, China):
3,064 T1-weighted contrast-enhanced MRI slices from 233 patients
(meningioma, glioma, pituitary tumor).

- Source: https://figshare.com/articles/dataset/brain_tumor_dataset/1512427
- DOI: 10.6084/m9.figshare.1512427
- License: CC BY 4.0 (confirm on the figshare page)
- The data is not included in this repository. Download it from figshare.

Citation: Cheng, J. (2017). brain tumor dataset. figshare.
https://doi.org/10.6084/m9.figshare.1512427

## Results (baseline: pretrained ResNet-18)

Patient-level split (no patient appears in more than one split):
187 / 23 / 23 patients, 2,449 / 365 / 250 slices (train / val / test).
Settings: 224x224 input, Adam (lr 1e-4), 8 epochs, flip/rotation augmentation.
The epoch with the best validation accuracy was kept, and the test set was evaluated once.

| | Slice accuracy | Patient-level accuracy |
|---|---|---|
| Validation | 95.1% | 95.7% (23 patients) |
| Test | 94.0% (95% interval 86.9-99.0%) | 87.0% (20 of 23 patients) |

Test set per class:

| Class | Precision | Recall | F1 |
|---|---|---|---|
| Meningioma | 0.892 | 0.767 | 0.825 |
| Glioma | 0.963 | 0.954 | 0.958 |
| Pituitary | 0.934 | 1.000 | 0.966 |

Limitations: each split has only about 23 patients, so results are uncertain.
Glioma slices from patients with numeric IDs (22 of 89 glioma patients) were
classified much less reliably than those with MR-prefixed IDs (61% vs 98% of
validation and test slices). The reason is not yet known.

**Disclaimer:** research demo, not for medical diagnosis.


