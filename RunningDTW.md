# Running DTW #

```
python -u search.py <queryList> <refList> [treeFile]
```

Where the `treeFile` is a file where to look for the tree with the indexing of the reference features. If a name is given but no tree is found, one is trained with the reference data and it is stored in the name provided. If no name is given, a default name is used,
and if no tree is found, it is computed and saved for later runs.

The `queryList` and `refList` are two text files with one feature-file per line (full path). Each feature file contains the features in text format, with one dimension per column and as many lines as feature frames. Internally, the code expects these files to be named `<features_path>.pos` and will also try to open a file `<features_path>.sad` to load the speech activity files, composed by a set of 0/1 values indicating, for each frame, whether it is considered speech or silence.
See the below examples of `.sad` and `.pos` files:

typical `.sad` file:
00001111111111111111111111110111111111111

typical `.pos` file:

8.744995e-14 4.590241e-18 4.788485e-06 9.204072e-05 3.005474e-15 7.432372e-15 9.571766e-18 3.566474e-12 2.863539e-16 6.006435e-17 7.827037e-06 4.958612e-06 7.003878e-19 6.641791e-17 1.211917e-21 1.707805e-16 6.386999e-20 4.689712e-25 8.997852e-17 2.424723e-25 7.492112e-72 2.662947e-28 2.847338e-19 1.943968e-24 6.726888e-28 1.238426e-28 3.047493e-18 1.060307e-32 1.366855e-27 5.368839e-24 3a.497585e-16 9.684900e-16 2.579744e-11 2.844339e-22 1.813527e-09 2.315172e-11 1.739866e-15 7.235705e-25 1.933785e-06 6.259972e-18 2.962683e-22 1.673897e-15 1.686069e-15 1.916072e-33 5.194437e-34 3.995280e-37 5.972308e-07 5.892396e-31 2.003480e-34 7.492112e-72
7.659889e-04 8.656478e-06 3.538178e-08 7.652169e-05 7.513226e-05 1.144178e-10 4.964446e-09 8.907847e-17 4.556657e-09 1.145985e-07 6.615825e-08 2.815173e-07 1.860274e-06 6.804312e-06
8.279220e-07 7.047789e-12 6.922832e-01 3.979083e-03 7.897346e-12 1.624714e-09 4.665377e-12 1.956409e-08 6.815599e-09 3.130153e-09 2.268899e-01 7.590290e-02 6.958585e-15 6.269384e-12 4.652817e-16 2.022701e-12 1.855526e-12 2.447941e-16 5.179124e-09 5.734803e-15 6.281622e-27 6.518506e-15 3.228797e-16 7.924112e-20 7.970464e-22 1.501305e-19 9.025719e-14 7.469261e-26 6.263783e-22 7.056545e-18 1.500537e-09 1.299099e-08 8.588020e-06 4.725414e-14 4.022573e-10 1.200463e-09 2.994923e-12 5.244895e-28 5.353953e-08 5.828681e-17 3.430652e-14 1.201565e-17 1.719214e-11 3.540555e-25 4.563279e-24 1.519441e-27 5.180320e-11 2.525710e-27 3.460866e-29 2.253491e-37


The `search.py` script outputs to stdout the results of the search. It is recommended to pipe such result to a log file. In order to convert such file into a `tlist.xml` file (scorable with the NIST STD scripts) we also provide the script `convert2std.pl` that takes the log file and a threshold as an input.
Note that the distances returned by the IR-DTW are first converted to similarities and the threshold is applied to define which results are considered as true results and which are not.


