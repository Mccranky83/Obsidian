```bash
foo1="hello"
foo2="there"

for var in "${!foo@}"; do
	echo "$var: ${!var}"
done
```
