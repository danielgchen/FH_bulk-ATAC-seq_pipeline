# > in rhino
# >> deactivate conda from auto-starting
module load Python/3.7.4-foss-2019b-fh1
module load FastQC/0.11.9-Java-11
module load MultiQC/1.9-foss-2019b-Python-3.7.4
module load cutadapt/2.9-foss-2019b-Python-3.7.4
module load BBMap/38.91-GCC-10.2.0
module load STAR/2.7.7a-GCC-10.2.0
module load picard/2.25.0-Java-11
module load SAMtools/1.11-GCC-10.2.0
pip install RSeQC
Successfully installed RSeQC-4.0.0 bx-python-0.8.11 pyBigWig-0.3.18 pysam-0.16.0.1
# > create working directory
# >> create symbolic links for the dataset
# >> in ipython
from glob import glob
import os
filenames = glob('/fh/fast/greenberg_p/SR/ngs/illumina/jwlee/210812_VH00319_90_AAAMCF5M5/Unaligned/Project_jwlee/ATAC*')
for filename in filenames:
    src = filename
    target = 'raw_data/' + filename.split('/')[-1]
    os.system(f'ln -s {src} {target}')
# > generate fastqc reports
base code off of https://github.com/danielgchen/FH_bulk-RNA-seq_pipeline
# > do bam coverage

