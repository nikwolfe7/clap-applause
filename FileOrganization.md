# Applause File Structure #

For our audio, documentation, scripts, and so on, our entire application directory structure will be organized in the data storage directory as follows...

### Root Application Folder ###

In our case, this is `pscoringData`. Currently all of our `awb/rms/bdl` etc. audio is in this root directory along with our evaluation test results and so on. Also contained in the root are the python scripts we have to crawl the web and download stuff into our target audio directory.

### Target Audio / Data ###

```
[root folder]/language-resources
```

All audio, features, and recordings of TARGET audio will be contained in this directory.

### Individual Languages ###

```
[root folder]/language-resources/
    [language-name]/
        audio/
        docs/
        feats/
        misc/
        scripts/
```

**Nothing besides language data and possibly a script or two belongs in this directory!! NO folders with other types of data at all!!**

The naming convention for new languages is all lower-case, and if multiple words are required they are to be separated by a dash (-). Within each language directory is an `audio` folder (self explanatory), a `scripts` folder, containing all .xls and .csv files pertaining to the language lesson scripts for that language, a `docs` folder containing all .pdf and .doc files with info about the language, a `feats` folder containing all extracted features for the target audio, and finally, a `misc` folder, with any miscellaneous other items we may accumulate for a given language.

### Backup ###

```
[root-folder]/language-resources-backup/
```

Self explanatory. in the `root folder` there's a script `backup-lang-data.sh` that will back up all data from the `language-resources` folder into the backup folder.

### User Data ###

