```zsh
find . -type f -regex '\./[0-9]*\.zip' -exec sh -c 'mv "$1" "$(printf "第%02d卷.cbz" $(basename -s .zip "$1"))"' _ {} \;_
```