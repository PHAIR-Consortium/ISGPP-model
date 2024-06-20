# Model Weights for the ISGPP model for the segmentation of Pancreatic Ductal Adenocarcinoma (PDAC) after neoadjuvant therapy

## Overview

NOTE: THE PUBLICATION ACCOMPANYING THIS MODEL IS NOT YET PUBLISHED.

This repository contains the model weights for the ISGPP segmentation model, which segments cancer tissue in whole slide images of H&E sections from PDAC samples after neoadjuvant therapy. This model is described in the following publication (UPCOMING).

Please cite this paper if you are using the ISGPP model for your research.

## Model Architecture
The model is based on a U-net with a densenet161 encoder. The model was defined in the segmentation-models for PyTorch library (https://pypi.org/project/segmentation-models-pytorch/).

## Training Data
For training, 528 digitized histopathological whole slide images (hematoxylin & eosin staining) from resected pancreatic cancer specimen from 14 centers in 7 countries in Europe, North America, Australia, and Asia were included. Four different scanner types were used: Philips, Hamamatsu, 3DHistech and Leica. More details about the dataset and model training can be found in our publication: (UPCOMING) Am J Surg Pathol (2024). 

## Training Procedure
The model was trained using binary-cross-entropy-loss with ADAM optimizer for 40 epochs. The learning rate was set to 0.0001, and a learning rate decay every 5 epochs. 

## Model Performance
The meta-analysis of the cross-validations showed a mean F1 score of 0.78 (0.71 – 0.84). 

## Usage Instructions

Size inputpatches: 512 x 512 x 3
Resolution inputpatches: 0.5px/micron  
Normalize inputpatches using: torch.transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))

Example code for loading the model:

```python
import torch
import segmentation_models_pytorch as smp

# Model definition
aux_params = dict(pooling='max', classes=5)
model = smp.Unet("densenet161", classes=5, aux_params=aux_params)

# Load model weights
model.load_state_dict(torch.load("checkpoint.pt"))
model.eval()

# example inference
pred, _ = model(image_loader(patch))


```

output:
Class 0: background
class 1: Normal ducts
Class 2: Cancer ducts
Class 3: residual parenchyma
Class 4: fat


For more information:
Boris Janssen (b.v.janssen@amsterdamumc.nl) or Onno de Boer (o.j.deboer@amsterdamumc.nl)
