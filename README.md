# antigen_screen.pl

A Perl script for antigen identification from BLASTn results.  
It processes BLASTn m6-format alignment output (sample sequences vs. database sequences), filters hits by identity and coverage thresholds, and reports matches to a provided antigen list.

## Dependencies

- Perl (>= 5.10)

## Usage

```bash
perl antigen_screen.pl <blast_m6> <output_file> <identity_threshold> <coverage_threshold> <antigen_list> <sample_name>
