
# singularity-pytorch-gpu
[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/4969)

Singularity image for a deep learning (pytorch) environment + GPU support (cuda-10.2). Contains libraries to perform common ML tasks. `Openslide` is included to manipulate whole-slide histology images, `imagemagick` for general image manipulation. `JupyterLab` and `code-server` (VS Code) are also included in the image. This image has been tested in an HPC (SGE) with distributed pytorch applications.

## Installing singularity
To install singularity, see the [official docs](https://sylabs.io/guides/3.6/admin-guide/installation.html#installation-on-linux).

## Building/downloading the image
To build an image called `torchenv.sif` based on the definition file `Singularity.1.0.0`, an NVIDIA GPU and `cuda-10.2` drivers must be available on the host system. Clone this repository, move into it and run the singularity build command. 

```
git clone https://github.com/manuel-munoz-aguirre/singularity-pytorch-gpu.git && \
cd singularity-pytorch-gpu && \
sudo singularity build torchenv.sif Singularity.1.0.0
```

Otherwise, the image can be pulled directly from singularity hub:
```
singularity pull torchenv.sif shub://manuel-munoz-aguirre/singularity-pytorch-gpu:1.0.0
```

## Using the container
To spawn an interactive shell within the container, use the command below. The `--nv` flag setups the container to use NVIDIA GPUs (read more [here](https://sylabs.io/guides/3.6/user-guide/gpu.html)).
```
singularity shell --nv torchenv.sif
```

To run a script (for example, `script.py`) using the container without starting an interactive shell:
```
singularity exec --nv torchenv.sif python3 script.py
```

The container can also be launched and used on a system without a GPU, but upon startup it will display a warning about missing NVIDIA binaries on the host.