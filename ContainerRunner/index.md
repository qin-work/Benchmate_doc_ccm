---
layout: default
title: ContainerRunner
---

## Container Runner module:

This is a module that would allow you to run any conteinerized application on your local machine or on a remote server. To give you the most
flexible way to incoporate your data into you database we have created a container runner class that can be used to run any singularity/apptainer
containter either locally or on HPC. We also have a to_container script that can be used to convert conda environments into singularity/appatiner
contianers. 

We are working on creating a small libarry of exisiting containers that can be immediately used to process your data. These will be available 
soon in our own docker container registry. You can then use these docker containers to create a singluarity/apptainer .sif file to run arbitrary packages and pipelines. You can run these packages and commands either in an interactive session or submit them as slurmm jobs in HPC. Please see the container runner module readme for usage instructions. 

Keep in mind that if you want to integrate the outputs of these containers/pipelines it's up to you to make sure that they are compatible with the modules in this package. 


## Overview

The `ContainerRunner` class provides a unified interface for:

- Running containers locally
- Submitting container jobs to SLURM
- Managing bind mounts and GPU access
- Monitoring SLURM job status

## Usage

### Basic Local Container Execution

```python
from ccm_benchmate.container_runner.container_runner import ContainerRunner

# Initialize with container path
runner = ContainerRunner(
    container_path="/path/to/container.sif",
    running_command="singularity"  # or "docker"
)

# Add bind mounts
runner.add_bind_mount(
    host_paths=["/host/path1", "/host/path2"],
    container_path="/container/path"
)

# Enable GPU support if needed
runner.enable_gpu()

# Run command in container
result = runner.run("echo hello")
```

### SLURM Cluster Execution

```python
# Submit job to SLURM
job_id = runner.run_slurm(
    command="python script.py",
    job_name="my_job",
    partition="gpu",
    nodes=1,
    ntasks=1,
    time="01:00:00",
    mem="16G",
    gpus=1,
    output_file="job_%j.out",
    additional_sbatch={"mail-type": "END,FAIL"}
)

# Check job status
status = runner.check_slurm_job_status(job_id)

# Get detailed job info
job_info = runner.get_slurm_job_info(job_id)
```

## Key Features

### Container Execution

- Support for Singularity and Docker containers
- Configurable bind mounts
- GPU support via `--nv` flag
- Command execution with subprocess handling

### SLURM Integration

- Submit container jobs to SLURM
- Monitor job status
- Retrieve detailed job information
- Customizable SLURM job parameters

### Error Handling

- Custom exception classes
- Subprocess error capturing
- SLURM job error handling

## Notes

- Requires Singularity/Docker to be installed
- SLURM functionality requires access to a SLURM cluster
- GPU support requires NVIDIA drivers and appropriate container configuration
- Bind mounts require valid host paths
- Ensure that the container image is accessible from the execution environment
- SLURM job submission may require additional configuration based on the cluster setup
