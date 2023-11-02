> Normal execution

You can use this loop in bash:

```bash
for i in */; do zip -r "${i%/}.zip" "$i"; done
```

`i` is the name of the loop variable. `*/` means every subdirectory of the current directory, and will include a trailing slash in those names. Make sure you `cd` to the right place before executing this. `"$i"` simply names that directory, including trailing slash. The quotation marks ensure that whitespace in the directory name won't cause trouble. `${i%/}` is like `$i` but with the trailing slash removed, so you can use that to construct the name of the zip file.

If you want to see how this works, include an echo before the zip and you will see the commands printed instead of executed.

> Parallel execution

To run them in parallel you can use `&`:
  
```bash
for i in */; do zip -0 -r "${i%/}.zip" "$i" & done; wait
```

We use wait to tell the shell to wait for all background tasks to finish before exiting.

Beware that if you have too many folders in your current directory, then you may overwhelm your computer as this code does not limit the number of parallel tasks.

Better still, 