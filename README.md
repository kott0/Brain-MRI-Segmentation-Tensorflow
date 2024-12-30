# Brain-MRI-Segmentation-Tensorflow
Brain MRI segmentation is a crucial step in medical imaging analysis. The U-Net model is widely used for such tasks due to its encoder-decoder structure that effectively captures spatial and contextual information. This project leverages a U-Net model for brain MRI segmentation.

### Model Architecture
The U-Net model consists of:
* Encoder:
  * Series of convolutional layers for feature extraction.
  * Max pooling layers for downsampling.
* Decoder:
  * Transposed convolution layers for upsampling.
  * Skip connections from encoder layers for retaining spatial information.
* Output:
  * A 1-channel output map with a sigmoid activation function for pixel-wise binary segmentation.

### Implementation Steps
1. Data Preparation
  * Data is loaded and split into training, validation, and test sets using train_test_split.
  * Data augmentation is applied to the training set using Keras ImageDataGenerator.
2. Loss and Metrics
  * Dice Coefficient: Measures overlap between predicted and true masks.
  * Binary Cross-Entropy with dice loss: Combines BCE loss and dice coefficient for robust segmentation.
3. Training
  * The model is trained for 150 epochs using the Adam optimizer and a batch size of 16.
  * Callbacks like ModelCheckpoint, ReduceLROnPlateau, and EarlyStopping improve training efficiency.
4. Evaluation
  * Besides performance evaluation using IoU and dice coefficient, I decided to visualize predictions against ground truth masks.
    
### Requirements
* pip install -r requirements.txt
* Paste the data to `source_data` folder.

### 

---
#### LGG Segmentation Dataset
Data source: Brain MRI segmentation, https://www.kaggle.com/mateuszbuda/lgg-mri-segmentation

This dataset contains brain MR images together with manual FLAIR abnormality segmentation masks.
The images were obtained from The Cancer Imaging Archive (TCIA).
They correspond to 110 patients included in The Cancer Genome Atlas (TCGA) lower-grade glioma collection with at least fluid-attenuated inversion recovery (FLAIR) sequence and genomic cluster data available.
Tumor genomic clusters and patient data is provided in `data.csv` file.

All images are provided in `.tif` format with 3 channels per image.
For 101 cases, 3 sequences are available, i.e. pre-contrast, FLAIR, post-contrast (in this order of channels).
For 9 cases, post-contrast sequence is missing and for 6 cases, pre-contrast sequence is missing.
Missing sequences are replaced with FLAIR sequence to make all images 3-channel.
Masks are binary, 1-channel images.
They segment FLAIR abnormality present in the FLAIR sequence (available for all cases).

The dataset is organized into 110 folders named after case ID that contains information about source institution.
Each folder contains MR images with the following naming convention:

`TCGA_<institution-code>_<patient-id>_<slice-number>.tif`

Corresponding masks have a `_mask` suffix.
