# Changelog

## 1.0.0
Initial app release. Converted from the `cnv-backbone-purple-atlas` `cgp-sage` **applet** into a
versioned, namespaced DNAnexus **app** (`org-emee_1`, `aws:eu-central-1`) for the `eggd_atlas_cnv`
somatic CNV workflow.

Conversion changes only: app metadata; explicit `timeoutPolicy` (8 h); system dependencies moved
from inline `apt-get install` to `runSpec.execDepends` (`openjdk-21-jre-headless`, `samtools`,
`tabix`). SAGE tool flags and the `somatic_vcf`/`somatic_vcf_tbi` outputs are unchanged.
