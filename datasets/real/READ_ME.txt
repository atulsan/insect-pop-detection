Overview

This dataset contains 92 high-resolution images of insects with detailed segmentation masks, bounding boxes, and order-level classifications (Coleoptera, Diptera, Aranea, etc.). 

There are approximately 3,109 annotated insects in total.

Folder Structure

DTRAB_Insect_Dataset/
│
├── images/                  # The 92 physical, high-resolution images
│
└── labels/
    └── labels.json          # The master Label Studio Native JSON file

Data Format Notes

The image strings inside the JSON contain URL encoding (e.g., %5C for backslashes) and local directory paths. They will need to be decoded and stripped to match the exact physical filenames in the images/ folder.

