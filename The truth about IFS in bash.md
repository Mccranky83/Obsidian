I'll showcase a few points I dug up about the Internal Field Separator, with the help of an example:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="l:o" # works like [:class:], in a sense

read -ra list <<<$hello

printf "%s\n" "${list[@]}"
```

`$hello` gets word split based on the current value of IFS, which are 'l', 'o', and ':':

```
hel l o : wo rl d: hel l o : wo rl d: hel l o
```

The whitespace here is used to indicate that the string has been split up into several arguments by the IFS. In reality, 'l', 'o', and ':' are literal values and won't be displayed without being wrapped in double quotes. `echo $hello` should output something like this:

```
he    w r d he    w r d he
```

The final result is this, a total 17 elements in the list:

```
he(l)
(l)
(o)
(:)
w(o)
r(l)
d(:)
he



w
r
d
he


```

##### Extra:

Switch out some sections of the snippet and test it out if you can:

1. `${list[@]}` (or `${list[*]}`, doesn't matter which, as long as no double quotes): Array expansion re-splitting.
2. With or without `\n` in the format specifier.
3. `IFS='h'` and `"${list[*]}"`.
