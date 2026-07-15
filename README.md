# sgRNA_counting
sgRNA_counting is a tool for quantifying sgRNA libraries used in perturb-seq data. Currently, sgRNA_counting is still under testing. For basic operation, please refer to the following commands. Note: sgRNA_counting_V2 fit BGI 5' scRNA-seq data.

## 1. Merge sgRNA reads
'''bash  
sample=CR4-SP2
outdir=/data/work/Batch2/01.PISA
fq1=/zfssz8/SZDCS_DATA/BGISEQ01/DIPSEQ/DIPSEQT20/P24Z10200N1035_Temp/D2606375238/260629_SEQ091_FP500005068_L01_D2606375238001/FP500005068_L01_25_1.fq.gz
fq2=/zfssz8/SZDCS_DATA/BGISEQ01/DIPSEQ/DIPSEQT20/P24Z10200N1035_Temp/D2606375238/260629_SEQ091_FP500005068_L01_D2606375238001/FP500005068_L01_25_2.fq.gz
mkdir -p ${outdir}/${sample}
/scRNA-seq-v3.1.5-pipeline/bin/PISA parse -t 16 -q 4 -dropN -config /data/input/Files/huangyaling/iMAP/scRNA_beads_darkReaction.json -cbdis ${outdir}/${sample}/barcode_counts_raw.txt -1 ${outdir}/${sample}/reads.fq -report ${outdir}/${sample}/sequencing_report.csv ${fq1} ${fq2}
'''

## 2. sgRNA counting
'''
python /data/work/process_sgRNA_counting_V2.py \
    -f /data/work/SPNK_analysis/01.PISA/Spleen_sgRNA/reads.fq \
    -r /data/work/reverse_complement_sgRNA_ref.csv \
    -t TTCCAGCATAGCTCTTAAAC \
    -l 20 \
    -n 32 \
    -o Spleen_sgRNA_matrix_rc \
    -m 1 \
    -c 200000 \
    -b /data/work/SPNK_analysis/01.PISA/Spleen_sgRNA/Spleen_barcodeTranslate.csv
'''
