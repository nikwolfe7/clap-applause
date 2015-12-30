# Pipeline #
## Score Judging ##
  * Input and Target are played for user
    * User ranks how close the Input is to the Target on a scale of 1-10
    * Phrases are randomized
  * Judge ID, phrase ID, the score, and the Input ID are stored into a SQL table
    * The scores are averaged for each phrase and for each Input
    * **Scores** are accumulated and sent to machine learning algorithm to be solved for

## Feature Extraction ##
  * Target is retrieved and Input is recorded
  * Run Praat script to correct sample rate (if necessary)
    * raat <script name> <absolute input directory with trailing "/"> <absolute output directory with trailing />
    * Example: `praat change_sample_rate_of_sound_files.praat /home/pscr/Desktop/quicknet/test/wav/ /home/pscr/Desktop/quicknet/test/wav/new/`
  * Run Prasanna's Neural Network on Input (hopefully already done for Target)
    * Add file name to `txt.done.data`
      * Format: `( filename1`
    * Run `extract_AFs.sh`
      * Automatically creates folders `mcep` (extension .mcep), `AF` (extension .af)
  * Run script to extract F0's
    * Input: .mceps from folder `mcep`
    * Output: .f0
    * Running it (start in subject's folder):
      * `mkdir f0`
      * `./bin/make_f0 wav/*`
  * Convert mcep to ASCII file
    * Input: .mceps from folder `mcep`
    * Output: .mcep
    * Running it (start in subject's folder):
      * `mkdir mcep_ascii`
      * `./bin/convert_mceps_to_ascii.sh`
  * Run script to shorten mcep files to first 12 mceps
    * Input: ASCII .mceps from folder `mcep_ascii`
    * Output: .mcep
    * Running it (start in subject's folder):
      * `mkdir mcep_ascii_short`
      * `./bin/make_melcep_short`
  * Run script to convert shortened **mcep** files binary again
    * Input: shortened .mceps from folder `mcep_ascii_short`
    * Output: .mcep
    * Running it (start in subject's folder):
      * `mkdir mcep_binary_short`
      * `./bin/convert_mceps_to_binary.sh`
  * Create faux label files
    * Input:
    * Output: .lab
    * Running it (start in subject's folder):
      * 
  * Running DTW
    * Input: .lab and .mcep
    * Output:
    * Running it (start in subject's folder):
      * 
  * Combine 12 mceps, AFs, F0 for aligned files
    * Output: .feat
  * Z-score normalize
    * Input: specified
    * Output: same as input
    * Running it:
      * `python zscore.py <relative input directory> <relative output directory> <optional file type>`
        * If no file type is specified, it will z-score all the files in the folder (including the ~'s)
        * Example: `python zscore.py mcep_aligned_rms mcep_zscored mcep`
  * Get Euclidian Distance to combine the 2 files
    * Input: .feat
    * Output: .zdelt
  * Get mean and variance from all features
  * Feed into Wagon
    * Solve for score using all features