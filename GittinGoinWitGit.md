# Gittin' Goin' Wit Git #

  * Open up Putty

  * Make a new SSH profile...

> Host Name: islpc19.is.cs.cmu.edu

> Port: **22**

> Give it a name if you like, in the 'Saved Sessions' box, I called mine 'Speech VM.' Click Save, then Open.

  * Login.

  * You'll see this prompt: `speech2013@islpc19:~$`

> If you `ls -l`, you'll see a file called `2-pscr.sh`
> By running this, you'll start the VM...

> Run it with this command: `./2-pscr.sh`

  * After a few seconds, you'll see this:

> `Welcome to Ubuntu 12.04.3 LTS (GNU/Linux 3.8.0-31-generic x86_64)`

> The prompt will read: `pscr@pscr:~$`
> If you want to become root, type: `sudo su`

> The prompt will become: `root@pscr:/home/pscr#`

  * Type:  `cd Desktop/`

> `ls -l` to see the files. You should see the following:
```
   total 20
   drwxrwxrwx 2 pscr pscr 4096 Oct 13 16:37 awb  
   drwxr-xr-x 3 pscr pscr 4096 Oct 13 18:44 clap-applause 
   -rwxr-xr-x 1 root root   89 Oct 13 18:42 git-auth.sh
   drwxr-xr-x 2 root root 4096 Oct 13 19:54 ir-dtw
   drwxrwxr-x 2 pscr pscr 4096 Oct 13 18:18 quicknet 
```
> The folder awb contains all of the Speech Tools, Festival, and Festvox stuff from this website: http://tts.speech.cs.cmu.edu/awb/20130703/

> The folder clap-applause is the repository for the project, cloned from the repository on Google Code. (NOTE: I have added my password credentials to the VM's .netrc file, which means we do **not** have to authenticate any of ourselves ever again on the VM. The commits will all show up as user **pscr**.)

> The folder quicknet contains the **pfile\_utils.tar.gz** and **quicknet.tar.gz** and **AF\_code.tar.gz** compressed bundles from the Quicknet site.

> The git-auth.sh script sets up the authentication for the git repo so you don't have to authenticate. You shouldn't have to use this. It's a run-once type thing unless something screws up.


  * As for using Git, let me show you how it's gonna work...

> Type: `cd /home/pscr/Desktop/clap-applause/`

> Now you're in the repository. Again, we might not even use this location for the repo, but wherever it is, it'll behave the same. First, let's commit to the Google Code repository

  * Type: `vi index.php`

> Hit **i** to get into "insert" mode. You should see `-- INSERT --`  on the bottom. Make any change you like when the editor opens up. It really doesn't matter. Hit **Esc** to get out when you're done, then type **:wq** to save and close the file.

  * Type: `git add .` (note the period)

> This will add whatever changes you made to the local repository.

  * Type: `git commit`

> The "commit message" editor will open up. Git demands that you make commit messages whenever you commit any code. Type a message, any message, but hopefully a useful one when it's a "real" commit, and then hit **Ctrl + X**, then hit **Y**, then hit **Enter**. Your change is committed, but is not synchronized with the Google repo yet...

  * Type: `git push`

> This will send the committed changes to the repository. If for some reason it starts asking you for a username and password, just cd to the `/Desktop` directory above and run the `git-auth.sh` script. (Run: `./git-auth.sh`)

  * Type: `git pull`

> This is going to update the working copy on the VM from the Google Code repository. If you're just doing this, you should see a message: `Already up-to-date`. That is, unless someone made a commit before you did. If any changes have been made, then some merging will have to happen, and hopefully there are no conflicts. We can talk about merging conflicts at a later time, when it happens. But in the meantime.


Note: When you `sudo su` to become root, your commits will show up in the repo as user `root`, not `pscr`.


---


> If you ever need to completely overwrite your repository and update with whatever is the latest version of the code in the repository, run the following command:

```
     git reset --hard HEAD
```

> Okay, so these are all the bread & butter commands you'll need to use Git. you may at some point need to re-clone the repository somewhere. Run the following command:

```
     git clone https://code.google.com/p/clap-applause/
```

> There is no need to use any authentication on the VM. If it asks for username or password, just run the git-auth.sh script.