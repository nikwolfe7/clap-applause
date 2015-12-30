# Preparing to Run DTW after Getting Mceps, f0s and AFs #
**Note:** These steps are to be done once you are in the subject/person's folder.

Run the script to convert Prasanna's mcep files to ASCII:
```
mkdir mcep_ascii
./bin/convert_mceps_to_ascii.sh
```

Then just extract the first 12 mceps.
```
mkdir mcep_ascii_short
./bin/make_melcep_short
```

Then convert this shortened mcep file to binary again.
```
mkdir mcep_binary_short
./bin/convert_mceps_to_binary.sh
```

Run the script to convert f0s to ascii
```
mkdir f0_ascii
./bin/convert_f0_to_ascii.sh
```

Align AFs and Mceps
```
./bin/make_mcep_AF_equal.sh
```

# Running DTW #
```
./bin/do_build build_prompts
./bin/do_build label
mkdir dtw_out
./bin/do_dtw
```

# Getting the aligned mceps, AFs and f0s using DTW backpointers #
```
mkdir mcep_aligned_rms
./bin/make_dtw_aligned_rms_mceps.sh
```
```
mkdir AF_aligned_rms
./bin/make_dtw_aligned_rms_AFs.sh
```
```
mkdir f0_aligned_rms
./bin/make_dtw_aligned_rms_f0s.sh
```