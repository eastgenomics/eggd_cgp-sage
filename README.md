# eggd_cgp-sage

SAGE (Hartwig Medical Foundation, v5.0-beta.11) tumour-only somatic SNV/indel caller, packaged as
a DNAnexus app. It is a parallel stage (with AMBER/COBALT) of the
[`eggd_atlas_cnv`](https://github.com/eastgenomics/eggd_atlas_cnv) somatic CNV workflow; its
somatic VCF anchors PURPLE's purity fit.

## Inputs (summary)
`tumour_bam`/`tumour_bai`, `sample_id`, `sage_jar`, `ref_fasta`/`ref_fai`, `hotspots_vcf`/`hotspots_tbi`,
`panel_bed`, `hc_bed`, `pon_file`, `ensembl_data`.

## Outputs
`somatic_vcf` (`{sample_id}.sage.somatic.vcf.gz`) + `somatic_vcf_tbi` → PURPLE.

## Notes
- Panel mode: `-panel_only -high_depth_mode -skip_msi_jitter -skip_bqr -ref_sample_count 0 -ref_genome_version 38`.
- Instance `mem2_ssd1_v2_x16`; timeout 8 h. Deps via `execDepends` (no run-time apt-get).
