# How to check the GPU usage?

It might be important for debugging purposes to check if the code is actually using GPUs and how?
In this section, we are giving some instructions to monitor this usage at a lower level.

## With tensorflow

Assuming the user has created a conda environment including tensorflow ([See *environments* section](./environments.md)), we can submit the following job script:

```
#!/usr/bin/env bash

#SBATCH -J testgpu-tf
#SBATCH --output testgpu-tf.log
#SBATCH -p gpu
#SBATCH -A bb1245
#SBATCH --time=1:00:00
#SBATCH --mem=32G
#SBATCH --reservation=GPUtest

module load python3
source activate test-env
python testgpu-tf.py
```

where the Python file contains the following instructions:
```
import tensorflow as tf
if tf.test.gpu_device_name():
    print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
else:
    print("No GPU device!")
```

With a successful installation, the output file "testgpu-tf.log" created in the working directory should contain the name of the GPU device (most likely "/device:GPU:0").


## With PyTorch


## NVIDIA System Management Interface

The NVIDIA management library is providing a useful command line utility called *nvidia-smi* (https://developer.nvidia.com/nvidia-system-management-interface). It can be used to get more detailed information about the GPU usage (.e.g, number of used GPUs, memory usage, etc.).

This information is provided in real time by logging to the node where the code is running. For example, if the computation node is l40366, one should first log to this node with:
```
ssh l40366
```
and then execute:
```
nvidia-smi
```

The result of the command line should be similar to the following screenshot:
```{figure} /media/nvidia-smi_example.png
```
