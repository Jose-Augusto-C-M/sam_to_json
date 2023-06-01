## A Python package to segmenting image data with the Segment Anything Model (SAM) and export to labelme json format

# Introduction

The basis for the idea of project involves SAM: https://github.com/facebookresearch/segment-anything, and labelme: https://github.com/wkentaro/labelme. The Segment Anything Model (SAM) produces high quality object masks from input prompts such as points or boxes, and it can be used to generate masks for a great diversity of objects and data in an image. Labelme is a graphical image annotation tool inspired by http://labelme.csail.mit.edu. It is written in Python and uses Qt for its graphical interface.


The code requires python>=3.9, as well as pytorch>=1.7 and torchvision>=0.8. Installing both PyTorch and TorchVision with CUDA support is strongly recommended.

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
