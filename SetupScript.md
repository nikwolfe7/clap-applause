# Applause Installation Script #

We can now install an entire directory structure (up to the point we have currently reached in the pipeline) including all scripts with a single unified script.

## Creating a New User ##

You will notice in our directory structure, inside of `~/CART` there is now a folder called `resources`. From now on, any and all scripts you write to work on the pipeline should be placed in this directory. You can peruse the folder to see what's inside. I have also moved the `/quicknets` directory here and changed the `extract_AFs.sh` script to point to this directory. This is simply for coherence; keeping things on the Desktop is kinda ugly. The Festvox install will likely have to move as well, but we can deal with that later.

One additional change is that the scripts that do all this magic are now in the `bin` directory in `/CART`.

To create a new user...

```
cd ~/CART

./bin/user_setup.sh [user]
```

For example:

```
./user_setup.sh vinay
```

This will create everything you need (with the exception of copying audio!) into a folder called 'vinay' inside the `~/CART` directory. Try it for yourself and see! I did not copy the audio because as this transforms into a real application we will need to be dynamically collecting audio from the web and stuffing it into the `[user]/recordings` folder. From there we will be running the pipeline. That is a separate script.

You can also use this from the web.

[celebrate-language.com/eval](http://celebrate-language.com/eval)