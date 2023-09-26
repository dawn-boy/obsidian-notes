# ssh
ssh is a program used for logging into a remote machine and for executing commands on it. It usually gives a secure encrypted communication between the two insecure or untrusted points, if configured properly.
- ==other services running on different ports can use ssh to tunnel their data securely.==
#### To connect with ssh
```sh
ssh -p port_number -l username destination_URL
```
# find
this finds files really..
```sh
find -user owner -group owningGroup -iname incaseSensitiveNamePattern 2> /dev/null -size {bytes}c
```
# strings
This prints all the printable characters in the file content (ignores all the binary stuffs)
```sh
string fileName
```

# sort
this sorts the file lines (numerically first, then alphabetically)
```sh
sort fileName
```
# uniq
this prints the unique line within the file, to use it properly first sort the file contents
```sh
uniq -u
```
# tr
this just transforms each letters to the other given letter
```sh
tr '[a-z]' '[m-za-l]'
```
# gzip2
decompress a .gz file
```sh
gzip2 -d file.gz
```
# tar
extracts .tar files
```sh
tar --extract -f file
```
# xxd
can revert hex dumps 
```sh
xxd -r file
```
# file
can tell you what type of file it is. ==(really useful for forensics)==
```sh
file filename
```


