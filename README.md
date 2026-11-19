# antigen_screen.pl

antigen_screen.pl
A Perl script for O-antigen typing from BLASTn m6 results.

This script identifies antigen types by comparing a query genome against curated O antigen reference databases. It is designed for O-antigen typing across all O serotypes, including the O-antigen references collected in this project.

It uses a two-tier strategy:

Full-length matching (tier 1) — an antigen is called when a match reaches ≥ 90% sequence identity and ≥ 90% alignment coverage.

Fragment merging and tiered comparison (tier 2) — for samples without a complete match, fragments with ≥ 80% identity and > 200 bp alignment length are merged into non-redundant intervals, and candidate antigens are ranked by merged coverage and maximum fragment ratio.

Results are reported in three categories:

- High-confidence automatic calls
- Merge-based calls requiring light manual review
- Calls requiring full manual inspection; for the latter, composite metrics of candidate antigens are reported to guide manual correction.

## Dependencies

- Perl (>= 5.10)
- BLAST+ (makeblastdb, blastn)
  
## Example workflow

```bash
## Build BLAST databases from the curated O antigen references
makeblastdb -in O_antigen_references.fasta -dbtype nucl -out O_antigen_db

# Run BLASTn against the antigen reference databases
blastn \
  -db O_antigen_db \
  -query query_genome.fna \
  -outfmt 6 \
  -evalue 1e-5 \
  -num_threads 4 \
  -out query_genome.O.blast.m6

# Run the antigen screening script on the BLAST output
perl antigen_screen.pl query_genome.O.blast.m6 query_genome.O.candicate 90 0.9 O_antigen_references.list query_genome

The -evalue 1e-5 threshold is set at the BLAST step, the Perl script does not re-apply this threshold.

text
```
## Usage

```bash
perl antigen_screen.pl <blast_m6> <output_file> <identity_threshold> <coverage_threshold> <antigen_list> <sample_name>
```
## Parameters

- blast_m6	BLASTn m6-format alignment result (sample sequences vs. database sequences)
- output_file	Output file name (e.g. sample.result)
- identity_threshold	Identity threshold (%) – example: 90
- coverage_threshold	Coverage threshold – example: 0.9
- antigen_list	List of antigen sequence names
- sample_name

See example/README.md for more details.
