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

