```bash
brew install xpdf
pdftotext file.pdf - | iconv -t UTF-8//IGNORE | say
```

If `xpdf` is not installed, then an alternative to `xpdf` would be `brew install poppler`. Poppler also installs `pdftotext` utility.