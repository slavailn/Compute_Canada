# 🗓️ Introduction to Job Scheduling on Compute Canada (Slurm)

## 1. What Is a Scheduler?
A **scheduler** queues and manages jobs on a compute cluster. Rather than executing immediately, jobs wait in a queue until resources are available. You create a job script that includes:

- Resource requests (CPU, time, memory)
- Job commands

Jobs are submitted with `sbatch`, monitored with `squeue`, and logs are saved automatically.

---

## 2. Scheduler Responsibilities

- Manage job queues and priorities
- Launch jobs when resources are free
- Enforce limits and clean up resources
- Allocate CPUs, RAM, GPUs fairly and efficiently

All Compute Canada clusters use **Slurm Workload Manager**.

---

## 3. Writing and Submitting Jobs

### 🔹 Basic Example: Hello World
```bash
#!/bin/bash
#SBATCH --time=00:01:00
#SBATCH --output=hello_%j.out

echo "Hello, world!"
```
Submit:
```bash
sbatch hello.sh
```

---

### 🔹 Example: Python Script Execution
```bash
#!/bin/bash
#SBATCH --account=def-myproj
#SBATCH --time=02:00:00
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --output=python_%j.log

module load python/3.9
srun python script.py
```

---

### 🔹 Example: GPU Job
```bash
#!/bin/bash
#SBATCH --account=def-myproj
#SBATCH --time=04:00:00
#SBATCH --gres=gpu:1
#SBATCH --mem=16G
#SBATCH --cpus-per-task=4
#SBATCH --output=gpu_%j.log

module load cuda/11.4
srun ./gpu_analysis
```

---

### 🔹 Example: Job Array
```bash
#!/bin/bash
#SBATCH --array=1-10
#SBATCH --time=01:00:00
#SBATCH --output=array_%A_%a.out

srun ./process_sample.sh sample_${SLURM_ARRAY_TASK_ID}.txt
```

---

## 4. Useful Slurm Commands

| Command                | Purpose                                |
|------------------------|----------------------------------------|
| `sbatch job.sh`        | Submit a job                           |
| `squeue -u $USER`      | View your job queue                    |
| `sacct -j <jobID>`     | Check job history & stats              |
| `scancel <jobID>`      | Cancel a running or queued job         |

---

## 5. Tips and Best Practices

- Always use `sbatch` (not manual login node execution)
- Use appropriate `--mem` and `--time` to reduce queue delays
- Prefer `/project` or `/scratch` paths for job I/O
- Use `srun` in scripts to ensure proper job execution context

---

## 6. Summary Table: SLURM Directives

| Directive            | Description                             |
|----------------------|-----------------------------------------|
| `--time=HH:MM:SS`    | Max runtime                             |
| `--mem=XM` or `--mem-per-cpu=XM` | RAM allocation              |
| `--cpus-per-task=X`  | CPU cores per task                      |
| `--gres=gpu:X`       | Number of GPUs                          |
| `--array=1-N`        | Job array for many similar jobs         |
| `--output=file_%j.out` | Output file naming (job ID = `%j`)    |

---

## 7. Final Notes

- Keep scripts modular and version-controlled
- Monitor queue wait times and job efficiency with `sacct`
- Use fairshare-aware submissions to avoid bottlenecks
- Leverage partitions wisely for your job’s memory/GPU needs
