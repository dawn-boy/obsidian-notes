Bash (Bourne again shell) resides at /bin/bash. It's a scripting language meaning it doesn't need to compile to run.
#### Ways to run the script
- bash script.sh (arguments)
- ./script.sh --> needs to have the execute bit turned on for script.sh
- sh script.sh (arguments)
***
# The Within side
## Shebang
```sh
#!/bin/bash
```
This let's the terminal know the location of the interpreter and is always specified on the top of the script.
## echo
```bash
echo -e "Helloworld\n"
```
-e --> enables for interpretation for backward slash escapes.
## Decision-making  
```bash
if [ condition ]
then
	statements
 
elif [ condition ]
then 
	statements
 
else
	statements
 
fi
```
==don't forget the spaces between the condition and the square bracs.==

```sh
if [[ '$1' == 'whatever']]
```
==string comparisions can be done only within double brackets.==

if the variable is given within quotes, then the if statement is looking for a string datatype to compare it with.
## operators
### string operators
```
== --> is equal to
!= --> is not equal to
<  --> is lesser than ASCII value
>  --> is greater than ASCII value

-z --> if string is null
-n --> if string is not null
```
==string comparisions can be done only inside (within two square brackets)==

### integer operators
```
-eq --> is equal to
-ne --> is not equal to

-gt --> is greater than
-ge --> is greater than or equal to

-lt --> is lesser than 
-le --> is lesser than or equal to
```
### file operators
```
-e --> if the file exist
-f --> tests if it's a file
-d --> tests if it's a dictionary
-L --> tests if it's a symbolic link
-N --> checks if the file was modified after the last read
-O --> checks if the current user owns the file
-G --> checks if the file's group id matches the current user's
-s --> tests if the file has size greater than 0
-r --> tests if the file has read permission
-w --> tests if the file has write permission
-x --> tests if the file has execute permission
```
### logical operators
```
!  --> logical negotiation NOT (just flips the bool)
&& --> logical AND
|| --> logical OR
```
## arguments
a bash script can take upto 9 arguments and they are stored in these reserved variables.
```
$0 --> executed script name
$1 --> argument 1
$2 --> argument 2
$3 --> argument 3
$4 --> argument 4
$5 --> argument 5
$6 --> argument 6
$7 --> argument 7
$8 --> argument 8
$9 --> argument 9
```
## special variables
```
$# --> holds the no. of arguments passed to the script
$@ --> used to retrieve the list of command-line arguments
$n --> used to retrieve the passed arguments in order (n=1--9)
$$ --> holds the process id of currently executing process
$? --> holds the exit status of the script.
(0 --> success, 1 --> failure)

```
## variable
```sh
var_name='string'
var_name=$another_var
echo $var_name
```
mind you, the spaces after and before the equal to sign.
## arrays
```bash
arrays=(element1 element2 "element3 uh with a space" element4 element5)
echo ${arrays[0]}
```
mind you, the index starts at 0 as customary.
curly brackets are used for variable expansion.

## arithmetic 
```sh
$((10 + 10))
((var_num++))
```
arithmetic is always done within two parenthesis.

```sh
${#variable}
```
this counts total number of charactes in the variable.
