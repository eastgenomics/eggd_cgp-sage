# eggd_cgp-sage

[SAGE](https://github.com/hartwigmedical/hmftools/tree/master/sage) (Hartwig Medical Foundation, v5.0-beta.11) tumour-only somatic SNV/indel caller, packaged as
a DNAnexus app. It is a parallel stage (with AMBER/COBALT) of the
[`eggd_atlas_cnv`](https://github.com/eastgenomics/eggd_atlas_cnv) somatic CNV workflow; its
somatic VCF anchors PURPLE's purity fit.

## Inputs (summary)
`tumour_bam`/`tumour_bai`, `sample_id`, `sage_jar`, `ref_fasta`/`ref_fai`, `hotspots_vcf`/`hotspots_tbi`,
`panel_bed`, `hc_bed`, `pon_file`, `ensembl_data`.

## Outputs
`somatic_vcf` (`{sample_id}.sage.somatic.vcf.gz`) + `somatic_vcf_tbi` → PURPLE.

## Usage
```bash
dx run eggd_cgp-sage \
  -itumour_bam=file-xxxx \
  -itumour_bai=file-xxxx \
  -isample_id=SAMPLE001 \
  -isage_jar=file-xxxx \
  -iref_fasta=file-xxxx \
  -ihotspots_vcf=file-xxxx \
  -ihotspots_tbi=file-xxxx \
  -ipanel_bed=file-xxxx \
  -ihc_bed=file-xxxx \
  -ipon_file=file-xxxx \
  -iensembl_data=file-xxxx \
  --destination /output/
```

## Notes
- **GRCh38 only**: all reference inputs (FASTA, hotspots, PON, panel BED, hc_bed) must use GRCh38 (`chr`-prefixed contigs); the app passes `-ref_genome_version 38` to SAGE and will not work with GRCh37 inputs.
- Panel mode: `-panel_only -high_depth_mode -skip_msi_jitter -skip_bqr -ref_sample_count 0 -ref_genome_version 38`.
- `ref_fasta` must be a **bgzipped** `.fa.gz`; the app decompresses it and regenerates `ref.fa.fai`/`ref.dict` at runtime (htsjdk needs plain FASTA), so `ref_fai` is not downloaded. The input is kept as **optional** in `dxapp.json` for interface stability — existing workflow configs that supply it will continue to work.
- `hc_bed` is expected as a **gzipped** BED (`.bed.gz`); it is passed to SAGE's `-high_confidence_bed` as-is.
