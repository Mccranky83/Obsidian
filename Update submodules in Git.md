> Only works interchangeably when submodules each have only one branch

Method 1:
```sh
git submodule foreach --recursive git pull
```

Method 2:
```sh
git submodule update --remote --merge
```