# xgrep

This is a very simple solution to a problem that had been bothering me for a long time. I wanted grep to allow to me to print more complex output using capturing groups.

In order to have the flexibility that Perl offers but at the same time keep the command line simple, I wrote this little script.

It takes 3 arguments; only the first one if obligatory.

```sh
$xgrep 'sequence=(\d+)' '$1\n' log.txt
20
30
40

$cat log.txt | xgrep 'sequence=(\d+)' '$1,'
20,30,40,

$cat log.txt | xgrep 'sequence=(\d+)' 
sequence=20
sequence=30
sequence=40

```

If there are two arguments it checks if the second argument is a file and, if it doesn't exist, the script simply reads from STDIN.

If you specify output, you have to include a newline if you want one. Otherwise, it will print out each line just as grep does.
