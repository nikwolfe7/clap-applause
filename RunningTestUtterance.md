# Testing an Utterance with the CART Tree #

Yay, we can test real utterances now!

## test\_utterance.sh ##

This script takes as arguments
  1. The SRC user
  1. The Target user
  1. The utterance key, e.g. arctic\_a0001 (NO file extension!)

Usage:
```
cd ~/applause
./bin/test_utterance.sh nmw rms arctic_a0002
```

This script assumes that `nmw` has placed `arctic_a0002` in the `/uploads` directory in the `~/applause` home directory. When the web app plugs into this, calling this script remotely will execute the script, run through the pipeline, and return a score. But this produces a lot of output. So there's also this:

## run\_test\_utterance.sh ##

This script takes as arguments
  1. The SRC user
  1. The utterance key, e.g. arctic\_a0001 (NO file extension!)

The code:
```
#==============================================================#
# Run Test Utterance
#==============================================================#
# 1.) is the user
# 2.) is the utterance, e.g. arctic_a0001
#
cp /media/sf_pscoringData/$1/khz16/$2.wav ~/applause/uploads
cd ~/applause/ 
OUT=$(./bin/test_utterance.sh nmw rms $2)
echo "Predicted Score: "$OUT
```

This makes it easier because it automatically copies the audio you request into the /uploads folder so you can run the script. This is for testing on the server, mostly, though it may be used otherwise. As you can see, this script also assumes that `rms` is the TARGET voice.

The output, for the following:
```
./bin/run_test_utterance nmw arctic_a0001
```
...is this:
```
Predicted Score: 2.22917
```
There's a `mv` command somewhere that's complaining too, but that's basically it. The result! Yay!

Try it yourself!