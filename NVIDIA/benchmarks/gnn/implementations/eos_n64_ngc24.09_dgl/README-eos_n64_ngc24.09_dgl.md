## Steps to launch training

### eos_n64_ngc24.09_dgl

Launch configuration and system-specific hyperparameters for the
eos_n64_ngc24.09_dgl submission are in the
`benchmarks/gnn/implementations/eos_n64_ngc24.09_dgl/config_DGXH100_64x8x512.sh` script.

Steps required to launch training for eos_n64_ngc24.09_dgl.  The sbatch
script assumes a cluster running Slurm with the Pyxis containerization plugin.

1. Build the docker container and push to a docker registry

```
docker build --pull -t <docker/registry:benchmark-tag> .
docker push <docker/registry:benchmark-tag>
```

2. Launch the training
```
source config_DGXH100_64x8x512.sh
CONT=<docker/registry:benchmark-tag> DATADIR=<path/to/data/dir> LOGDIR=<path/to/output/dir> sbatch -N ${DGXNNODES} -t ${WALLTIME} run.sub
```
