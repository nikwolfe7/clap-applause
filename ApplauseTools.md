# Applause Tools #

We have a few tools at our disposal now in the `/bin` folder in the Applause root folder (`/applause`). Here is a brief description of how they work...

## config.sh ##
Usage:
```
source config.sh
```
This script is referred to by all relevant pipeline scripts. It contains all of the directory specifics for the applause application, and the FESTIVAL tools. Ideally one would use this to set things up on a new machine. Unfortunately, the path to this script must be pointed to at the top of most of the scripts below. Check and see before running things.

## gitup.sh ##
Usage:
```
./bin/gitup.sh
```
This does the essential commands for a `git push` without unintentionally destroying the repository, or your local copy. (It also authorizes you to push to the repository without supplying a password.) It will fail if you have not updated your project to the most recent version.

## update.sh ##
Usage:
```
./bin/update.sh
```
Performs a `git pull` and moves scripts around to their respective directories (for instance the web server, which is not under version control). It also runs `misc_updates.sh` so if you have additional things to do on every update, put them there instead of changing `update.sh`. This is mostly intended to work on the server, but it will work on your local copy as well. It just won't move things around outside of your repository folder.

## user\_setup.sh ##
Usage:
```
./bin/user_setup.sh [user]
```
This script takes a username (NOT a directory) and sets up a new user profile with all of the festival, festvox, speech tools, articulatory features neural network stuff, and required scripts and directories for our audio processing pipeline. Run this to create a new user.

## run\_pipeline.sh ##
Usage:
```
./bin/run_pipeline.sh [user] [target]
```
This runs our audio processing pipeline on the data for a specified user (NOT a directory) and target speaker to compare against. At the end of running this, all mceps, f0s, AFs, and final feature vectors will be processed. This script grabs whatever is in the `/recording` directory of the user, combined with the information in `/etc/txt.done.data`.

## build\_tree.sh ##
Usage:
```
./bin/build_tree.sh [target]
```
This takes the processed data in each user's `/cfeats_ascii_final` directory and re-builds the CART tree. The target user that all speakers are compared against must be passed as an argument. This will output the combined features into a file called `utterance_vectors.data` in the `/cart` directory

## nuclear\_reboot.sh ##
Usage:
```
./bin/nuclear_reboot.sh [target]
```
This is the big kahuna burger. Given a target user to compare against, this script...
  1. Saves the audio and transcript files in all currently existing user directories
  1. Completely destroys the existing user directories
  1. Runs `user_setup.sh` on all former usernames
  1. Runs `run_pipeline.sh` on all users against the target passed to the script as an argument, regenerating all data.
  1. Runs `build_tree.sh` on the processed data, re-creating the CART tree.

**Do NOT use this unless you know EXACTLY what it does!!**