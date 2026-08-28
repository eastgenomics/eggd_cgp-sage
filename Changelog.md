# Changelog

## 1.0.2
Fix: `runSpec.execDepends` declares `openjdk-21-jre-headless`, `samtools`, and `tabix`,
which are resolved from an apt mirror at job start. execDepends was replaced with assetDepends
to prevent failures if the mirror is unreachable. 

## 1.0.1
Fix: the SAGE panel-of-normals contig-prefix check (`code.sh`, added in the 1.0.0 review
round) misread the PON TSV's plain header row (`Chromosome\tPosition\t...`, no `#`
marker) as data, incorrectly failing every run with "PON file does not have chr-prefixed
contigs". Every other chr-prefix-checked input (BAM, hotspots VCF, panel BED, hc_bed) has
either a `#`-marked header or no header at all, so this went uncaught until the first
end-to-end run against the published app. Fixed by explicitly skipping the PON's first
line (`tail -n +2 | head -1`) rather than filtering on `#`. No interface change.

## 1.0.0
Initial app release. Converted from the `cnv-backbone-purple-atlas` `cgp-sage` **applet** into a
versioned, namespaced DNAnexus **app** (`org-emee_1`, `aws:eu-central-1`) for the `eggd_atlas_cnv`
somatic CNV workflow.

Conversion changes only: app metadata; explicit `timeoutPolicy` (8 h); system dependencies moved
from inline `apt-get install` to `runSpec.execDepends` (`openjdk-21-jre-headless`, `samtools`,
`tabix`). SAGE tool flags and the `somatic_vcf`/`somatic_vcf_tbi` outputs are unchanged.
