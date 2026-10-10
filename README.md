# antigen_screen.pl

A Perl script for antigen identification from BLASTn results.  
It processes BLASTn m6-format alignment output (sample sequences vs. database sequences), filters hits by identity and coverage thresholds, and reports matches to a provided antigen list.

## Dependencies

- Perl (>= 5.10)

## Usage

```bash
perl antigen_screen.pl <blast_m6> <output_file> <identity_threshold> <coverage_threshold> <antigen_list> <sample_name>

##Parameters
Position	Argument	Description
1	blast_m6	BLASTn m6-format alignment result (sample sequences vs. database sequences)
2	output_file	Output file name (e.g. sample.result)
3	identity_threshold	Identity threshold (%) – example: 90
4	coverage_threshold	Coverage threshold – example: 0.9
5	antigen_list	List of antigen sequence names
6	sample_name	Sample name


##Output
Output depends on the classification result:

1 (full-sequence match) → a single non-empty result file.

1* (partial / word-level match) → a non-empty result file plus a sample.result.merge file for auxiliary verification.

Unresolved → an empty result file plus a sample.result.manual file containing sample name, input files, classification level, candidate list with priority (rank, lower value = higher priority, 1 = highest), and parameters for manual review.

See example/README.md for details.
