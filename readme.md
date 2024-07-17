# CDEP with DeepLIFT
This fork is an adjusted version of [Contextual Decomposition Explanation Penalization (CDEP)](https://github.com/laura-rieger/deep-explanation-penalization) and also includes changes from [this repository](https://github.com/AminMirzaie/CDEP/). These changes should make the original implementation compatible with newer package versions.

## What is CDEP?
Datasets often include misleading information in the data, which models tend to use in their predictions, even though they are actually irrelevant. Imaging you have an image classifier that decides, if an image shows a "dog" or not. The model may look at wrong areas in images, like the background or objects like dog toys, which frequently appear in those images. In order to fix this issue, CDEP can penalize the model for looking at the wrong information, so that they only produce right predictions for the right reasons (by looking at the dog). To do this uses a generalized version of [Contextual Decompositions (CD)](https://github.com/jamie-murdoch/ContextualDecomposition) to figure out, what information in data models use. Then it compares this to the actual ground-truth explanation and if the model's explanation differs from it, they will be penalized.
To find out more about CDEP, you can read the paper [here](http://proceedings.mlr.press/v119/rieger20a.html) if you are interested. :)

## What is this repository doing?
I'm currently trying to change the CDEP implementation by replacing CD with [DeepLIFT](https://github.com/kundajelab/deeplift), specifically the PyTorch implementation provided by the [Captum](https://github.com/pytorch/captum/tree/master) library. I will be using this modification on the ISIC-experiment and the ColorMNIST-experiment and observe, how this could improve the model's accuracy. But since I'm a PyTorch noob, this idea may not work out as I had planned. We'll see what happens...

## Setup
You'll need Python +12.0 and CUDA 12.1 (with PyTorch 2.3.1). I'd recommend getting the Conda package manager from [Anaconda](https://www.anaconda.com/download/success) to install the other dependencies. In the Jupyter-notebook /isic-skin-cancer/ISIC/Run_ISIC.ipynb you have instructions on how to install necessary packages with Conda for the ISIC-experiment. If some imports won't work, try reinstalling (or uninstall, then install) those packages manually.
I've also included a requirements.txt, although it's still incomplete and I will be updating it, so it hopefully works in the future. Once I've fixed this, you should be able to run "conda env create -f requirements.txt" to create a Conda-environment and immediately install all dependencies.

## Structure / How to use this project
- /src/ contains the CD and CDEP code
- /isic-skin-cancer/ISIC/Run_ISIC.ipynb has the complete, adjusted experiment and analysis on the [ISIC dataset](https://www.isic-archive.com/), run all the cells in order
- /mnist/ColorMNIST/ contains the training on a colored variant of [MNIST](https://yann.lecun.com/exdb/mnist/), execute 00_makedata.py 01_train_all.py in order (or just 02_make_demo.py)
- /mnist/analyze_colormnist.ipynb and /mnist/analyze_mnist.ipynb has the analysis part on the MNIST-experiment, run all the cells in order after training
Note: other folders have experiments on more datasets, like in the original paper. But the code doesn't fully work atm and I won't be fixing those bugs.