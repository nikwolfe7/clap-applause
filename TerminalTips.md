# Terminal Tips #

## Copying to the VM ##
  1. Copy from personal computer to speech2013@islpc19.is.cs.cmu.edu
  1. `scp` from `islpc19` to `pscr@192.168.56.102:~`

The `:~` will put the file(s) in the home directory on the VM. You can change this.

Then **you must delete your files** from islpc19.


---

## Split Screen in Vim/Vi ##
```
:vsp [your file]
```

Example:
```
:vsp etc/txt.done.data
```


---

## Run a Process in the Background ##
```
nohup [nice] <program> &
```

`nice` is an optional argument that will put the process on a lower priority.
**NOTE:** The `&` is the actual command to run it in the background, without it, `nohup` will not know this.

`exit` or **CTRL+D** will let you leave the remote server.


---

## Comparing Two Files in Vim ##
```
vimdiff <file1> <file2> [file3 [file4]]
```