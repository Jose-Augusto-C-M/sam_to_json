## A Python package to segmenting image data with the Segment Anything Model (SAM) and export to labelme json format

# Introduction

The basis for the idea of project involves SAM: https://github.com/facebookresearch/segment-anything, and labelme: https://github.com/wkentaro/labelme. The Segment Anything Model (SAM) produces high quality object masks from input prompts such as points or boxes, and it can be used to generate masks for a great diversity of objects and data in an image. Labelme is a graphical image annotation tool inspired by http://labelme.csail.mit.edu. It is written in Python and uses Qt for its graphical interface.


The code requires python>=3.9, as well as pytorch>=1.7 and torchvision>=0.8. Installing both PyTorch and TorchVision with CUDA support is strongly recommended.

# Features

With SAM

Create foreground and background markers interactively
Save segmentation results as vector format (JSON)

With labelme

Image annotation for polygon, rectangle, circle, line and point. 
Posterior annotation edition for classification and cleaning.
Exporting VOC-format dataset for semantic/instance segmentation.
Exporting COCO-format dataset for instance segmentation.


# Getting Started
Minimun requirements:

Ubuntu 20.04
Python3.9
20 GB RAM
12 GB GPU RAM

Download the repository to a folder and get inside the folder

Create and install dependencies in a new environment by running

```python
conda create --name=samjson python=3
source activate samjson
pip install -r requirements.txt
```

# Usage

Run one of the following code chaging the path to files inside the scripts

More than one image: https://github.com/Jose-Augusto-C-M/sam_to_json/blob/master/Many_images.ipynb


Single image: https://github.com/Jose-Augusto-C-M/sam_to_json/blob/master/Single_image.ipynb

Inside the scripts there are ploting tools for analisys of the proposed mask

The part of the code that creates the mask is:

```python
mask_generator_ = SamAutomaticMaskGenerator(
    model=sam,
    points_per_side=20,
    pred_iou_thresh=0.95,     
    stability_score_thresh=0.95,
    crop_n_layers=1,
    crop_n_points_downscale_factor=2,
    min_mask_region_area=300,  
)
```

provide the tuning parameters for the created masks, if the mask is adequated, you follow the code and execute:

```python
import json

# Define o nome do arquivo .json que será criado
filename = "output.json"

# Define o número de labels a serem geradas
num_labels = len(masks)

# Cria uma lista vazia para armazenar as informações dos labels
labels = []

for i in range(len(masks)):
    shapes = from_binary_image(masks[i]['segmentation'].astype(np.uint8), simplify_tolerance=2)
    for shape in shapes:
                
        # Define o nome do label com base no valor de i
        label_name = f"label_{i}"

        # Define os pontos para o label com base no valor de i
        # pontos_array = class_points
        aux_pontos = [list(t) for t in shape.exterior.coords[:]]
        points = []
        for ponto in aux_pontos:
            points.append([ponto[1], ponto[0]])
        
        # Define as informações do label
        label_info = {
            "label": label_name,
            "points": points,
            "group_id": None,
            "description": "",
            "shape_type": "polygon",
            "flags": {}
        }

        # Adiciona o label à lista de labels
        labels.append(label_info)


# Define as informações adicionais do arquivo
info = {
    "version": "5.2.0.post4",
    "flags": {},
    "shapes": labels,
    "imagePath": path_image_i,
    "imageData": None,
}
        
# Cria o arquivo .json e adiciona as informações
with open(filename, 'w') as outfile:
    
    json.dump(info, outfile)
```

That will create the json file(s). After this procedure, execute labelme and load the json and make the necessary edition to the masks.






