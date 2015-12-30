# Setting Up the Neural Network to Extract Articulatory Features #

## Downloading the Code ##
Let's assume that you want to run the AF extraction in a directory called `yyy`, then you do:

```
mkdir yyy
cd yyy
$FESTVOXDIR/src/clustergen/setup_cg cmu us yyy
```

This will create a bunch of sub-directories and copy a lot of code into them.

Once you have done this, copy the `AF_nets/` from Prasanna's code to the directory where you ran the `setup_cg` script (This would be `yyy` in our example)
```
cp -r ../AF_Code/AF_nets/ .
```

Also be sure that the following scripts are copied as well:
```
cp ../AF_Extracted/extract_AFs.sh .
cp qnfwds.sh .
```

Change the path and `PROMPTFILE` in `extract_AFs.sh` and `qnfwds.sh` to point to the directories where you have the appropriate code. The code assumes that the paths to binaries in quicknet and pfile\_utils are already in your `$PATH` variable.

## Preparing the Audio ##

Put your audio files in the wav/ directory. The audio files have to be in .wav format. The audio files also have to be 16KHz mono. If they are at some other sampling frequency or if you are unsure, put the wav files in some other directory and then run:
```
./bin/get_wavs   some_other_directory/*.wav
```
This will convert the files to 16KHz mono, power-normalized files and put them in the `wav/` directory automatically

### Vinay's Arctic files ###
```
cp ../AF_Extracted/wav/* wav
```

And their transcriptions:
```
cp ../AF_Extracted/etc/txt.done.data etc
```

## Formatting the scripts ##
In all scripts written for Festival, we assume that the transcripts for all the wav files are in the file `txt.done.data` in the `etc/` directory. The `txt.done.data` file typically looks like this:
```
( filename1 " transcript 1 ")
( filename2 " transcript 2 ")
....
```
There's a sample `txt.done.data` file in the project's Drive folder.
https://docs.google.com/file/d/0Bzfw-X-bLorBMFk0Z2dqYzRYT2c/edit?usp=sharing

For your task, we don't have transcripts but all my scripts still use the `txt.done.data` file to know what files will need processing. So, create a file called `txt.done.data` and put it in the `etc/` directory. The file should look like this:
```
( filename1
( filename2
....
```
Note that there are no extensions in the filenames. If your wav file is called something like `blah_0001.wav`. The entry in the `txt.done.data` file will be:
```
( blah_0001
```

## Running the Melcep and AF Extractor ##
You can now run the `extract_AFs.sh` code in the `yyy` directory. This will create a melcep static directory and automatically extract the **Mel Cepstral Coefficients** from the wav files, use the neural nets to predict the values of the AFs and put the predicted AFs corresponding to each file in a new directory called AF.

**Note:** The articulatory features are trained on English.

