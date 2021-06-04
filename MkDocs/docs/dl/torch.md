# PyTorch Notes

This jupyter notebook contains my code when studying PyTorch.


```python
# torch edition 
import torch
print(torch.__version__)
```

    1.8.1+cu111



```python
# cuda 
print(torch.cuda.is_available())
print(torch.cuda.device_count())
print(torch.cuda.get_device_name())
print(torch.cuda.get_device_capability(0))
```

    True
    1
    GeForce GTX 1060
    (6, 1)
