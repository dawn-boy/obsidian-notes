## Shebang
```sh
# This let's the terminal know the location of the interpreter and is always specified on the top of the script.

#!/bin/bash
```
## echo
```bash
# -e enables for interpretation for backward slash escapes.
echo -e "Helloworld\n"
```
## variable declaration
```sh
# note there is no space before and after the equal sign.
FIRST_NAME=someName
LAST_NAME=someLstName

echo Hi $FIRST_NAME $LAST_NAME
```
## positional arguments
```sh
echo $0 $1 $2 $3 $4 $5
```
## user input
```sh
echo What is thy name?
read FIRST_NAME
echo what is thy last name?
read LAST_NAME

echo Hello there, $FIRST_NAME $LAST_NAME
```
## Decision-making 
```bash
# don't forget the spaces between the condition and the square bracs.
 
if [ condition ];
then
	statements
 
elif [ condition ];
then 
	statements
 
else
	statements
fi
```
## case statements
```sh
#!/bin/bash

case $variable in 
pattern1)
	statements
	;;
pattern2)
	statements
	;;
pattern3)
	statements
	;;
*)
	#anything else
	statements
	;;
esac
```
## arrays
```sh
MY_FIRST_LIST=(one two three four 'finee five' six)
# will give the first element
echo $MY_FIRST_LIST
# will give the indexed element
echo ${MY_FIRST_LIST[3]}
# will give the entire list
echo ${MY_FIRST_LIST[@]}

# note: {} means variable expansion
```
### Associative arrays
```sh
declare -A dict_name=([key1]=value1 [key2]=value2)

echo ${dict_name[key]}

for key in "${!dict_name[@]}"
do
	echo $key
done

for value in "${dict_name[@]}"
do
	echo $value
done
```

### variable expansion vs calling a variable
```sh
# this is variable expansion
${var_name}
# this executes the command returns its output
$(cmd)
# this calls the variable
$var_name
```
## for loop
```sh
for item in $LIST;
do 
	statements;
done

# give it a range
for loop in 'seq 1 33';
do 
	statements;
done

# a list of elements read from a file
for ip in $(cat ip_list.txt);
do 
	statements;
done

```
## functions
```sh
showuptime(){
	up=$(uptime -p | cut -c4-)
	since=$(uptime -s)
	cat << EOF
-----
This machine has been up for $up
THis machine has been running since $since
-----
EOF
}

showuptime
```
### passing parameters to function
```sh
showuptime(){
	echo $1 $0
}
showuptime yeah adi

# output --> yeah adi
```
### not change the global variables value
```sh
num=1
function(){
	# this won't change the global num
	local num=0
	echo $num
	# output is 0
}
echo $num
# output is 1
```

```sh
showname(){
	echo hello $1
	if [${1,,} = adi ]; then
		return 0
	else
		return 1
	fi
}

showname $1
# $? refers to the execution code of the previously executed process
if [$? = 1]; then
	echo 'Someone snooping in, unknown, for now.'
fi
```
## awk
```sh
# by default, awk splits the contents based on a space. This command give the 2 element. Indexing starts at 1(radicul, ik).
awk '{print $2}' fileName

# you can pass the separator char with -F option
awk -F, '{print $1}' mama.csv
```
## sed
```sh
# s means substitute, g means affect globally 
# this outputs the result to screen, no changes made in the file
sed 's/wordToReplace/wordToReplaceWith/g'

# this makes changes in the original file and creates a backup file of original contents if any suffix is given after -i option.
sed 's/sanity/humanity/g' sedTest -i.original

```