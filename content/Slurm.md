

### Basic slurm syntaxes

To submit a slurm job. Once you submit a job you will get a slurm job id.
```
sbatch your_slurm_file_name.job
```

To see the status of submitted job
```
squeue job_id

```

Cancel/kill submitted job
```
scancel job_id
```

### Example slurm script `slurm.job`

Modify the script below according to your usage and environment variables.

```
#!/bin/bash
#SBATCH --job-name=beta_search
#SBATCH --cpus-per-task=24
#SBATCH --mem=32G
#SBATCH --time=2-00:00:00                    # Max runtime: 3 days
#SBATCH --nodelist=server1                   # Run on a specific node (optional)

# --- Timestamp for logs ---
basefolder=../../Data/rnn_data
timestamp=$(date +"%Y%m%d_%H%M%S")
logsfolder=${basefolder}/logs
mkdir -p ${logsfolder}

# --- Redirect stdout and stderr ---
exec > ${logsfolder}/${SLURM_JOB_NAME}_${timestamp}_${SLURM_JOB_ID}.out
exec 2> ${logsfolder}/${SLURM_JOB_NAME}_${timestamp}_${SLURM_JOB_ID}.err

# --- Log job start ---
echo "Job started at: $(date)"
echo "Running on node: $(hostname)"
echo "SLURM Job ID: $SLURM_JOB_ID"

# --- Conda activation ---
eval "$(/mnt/pve/Homes/conda/miniconda3/bin/conda shell.bash hook)"
conda activate bapun_conda_env

# --- Export custom PYTHONPATH ---
export PYTHONPATH=/mnt/pve/Homes/bapun/Codes/NeuroPy:/mnt/pve/Homes/bapun/Codes/BanditPy:/mnt/pve/Homes/bapun/Codes/py_adlab_bg:$PYTHONPATH

# --- Run your Python job ---
python create_rnn_data.py

# --- Log job end ---
echo "Job finished at: $(date)"
```

