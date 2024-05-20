```bash
printf "%.0s[=*n]" $(seq 5)
```
- `'=%.0s'`: `.0s` is a format specifier that tells `printf` to print the string argument exactly 0 times.