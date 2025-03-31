# Installation


The code was tested on Ubuntu 24.04, with [Anaconda](https://www.anaconda.com/download) Python 3.11 and [PyTorch]((http://pytorch.org/)) v2.5.1. NVIDIA GPUs are needed for both training and testing.
After install Anaconda:

0. [Optional but recommended] create a new conda environment. 

    ~~~
    conda create --name CenterNet python=3.11
    ~~~
    
    And activate the environment.
    ~~~
    conda activate CenterNet
    ~~~

1. Install pytorch:

    ~~~
    conda install pytorch torchvision -c pytorch
    ~~~
    
    And disable cudnn batch normalization(Due to [this issue](https://github.com/xingyizhou/pytorch-pose-hg-3d/issues/16)).
    
    Open `~/anaconda3/envs/CenterNet/lib/python3.11/site-packages/torch/nn/functional.py` and find the line with `torch.batch_norm` and replace the `torch.backends.cudnn.enabled` with `False`. We observed slight worse training results without doing so. 
     
2. Install [opencv-python](https://pypi.org/project/opencv-python/)

    ~~~
    pip install opencv-python
    ~~~

3. Clone this repo & intall the requirements:

    ~~~
    CenterNet_ROOT=/path/to/clone/CenterNet
    git clone https://github.com/xingyizhou/CenterNet $CenterNet_ROOT
    cd $CenterNet_ROOT
    conda install --file requirements.txt
    ~~~

4. Install [COCOAPI](https://github.com/cocodataset/cocoapi):

    ~~~
    # COCOAPI=/path/to/clone/cocoapi
    git clone https://github.com/cocodataset/cocoapi.git $COCOAPI
    cd $COCOAPI/PythonAPI
    make
    python setup.py install --user
    ~~~

5. Clone repo & compile deformable convolutional (from [DCNv2](https://github.com/lucasjinreal/DCNv2_latest)).

    ~~~
    cd $CenterNet_ROOT/src/lib/models/networks/
    git clone https://github.com/lucasjinreal/DCNv2_latest.git DCNv2
    cd DCNv2
    ./make.sh
    ~~~

6. [Optional, only required if you are using extremenet or multi-scale testing] Compile NMS if your want to use multi-scale testing or test ExtremeNet.

    ~~~
    cd $CenterNet_ROOT/src/lib/external
    make
    ~~~

7. Download pertained models for [detection]() or [pose estimation]() and move them to `$CenterNet_ROOT/models/`. More models can be found in [Model zoo](MODEL_ZOO.md).
