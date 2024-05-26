I'll showcase a few points I digged up about the Internal Field Separator, with the help of an example:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="l:o" # works like [:class:], in a sense

read -ra list <<<$hello

printf "%s\n" ${list[@]}
```

`$hello` gets word split based on the current value of IFS, which are 'l', 'o', and ':':

```
hel l o : wo rl d: hel l o : wo rl d: hel l o
```

The whitespace here is used to indicate that the string has been split up into several arguments by the IFS. In reality, 'l', 'o', and ':' are literal values and won't be displayed without being wrapped in double quotes.

Because 'l' is currently the IFS, it's literal value won't be displayed, and it leaves behind a blank space:

```
he    w r d he    w r d he
he o:wor
d:he

o:wor
d:he

o
```

and although `${list[@]}` is not wrapped with double quotes, because the list elements can not be further split based on 'l', they will be displayed as they are now.

am i correct?

