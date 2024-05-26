I'll showcase a few points I digged up about the Internal Field Separator, with the help of an example:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="l:o" # works like [:class:], in a sense

read -ra list <<<$hello

printf "%s\n" ${list[@]}
```

`$hello` gets word split based on the current value of IFS, which are `[l:o]`:

```
hel
l
o:worl
d:hel
l
o:worl
d:hel
l
o
```

Because 'l' is currently the IFS, so it won't show, resulting in something close to this:

```
he

o:wor
d:he

o:wor
d:he

o
```

and although `${list[@]}` is not wrapped with double quotes, because the list elements can not be further split based on 'l', they will be displayed as they are now.

am i correct?

