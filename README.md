# DropBlock

![build](https://travis-ci.org/miguelvr/dropblock.png?branch=master)


Implementation of [DropBlock: A regularization method for convolutional networks](https://arxiv.org/pdf/1810.12890.pdf) 
in PyTorch.

## Abstract

Deep neural networks often work well when they are over-parameterized 
and trained with a massive amount of noise and regularization, such as 
weight decay and dropout. Although dropout is widely used as a regularization 
technique for fully connected layers, it is often less effective for convolutional layers. 
This lack of success of dropout for convolutional layers is perhaps due to the fact 
that activation units in convolutional layers are spatially correlated so 
information can still flow through convolutional networks despite dropout. 
Thus a structured form of dropout is needed to regularize convolutional networks. 
In this paper, we introduce DropBlock, a form of structured dropout, where units in a 
contiguous region of a feature map are dropped together. 
We found that applying DropBlock in skip connections in addition to the 
convolution layers increases the accuracy. Also, gradually increasing number 
of dropped units during training leads to better accuracy and more robust to hyperparameter choices. 
Extensive experiments show that DropBlock works better than dropout in regularizing 
convolutional networks. On ImageNet classification, ResNet-50 architecture with 
DropBlock achieves 78.13% accuracy, which is more than 1.6% improvement on the baseline. 
On COCO detection, DropBlock improves Average Precision of RetinaNet from 36.8% to 38.4%.


## Installation

Install directly from PyPI:

    pip install dropblock
    
or the bleeding edge version from github:

    pip install git+https://github.com/miguelvr/dropblock.git#egg=dropblock

## Usage


For 2D inputs (DropBlock2D):

```python
import torch
from dropblock import DropBlock2D

# (bsize, n_feats, height, width)
x = torch.rand(100, 10, 16, 16)

drop_block = DropBlock2D(block_size=3, drop_prob=0.3)
regularized_x = drop_block(x)
```

For 3D inputs (DropBlock3D):

```python
import torch
from dropblock import DropBlock3D

# (bsize, n_feats, depth, height, width)
x = torch.rand(100, 10, 16, 16, 16)

drop_block = DropBlock3D(block_size=3, drop_prob=0.3)
regularized_x = drop_block(x)
```

## Implementation details

We use `drop_prob` instead of `keep_prob` as a matter of preference, 
and to keep the argument consistent with pytorch's dropout. 
Regardless, everything else should work similarly to what is described in the paper.
  
## Reference
[Ghiasi et al., 2018] DropBlock: A regularization method for convolutional networks

## TODO
- [ ] Scheduled DropBlock
- [ ] Get benchmark numbers
- [x] Extend the concept for 3D images
