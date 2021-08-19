# Install Packages
We run the following command in rhino (make sure that `Anaconda` is not installed).
1. **Install modules**
  - module load Python/3.7.4-foss-2019b-fh1
  - module load FastQC/0.11.9-Java-11
  - module load MultiQC/1.9-foss-2019b-Python-3.7.4
  - module load cutadapt/2.9-foss-2019b-Python-3.7.4
  - module load BBMap/38.91-GCC-10.2.0
  - module load STAR/2.7.7a-GCC-10.2.0
  - module load picard/2.25.0-Java-11
  - module load SAMtools/1.11-GCC-10.2.0
2. Install pip packages
  - pip install RSeQC

    The output should look like: `Successfully installed RSeQC-4.0.0 bx-python-0.8.11 pyBigWig-0.3.18 pysam-0.16.0.1`

# Prepare Directory Environment
1. **Make Directories**
  - Create a directory for the project (`workdir`)
  - Inside `workdir` make a `data/raw_data` folder
  - `controller.py` and `config.yaml` will reside in `workdir`
2. **Create Symbolic Links to the Dataset**
  - Create these links in the `workdir/data/raw_data` folder, example code is below.

    ```
    from glob import glob
    import os
    filenames = glob('/fh/fast/greenberg_p/SR/ngs/illumina/jwlee/210812_VH00319_90_AAAMCF5M5/Unaligned/Project_jwlee/ATAC*')
    for filename in filenames:
        src = filename
        target = 'raw_data/' + filename.split('/')[-1]
        os.system(f'ln -s {src} {target}')
    ```

# Run Main Pipeline
1. **Run `controller.py`**
  - Ideally open a `tmux` window or use `nohup` because this command generally takes a while to run. Final QC reports can all be found in the `workdir/qc_reports` folder. The full summary is in `workdir/qc_reports/summary/multiqc.html`.

# `TODO`:
- add argparse to the controller.py
  - to allow for custom R1/read1 naming schemes
  - to substitute for config.yaml (at least for the small things aside from hg38 and links)
  - to allow for custom step running
- allow a run from x nature so we can save certain steps
  - restructure code to have methods
- see if we can directly download adapters.fa
  - and keep it in a separate location from raw data

