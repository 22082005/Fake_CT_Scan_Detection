FakeCTScanDetection
#Overview
The Fake CT Scan Detection System is a deep learning framework designed to identify forged or manipulated 3D CT medical images.
With the growing use of digital imaging and AI-based editing tools, there is an increasing threat of fake CT scans being used for fraudulent or unethical purposes.
This project aims to verify the authenticity of CT scans by detecting subtle artifacts introduced during image tampering.

The model uses a 3D EfficientNet-B3 architecture that can capture volumetric features and learn pixel-level inconsistencies that indicate manipulation.

#Objective
To build an automated system capable of distinguishing between authentic and tampered CT scans with high accuracy using deep learning.
The system focuses on identifying image irregularities that are not visible to the human eye, ensuring data reliability in medical imaging systems.

#Methodology
1)Dataset
A custom dataset was created since no public dataset for fake CT scans exists.
Authentic data: 1050 real 3D CT volumes collected from public medical repositories.
Fake data: 3636 synthetic forgeries generated using a patch-based splicing and blending process.
Each fake scan was created by taking a random patch from one CT volume and blending it into another using a spherical alpha mask to ensure smooth transitions.

2)Preprocessing
All volumes were processed as follows:
Conversion to Hounsfield Units (HU) and clipping within the range -1000 to 400.
Normalization to a [0, 1] scale for stable gradient updates.
Resizing to a fixed dimension of 96×96×96 voxels to handle memory efficiently.

3)Model Architecture
Model: 3D EfficientNet-B3 (adapted using the MONAI framework)
Loss Function: Binary Cross-Entropy with Logits
Optimizer: Adam (learning rate 5×10⁻⁵)
Scheduler: ReduceLROnPlateau
Training Epochs: 25 (with early stopping)
Batch Size: 2
Data augmentation was performed using 3D transformations such as random flips, affine transformations, Gaussian noise, blur, gamma correction, and bias field distortion to improve model generalization.

4)Results
The model achieved an overall accuracy of 98.93% on the validation dataset.

Metric	Value
Accuracy	98.93%
Precision	99.86%
Recall	98.76%
F1-Score	99.31%
The confusion matrix showed extremely low false positives, indicating that the model can reliably detect fake scans while minimizing incorrect classifications of real ones.

#Explainability
To ensure transparency, Grad-CAM visualization was applied to the trained model.
The activation heatmaps clearly localized manipulated regions in fake scans, while showing diffuse attention for real scans, confirming that the model learned genuine forensic features rather than spurious correlations.

#Conclusion
The project demonstrates that 3D CNNs, specifically EfficientNet-B3, can effectively detect tampered CT scans with high precision.
It establishes a baseline for future research in medical image forensics and helps protect against data manipulation in clinical environments.
Future work includes expanding the dataset to cover GAN-generated forgeries, adapting the model for other modalities such as MRI and PET, and developing a lightweight version that can be integrated into hospital PACS systems for real-time fraud detection.
