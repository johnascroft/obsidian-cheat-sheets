# grep

Stands for global regular expression print.

Searches for text patterns in files. Usage:

```bash
$ command -options arguments
```

|-options|description|
|---|---|
|--color|Highlight selected text in a different color|
|-c|Count the number of occurences|
|-n|Print line numbers|

Count the occurrences of "thrid" in files starting with the word "video":

```bash
grep -c "thrid" video*.txt
```

Print the line numbers of the selected occurence:

```bash
grep -n "OfferController->sign" storage/logs/laravel.log
```

Find instances of a search term in a file:

```bash
grep Human characters.txt
```

grep is **case-sensitive**. If you want to ignore case, you can use the `--ignore-case` option:

```bash
grep -i ironman marvel-characters.txt
```

Recursively search through files and directories:

```bash
grep -r "failed to load" /var/log
```