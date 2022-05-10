This repository seeks to recreate the work of https://arxiv.org/abs/1908.11025. Their original code is published in [the author's original repository](https://github.com/zlzeng/DeepFloorplan). However, it was written in a much older version of Python and Tensorflow, so [here is a repository that rewrites it into Python 3.7.4 with Tensorflow version 2.3.](https://github.com/zcemycl/TF2DeepFloorplan)

To recreate training of the network, you can broadly follow the steps written in the [updated repository](https://github.com/zcemycl/TF2DeepFloorplan). However, due to versioning and certain package problems (scipy dropping support for certain functions, etc.,) there were a couple problems that I needed to fix.

The initial repository (the one in Python 2.7) was trained using the r3d dataset & the r2v dataset. [Information about r3d is available here.] (http://www.cs.toronto.edu/~fidler/projects/rent3D.html). It can be [downloaded here](https://structured3d-dataset.org/#download). The new repository out of box only works with r3d. The original repository has the instructions to transform the r3d dataset into the proper tfrecords format. 

R2v is accessible by following the link [available here](https://github.com/zlzeng/DeepFloorplan/blob/master/dataset/download_links.txt). It is the result of transforming the LIFULL HOME dataset into a vectorized (instead of rasterized) format. [More information can be found here.](https://github.com/art-programmer/FloorplanTransformation)

[A recreation of most functionality can be found here in a colab notebook.](https://colab.research.google.com/github/zcemycl/TF2DeepFloorplan/blob/master/deepfloorplan.ipynb)


So to recreate training:

[Set up NVIDIA cuDNN](https://developer.nvidia.com/cudnn)

[Clone the repository](https://github.com/zcemycl/TF2DeepFloorplan)

Fix the following bugs when they come up:

It is highly likely that pip will fail to download the versions required. You can install the most recent versions of everything, but a couple issues will arise:
scipy will have an error with await: you need to downgrade to scipy to 1.1.0 and install Pillow. If this does not work, downgrade Pillow to 8.0.1. If that still does not work, change scipy to 1.4.1. 

An error with pyreadline complaining about ‘collections’ will come up. [Follow this link to resolve](https://github.com/pyreadline/pyreadline/issues/65).

Populate the annotations folder with files from the following https://github.com/zlzeng/DeepFloorplan/blob/master/dataset/download_links.txt
	
Test with python train.py --batchsize=8 --lr=1e-4 --epochs=60 
--logdir=log/store --modeldir=model/store
. More information about the CLI can be found at [this readme](https://github.com/zcemycl/TF2DeepFloorplan).

