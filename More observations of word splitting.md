Example code snippet:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="lo:"

read -ra list <<<"$hello"

printf "%s\n" ${list[*]}
```

1. [Double quotes](#double-quotes)

#### Double quotes

If `$hello` is wrapped with `""`, its literal value will be preserved. Without them, IFS characters will be displayed as blanks spots.

|              With               |             Without             |
| :-----------------------------: | :-----------------------------: |
| `hello:world:hello:world:hello` | `he    w r d he    w r d he   ` |

2. Bundling into an array

`read -ra list` cares not for whether the string is wrapped in quotes. It will split the string into an array regardless.

However, mind that the `read` command reads one line at a time. If the string is multiline, `read` will only read the first line.
