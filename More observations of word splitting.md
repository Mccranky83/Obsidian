Example code snippet:

```bash
#!/usr/bin/env -S bash

hello="hello:world:hello:world:hello"

IFS="lo:"

read -ra list <<<"$hello"

printf "%s\n" ${list[*]}
```

f

