# Preparation of dependencies

The code requires python>=3.9, as well as pytorch>=1.7 and torchvision>=0.8. Installing both PyTorch and TorchVision with CUDA support is strongly recommended.

The basis for the idea of project involves SAM: https://github.com/facebookresearch/segment-anything, and labelme: https://github.com/wkentaro/labelme. The Segment Anything Model (SAM) produces high quality object masks from input prompts such as points or boxes, and it can be used to generate masks for all objects in an image. It has been trained on a dataset of 11 million images and 1.1 billion masks, and has strong zero-shot performance on a variety of segmentation tasks. Labelme is a graphical image annotation tool inspired by http://labelme.csail.mit.edu. It is written in Python and uses Qt for its graphical interface.

Requirements
Ubuntu / macOS / Windows
Python3.9
PyQt5 / PySide2

# Environment setup:

#python3
conda create --name=sam_to_json python=3.9
source activate sam_to_json

# SAM instalation:

pip install git+https://github.com/facebookresearch/segment-anything.git
or clone the repository locally and install with

git clone git@github.com:facebookresearch/segment-anything.git
cd segment-anything; pip install -e .

To load SAM download the description from the official SAM repository: https://github.com/facebookresearch/segment-anything/tree/main#model-checkpoints

Model Checkpoints
Three model versions of the model are available with different backbone sizes. These models can be instantiated by running

from segment_anything import sam_model_registry
sam = sam_model_registry["<model_type>"](checkpoint="<path/to/checkpoint>")
Click the links below to download the checkpoint for the corresponding model type.

default or vit_h: ViT-H SAM model. https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth
vit_l: ViT-L SAM model. https://dl.fbaipublicfiles.com/segment_anything/sam_vit_l_0b3195.pth
vit_b: ViT-B SAM model. https://dl.fbaipublicfiles.com/segment_anything/sam_vit_b_01ec64.pth

To see and edit the .json labels you can use labelme

# labelme instalation: 

#conda install -c conda-forge pyside2
#conda install pyqt
#pip install pyqt5  # pyqt5 can be installed via pip on python3
pip install labelme

