## Steps to launch training

### eos_ngc24.09_nemo

Launch configuration and system-specific hyperparameters for the
eos_ngc24.09_nemo submission are in the
`benchmarks/llama2_70b_lora/implementations/eos_ngc24.09_nemo/config_DGXH100_1x8x4xtp4pp1cp1.sh` script.

Steps required to launch training for eos_ngc24.09_nemo.  The sbatch
script assumes a cluster running Slurm with the Pyxis containerization plugin.

1. Build the docker container and push to a docker registry

```
docker build --pull -t <docker/registry:benchmark-tag> .
docker push <docker/registry:benchmark-tag>
```

2. Launch the training
```
source config_DGXH100_1x8x4xtp4pp1cp1.sh
CONT=<docker/registry:benchmark-tag> DATADIR=<path/to/data/dir> LOGDIR=<path/to/output/dir> sbatch -N ${DGXNNODES} -t ${WALLTIME} run.sub
```
