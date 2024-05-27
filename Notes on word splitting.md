Example code snippet:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="lo:"

read -ra list <<<"$hello"

printf "%s*" "${list[*]}"
```

1. [Double quotes](#double-quotes)
2. [Bundling into an array](#bundling-into-an-array)
3. [Array expansion re-splitting](#array-expansion-re-splitting)

#### Double quotes

If `$hello` is wrapped with `""`, its literal value will be preserved. Without them, IFS characters will be displayed as blanks spots.

|              With               |             Without             |
| :-----------------------------: | :-----------------------------: |
| `hello:world:hello:world:hello` | `he    w r d he    w r d he   ` |

#### Bundling into an array

`read -ra list` cares not for whether the string is wrapped in quotes. It will split the string into an array regardless.

However, mind that the `read` command reads one line at a time. If the string is multiline, `read` will only read the first line.

#### Array expansion re-splitting

Both `${list[*]}` and `${list[@]}` are prone to re-splitting the array.

| `IFS` \ `printf "%s*" <..>` |                  `${list[*]}`                  |  `${list[@]}`   | `"${list[*]}"`                                  |                 `"${list[@]}"`                  |
| :-------------------------: | :--------------------------------------------: | :-------------: | ----------------------------------------------- | :---------------------------------------------: |
|         `IFS="lo:"`         | `he****w*r*d*he****w*r*d*he**` [(1)](#summary) | [(1)](#summary) | `hellllwlrldlhellllwlrldlhell*` [(2)](#summary) | `he****w*r*d*he****w*r*d*he***` [(3)](#summary) |
|           `IFS=`            |    `he*w*r*d*he*w*r*d*he*` [(4)](#summary)     | [(4)](#summary) | [(2)](#summary)                                 |                 [(3)](#summary)                 |

##### Summary

- `IFS="lo:"`
  1. `*` acts like a delimiter, and fills the gap between each array element. Eg: he~~l~~ \* ~~l~~ \* ~~o~~
  2. The first character of `IFS`, which happens to be `l`, serves as the delimiter for the array elements. The whole string is treated as one element, thus `*` is appended to the very end.
  3. `*` acts normally and is appended to each array element. Eg: he~~l~~ \* ~~l~~ \* ~~o~~ \*
- `IFS=`: The effect this has on word splitting seems to be that it squeezes multiple blank arguments into one.