# How to install packages?

If the code is written in Python, it can be very convenient to use *conda* package manager (https://docs.conda.io/en/latest/). With *conda*, it is possible to quickly install and manage the required packages and their dependencies by creating "environments".

### Example with tensorflow

Our code is a simple "Hello world" code. It is using *tensorflow* and has some dependencies. Just to take an example, let say it depends on a specific version (3.5.1) of matplotlib.

The "Hello world" code instructions are contained in a file called helloworld-tf.py:
```
import tensorflow as tf
msg = tf.constant('Hello TensorFlow!')
tf.print(msg)
```

In order to install these packages and their dependencies, we will create a conda environment called "test-env".
To do so, we first create a *environment.yml* file containing the specifications about the environment: name, the required conda channels and the dependencies:
```
name: test-env
channels:
  - conda-forge
dependencies:
  - tensorflow-gpu
  - matplotlib==3.5.1
```
The environment is created with:
```
module load python3
conda env create -f environment.yml
```

To run the code on a GPU node, we submit a job with sbatch:
```
sbatch helloworld-tf.sh
```

where helloworld-tf.sh contains some usual SLURM specifications and the instructions to load the *test-env* environment and execute the code:
```
#!/usr/bin/env bash

#SBATCH -J helloworld-tf
#SBATCH --output helloworld-tf.log
#SBATCH -p gpu
#SBATCH -A bb1245
#SBATCH --time=1:00:00
#SBATCH --mem=32G
#SBATCH --reservation=GPUtest

module load python3
source activate test-env
python helloworld-tf.py
```

The working directory should then contain a "helloworld-tf.log" output file with the corresponding 'Hello TensorFlow!' line.
