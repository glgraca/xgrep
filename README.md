
# grepp (grep++)

This is a very simple solution to a problem that had been bothering me for a long time. I wanted grep to allow to me to print more complex output using capturing groups.

In order to have the flexibility that Perl offers but at the same time keep the command line simple, I wrote this little script.

It takes 3 arguments; only the first one is mandatory.

```sh
$grepp
Usage: grepp regex [output] [filename]

$grepp 'sequence=(\d+)' '$1\n' log.txt
20
30
40

$cat log.txt | grepp 'sequence=(\d+)' '$1,'
20,30,40,

$cat log.txt | grepp 'sequence=(\d+)' 
sequence=20
sequence=30
sequence=40

$gunzip -c data.log.gz | grepp 'id=(\d+)' '$1,'
150647,160346,150648,160347,160348,150649,

$gunzip -c data.log.gz | grepp 'id=(\d+) val=(\d+)' '$1=$2\n'
150647=7
160346=9
150648=4
160347=5

$grepp 'enabled=(\w+)' '$filename: $1\n' *.ini
abc.ini: true
xyz.ini: false

$grepp 'weight=(\d+) items=(\d+)' '@{[$1*$2]}' data.txt
34
110

$grepp while '$filename($lineno): $_' grepp
grepp(22):   while(<$fh>) {

```

If there are two arguments it checks if the second argument is a file and if the file doesn't exist the script simply reads from STDIN.

If you specify output you have to include a newline if you want one. Otherwise, it will print out each line just as grep does.

You can use any Perl expression as output; these are the variables you will most likely need:

| Variable | Meaning |
| :----- | :----- |
| $1, $2, etc. | Regexp groupings |
| $filename | The current filename |
| $lineno | The current line number in the current file |
| $_ | The whole line that was matched (includes the trailing newline) |
