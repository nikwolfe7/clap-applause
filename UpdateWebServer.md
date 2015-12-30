## Work locally, update easily! ##

So, I wrote a script called `update.sh`, and what it does is `git update` the code repository and put the files that are relevant for the web server in the web server folder. It's sorta dropboxy... but here's what you do...

In our `~/Desktop` folder, there's our repo clap-applause

`cd clap-applause`

Now you're in the repository. Notice that there is now a folder called `/www` in there. This is, in essence, a web deploy folder -- but not really. Think of it like this: Anything you have that you're planning to deploy on the web server, put it in here.

No need to touch anything else here! So...

`cd /media/sf_htdocs/clap-applause`

This is the web server that is pointed to by [our web page!](http://celebrate-language.com/eval)

(You should make yourself root to do this to avoid nasty permission fails. So `sudo su`, la la la...)

Run the following...

`./update.sh`

And you're done! Anything you commit to the git repo on google code in the `/www` folder is now deployed on the web server.

So you can work on your local machine now. Make a change or two, git push it to the repo, then go back to your terminal on the VM and run that `./update.sh` script. It's directory independent so despite the fact that it's in the `/media/sf_htdocs/clap-applause` directory, you can run it from anywhere and it will do the same thing. Just don't delete `git-auth.sh` from the www folder in the repo, because it calls that.

Enjoy!