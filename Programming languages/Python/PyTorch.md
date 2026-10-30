Inorder to get familiar with PyTorch at first watch this course from the PyTorch itself: [PyTorch Beginner Series](https://www.youtube.com/playlist?list=PL_lsbAsL_o2CTlGHgMxNrKhzP97BaG9ZN)

You can view the PyTorch documents relative to the course in here too: [PyTorch Beginner Series Doc](https://docs.pytorch.org/tutorials/beginner/introyt/introyt_index.html)


>Note: Not everything of the course is written here!

## Auto grad
Pytorch has got an Automatic Differentiation Engine.
Actually each tensor has got some meta data about its history, where it came from, and pytorch calculates the gradients using that history.
![[PyTorch-20261029185319915.webp]]


## A simple PyTorch model
```python
import torch #W for all things PyTorch
import torch.nn as nn # for toch.nn.Module, the parent bject for PyTorch models
import torch.nn.functional as F # for the activation function
```

