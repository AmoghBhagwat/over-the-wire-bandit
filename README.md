# Level 0 -> Level 1

```
cat readme
```
Prints the password of next level

# Level 1 -> Level 2
```
cat ./-
``` 

```./-``` is needed because writing ```cat -``` is used to specify parameters. ```./``` gives the absolute path of the file.

# Level 2 -> Level 3
```
cat 'spaces in this filename'
```

For specifying a filename with spaces, we can write the entire filename in quotes.

# Level 3 -> Level 4

```
cd inhere
ls -a
cat .hidden
```

```ls -a``` lists all the files in the directory, including hidden files. From this, we get to know the name of the hidden file containing the password, which happens to be ```.hidden```

# Level 4 -> Level 5

```
cd inhere
file ./-file00
file ./-file01
file ./-file02
file ./-file03
file ./-file04
file ./-file05
file ./-file06
file ./-file07
file ./-file08
file ./-file09
cat ./-file07
```

```file <filename>``` prints the type of data stored in the file. Only ```-file07``` has ASCII text, which is human readable. So the password is stored in this file.

# Level 5 -> Level 6

```
cd inhere
find ./ -size 1033c -type f ! -executable
cat ./maybehere07/.file2
```

```find ./ -size 1033c -type f ! -executable``` finds all the files in current directory (```./```), with size 1033c (c specifies bytes). ```-type f``` specifies that we have to find a regular file, not a directory. ```! -executable``` means that the file should not be executable. 

# Level 6 -> Level 7
```
cd /
find ./ -size 33c -user bandit7 -group bandit6
cat ./var/lib/dpkg/info/bandit7.password
```

This finds in the entire disk the file with given properties. We get multiple lines of output, but all of them except one give the error "Permission Denied". The only file which does not give any error is ```./var/lib/dpkg/info/bandit7.password```. This file contains the password.

# Level 7 -> Level 8
```
grep 'millionth' data.txt
```

```grep``` finds the specified pattern in the text.

# Level 8 -> Level 9
```
cat data.txt | sort | uniq -c | grep '1'
```

We redirect the contents of the file to sort, which sorts it. Then we use the ```uniq -c``` command to print the count of unique adjacent lines, in which we search "1 ", for the line which has only 1 occurrence.

# Level 9 -> Level 10
```
strings data.txt | grep '======'
```
strings command prints all the human readable lines of the file, and we use the grep command to print the lines starting with few = signs.

# Level 10 -> Level 11
```
base64 --decode data.txt
```

Decodes the encoded data.

# Level 11 -> Level 12
```
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
Rotates the file contents by 13. (rotating alphabets by 13 twice results in the same alphabets again)

# Level 12 -> Level 13
```
cp data.txt /tmp/amogh/data.txt
xxd -r data.txt > data.bin
file data.bin
gzip -d -c data.bin > data1
file data1
bzip2 -d -c data1 > data2
file data2
gzip -d -c dara2 > data3
file data3
tar -xvf data3
file data5.bin
tar -xvf data5.bin
file data6.bin
bzip2 -d -c data6.bin > data7.bin
file data7.bin
tar -xvf data7.bin
file data8.bin
gzip -d -c data8.bin > data9.bin
file data9.bin
cat data9.bin
```
We first copy the file to working directory, and reverse the hex dump into a new file. Then we check the type of the file and decompress it accordingly until the type of the output file is ASCII text.
