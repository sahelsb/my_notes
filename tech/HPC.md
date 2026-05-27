The terms **cloud**, **cluster**, and **high-performance computing (HPC)** refer to different types of computing resources:

- **Cloud**: A flexible, on-demand computing resource that can be located anywhere globally. It includes both internal (private) and external (commercial) services, supporting various tasks from web hosting to compute-intensive simulations.
- **HPC (High-Performance Computing)**: A specialized system designed for highly demanding computational tasks, featuring integrated processing and storage elements. These systems are physically fixed in specific locations to ensure optimal performance.
- **Cluster**: A smaller-scale HPC system, often found in computing centers, where multiple interconnected machines share storage and networking to handle intensive computational workloads.

HPC stands for **High Performance Computing** and is synonymous with the more colloquial term **Supercomputer**. A supercomputer is a collection, or cluster, of a large number of regular computers (referred to as **compute nodes**) connected over a network. Each of the computers is like a local workstation though typically much more capable. 

A **cluster** consists of multiple **nodes** (also called servers or machines), each serving different roles:

- **Frontend Node**: The access point to the cluster, used for file transfers, software setup, and quick tests. It should not be used for intensive tasks.  In our case tinygpu.nhr.fau.de is the shared frontend node of the cluster `tinygpu` that we get access to.
- **Worker (Compute) Nodes**: Perform the actual computational work, handling resource-heavy tasks. In our case `tinygpu` has some different gpu working nodes like `tg06x`
- **Scheduler**: Manages job distribution across worker nodes.

Each node contains standard computer components: **CPUs (processors/cores), memory (RAM), and disk storage**. While some storage may be local, clusters often use shared, remote fileservers.

Each of the users connects to HPC from their own local workstation and can run work on one or more of HPC's compute nodes. You can imagine with this shared resource model, however, that without some sort of coordination, managing which users get what resources turns into a major logistical challenge. That's why supercomputers use **job schedulers**.

#### Slurm

A job scheduler is software used to coordinate user jobs. In our case, we use a scheduler called [Slurm](https://slurm.schedmd.com/documentation.html). You can use it by writing a **batch script** that requests compute resources (e.g., CPUs, RAM, GPUs) and includes instructions for running your code. You submit this script to the job scheduler which then goes and finds available resources on the supercomputer for your job. When the resources become available, it initiates the commands included in your batch script, and outputs the results to a text file.

Slurm is a highly customizable, open-source job scheduler used on many high-performance computing (HPC) systems. It allows you to manage resources (like CPUs, GPUs, and memory) and run jobs (scripts or commands) on those resources.

**Slurm Job**: A **Slurm job** is a script or command that you want to run on the cluster. It can be a Python script, a shell command, or a program that requires specific computational resources (like CPUs, GPUs, memory).

**Job Queuing**: When you submit a job, it enters a queue and is managed by the scheduler, waits for the necessary resources (such as a GPU) to become available. Once resources are available, Slurm allocates them to your job and starts execution.

---

**Slurm Commands**: Slurm uses a few key commands for job management:

`salloc`: Allocates resources interactively ,for **interactive jobs** (for one-off commands or development).
**interactive jobs** allow users to work directly on compute nodes as if they were using a local terminal. This is useful for debugging, testing, or running exploratory computations.

To request an interactive session, use the `salloc` or `srun` commands:

```
salloc.tinygpu --gres=gpu:1 --time=01:00:00
```
After running this command, you’ll be given a terminal session with exclusive access to a GPU for 1 hour.

###### Controlling interactive jobs:

```
# Check the hostname of the compute node
hostname             

# Monitor resource usage
top

# exiting and interactuve job
exit
```

---

`sbatch`: Submits a **batch job** script that will be executed on allocated resources.

```
sbatch.tinygpu my_batch_script.sh
```

Batch job scripts typically contain job parameters (e.g., how many GPUs or CPUs you need) and the command to run (e.g., a Python script).

- `srun`: Runs commands inside `sbatch` or `salloc` (can be used to start parallel jobs).
- `squeue`: Shows the status of jobs in the queue.  `squeue -u $USER`
- `scancel`: Cancels a running or queued job.  `scancel <job_id>`

**Interactive vs Batch Jobs**:
- **Interactive jobs** are useful when you need immediate access to computational resources and want to execute commands or scripts directly. They are typically used for debugging, development, or testing.
- **Batch jobs** are for longer, non-interactive tasks, such as model training or data processing. Batch jobs are queued and executed without requiring direct interaction.

##### Batch jobs
When using **batch jobs**, you’ll typically create a shell script that contains all the Slurm directives (e.g., which resources you want to request) and the commands you want to run. Here's an example script for running a Python script with GPU resources:

```
#!/bin/bash -l
#SBATCH --gres=gpu:1         # Request 1 GPU
#SBATCH --partition=rtx3080  # Specify GPU type (if you want RTX 3080)
#SBATCH --time=06:00:00      # Set job runtime
#SBATCH --mem=32GB           # Set memory allocation
#SBATCH --cpus-per-task=4    # Request 4 CPUs for the job
#SBATCH --export=NONE        # Avoid exporting environment variables

# Set up the environment and activate your conda environment
module load python          # Load Python module
conda activate myenv        # Activate your conda environment

echo "Job started on $(hostname) at $(date)"

# Run your Python script
python3 my_script.py

echo "Job finished at $(date)"

```

###### Monitor the job queue:

```
squeue -u yourUsername
OR
watch -n 15 squeue -u yourUsername
```

---
#### Running Jupyter Notebook with Slurm

In order to run jupyter notebook with GPU access you need to 

1. get connect to the the front end node in hpc like tinygpu via ssh connection in vscode
2. Then inside the vscode terminal actiavte your conda environemnet and request gpu access via salloc

```
salloc.tinygpu --gres=gpu:1 --time=01:00:00
```

3. Then in a second treminal  in vscode (that is connected to tinygpu), you have to get connected to the gpu node and forward the port from gpu node to tinygpu 

```
iwi1115h@tinyx: ssh -L 2718:localhost:2718 iwi1115h@tg067
```

1. then in a terminal in your local machine you have to forward the port from tinygpu to your local machine to be able to open jupyter server

```
 ssh -L 2718:localhost:2718 iwi1115h@tinyx.nhr.fau.de

```

Now you can open the jupyter server under the localhost with this port 2718 in your browser

--- 
#### Start an Interactive Job with GPU

1. salloc.tinygpu --gres=gpu:1 --time=01:00:00
2. module load python 
3. conda activate myenv
4. run the script

```
salloc.tinygpu --gres=gpu:a100:1  -p a100 --time=03:00:00
module load python
module load gcc/11.2.0
export http_proxy=http://proxy:80
export https_proxy=http://proxy:80
```

Performance boosts come from optimizing your code to make use of the additional processors available on HPC, a practice known as parallelization..
Parallelization enables jobs to "divide-and-conquer" independent tasks within a process when multiple threads are available. In practice, this typically means running a job with multiple CPUs on the HPC. On your local machine, running apps like your web browser is natively parallelized, meaning you don't have to worry about having so many tabs open. However, on the HPC, parallelization must almost always be explicitly configured and called from your job.



### Error for gcc version

The error happened because your system was using an older version of **GCC's libstdc++**, which didn't include `GLIBCXX_3.4.29`. The **SciPy** library (used by `transformers`) required this newer version, but your system couldn't find it.

By switching to **GCC 11.2**, you upgraded `libstdc++`, which resolved the issue

```
module avail gcc  # Check available versions
module load gcc/11.2.0  # Example: Load GCC 11.2.0
```