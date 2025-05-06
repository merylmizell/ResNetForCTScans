Introduction

Intracranial hemorrhage (ICH) is a serious medical condition that requires fast and accurate diagnosis to prevent long-term damage or death. While CT scans are the current gold standard, manual interpretation can be time-consuming and inconsistent. My research leverages deep learning, specifically convolutional neural networks (CNNs), to automate and improve the identification and classification of ICH subtypes using the publicly available RSNA dataset.


Methods

  I processed over 147,000 DICOM-format CT images by:
  Converting them to PNG format.
  Extracting pixel values in Hounsfield Units (HU).
  Applying brain-specific windowing (center = 40 HU, width = 80 HU).
  Normalizing intensities to a [-1, 1] range.
  The dataset was then split into training, validation, and testing subsets. These steps ensured uniformity across input images and reduced preprocessing overhead during training.


Model Training & Evaluation

  I trained a multi-label CNN using a modified ResNet-152 architecture in PyTorch:
  Each CT image was resized to 224×224 and stacked into three channels.
  The model predicted five subtypes: subdural, epidural, subarachnoid, intraparenchymal, and intraventricular hemorrhages.
  We used sigmoid activation and Binary Cross-Entropy loss to support multi-label classification.
  Training used a grid search to optimize threshold cutoffs per class (ranging from 0.1 to 0.9) and focused on maximizing F1-score, especially to balance sensitivity and specificity.


Results

  The model achieved high accuracy overall, but performance varied across subtypes.
  Subdural and epidural hemorrhages were the most difficult to classify, with lower F1-scores.
  Confusion matrices show most false negatives occur in rare or visually similar hemorrhage types.
  A pixel intensity histogram (Figure 2) validated successful preprocessing and normalization.


Conclusion

  This work confirms the potential of deep learning in ICH classification, especially as a screening tool in time-sensitive clinical settings. However, performance differed by subtype, reflecting the challenges of distinguishing certain hemorrhages visually.

Key takeaways:

  CNNs can rapidly identify most hemorrhage types.
  Precision is lower for rare or visually similar subtypes.
  Better sampling, larger datasets, and customized loss functions could further improve results.


Future Directions

  To enhance clinical relevance and generalization:
  Balanced Sampling to reduce subtype imbalance.
  Data Augmentation to improve generalization to unseen variations.
  Model Refinement through custom CNN architectures or attention mechanisms.
