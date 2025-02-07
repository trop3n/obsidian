> **Bash** is a scripting language we use to communicate with Unix-based OS and give commands to the system. 

Since May 2019, Windows provides a **Windows Subsystem for Linux** that allows us to use `Bash` in a Windows environment. It is essential to master the language to work effectively with it.

The main difference between *scripting and programming languages*:

- Scripting languages don't need to compile the code to execute the scripting language.

> As penetration testers, we must be able to work with any operating system, whether it is Windows or Unix-based. 
> 	Efficiency depends mainly on the knowledge of the systems, especially in the *privilege escalation field.* 

On Unix-based systems, it is essential to learn how to use the terminal, filter data, and automate these processes. 

- Especially in large Unix-based enterprise networks, we will have to deal with large amounts of data. We have to *sort and filter out accordingly to determine potential gaps and information as fast as possible.* 

> It is also essential to learn how to combine several commands and work with individual results. This is where scripting comes in, increasing our speed and efficiency. 

Like a programming language, a scripting language has almost the same structure, which can be divided into:

- `Input & Output`
- `Arguments, Variables and Arrays`
- `Conditional execution`
- `Arithmetic`
- `Loops`
- `Comparison Operators`
- `Functions`

> It is often common to automate some processes not to repeat them all the time and filter large amounts of information. 

In general, *a script does not create a process, but it is executed by the interpreter that executes the script* in this case, the Bash.

### Script Execution - Examples

```shell
trop3n@htb[/htb]$ bash script.sh <optional arguments>
```
`
```shell
trop3n@htb[/htb]$ sh script.sh <optional arguments>
```

```shell
trop3n@htb[/htb]$ ./script.sh <optional arguments>
```

Let us look at such a script and see how they can be created to get specific results. If we execute this script and specify a domain, we see what information this script provides.

#### CIDR.sh

```shell
trop3n@htb[/htb]$ ./CIDR.sh inlanefreight.com

Discovered IP address(es):
165.22.119.202

Additional options available:
	1) Identify the corresponding network range of target domain.
	2) Ping discovered hosts.
	3) All checks.
	*) Exit.

Select your option: 3

NetRange for 165.22.119.202:
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16

Pinging host(s):
165.22.119.202 is up.

1 out of 1 hosts are up.
```

Now let us look at that script in detail and read it line by line in the best possible way. In the next sections, we will look at and analyze all the parts of this script.

```bash
#!/bin/bash

# Check for given arguments
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}

# Ping discovered IP address(es)
function ping_host {
	hosts_up=0
	hosts_total=0
	
	echo -e "\nPinging host(s):"
	for host in $cidr_ips
	do
		stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
	done
	
	echo -e "\n$hosts_up out of $hosts_total hosts are up."
}

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

echo -e "Discovered IP address:\n$hosts\n"
ipaddr=$(host $domain | grep "has address" | cut -d" " -f4 | tr "\n" " ")

# Available options
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```

As we can see, we have commented here several parts of the script into which we can split it.

1. `Check for given arguments`
2. `Identify network range for the specified IP addresses`
3. `Ping discovered IP addresses`
4. `Identify IP addresses of the specified domain`
5. `Available options`

### 1. Check for given arguments

> In the first part of the script, we have an if-else statement that checks if we have specified a domain representing the target company.

### 2. Identify network range for the specified IP address

> Here we have created a function that makes a "whois" query for each IP address and displays the line for the reserved network range, and stores it in the CIDR.txt

### 3. Ping discovered IP addresses

> This additional function is used to check if the found hosts are reachable with the respective IP addresses. With the For-Loop, we ping every IP address in the network range and count the results.

### 4. Identify IP addresses of each specified domain

> As the first step in this script, we identify the IPv4 address of the domain returned to us.

### 5. Available options

> Then we decide which functions we want to use to find out more information about the infrastructure.

# Conditional Execution

> **Conditional Execution** allows us to control the flow of our script by reaching different conditions.

- This function is one the essential components, otherwise, we could only execute one command after another.

When defining various conditions, we specify which functions or sections of code should be executed for a specific value. If we reach a specific condition, only the code for that condition is executed, and the others are skipped. 

As soon as the code section is completed, the following commands will be executed outside the conditional execution. Let us look at the first part of the script again and analyze it.

```bash
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

<SNIP>
```

In summary, this code section works with the following components:

- `#!/bin/bash` - Shebang
- `if-else-fi` - Conditional execution.
- `echo` - Prints specific output
- `$#` / `$0` / `$1` - Special variables
- `domain` - variables

> The **conditions** of the conditional executions can be defined using **variables** (`$#`. `$0`, `$1`, `domain`), values (`0`), and strings, as we will see in the next examples. 

### Shebang

> The shebang line is always at the top of each script and always starts with "`#!`" . This line contains the path to the specified interpreter (`/bin/bash`) with which the script is executed. 

We can also use Shebang to define other interpreters like Python, Perl and others.

```python
#!/usr/bin/env python
```

```perl
#!/usr/bin/env perl
```

### If-Else-Fi

> One of the most fundamental programming tasks is to check different conditions to deal with these. Checking of conditions usually has two different forms in programming and scripting languages:

- The `if-else conition` and `case statements`

```bash
if [ the number of given arguments equals 0 ]
then
	Print: "You need to specify the target domain."
	Print: "<empty line>"
	Print: "Usage:"
	Print: "   <name of the script> <domain>"
	Exit the script with an error
else
	The "domain" variable serves as the alias for the given argument 
finish the if-condition
```

> By default, an `if-else` condition can contain only a single `if`, as shown in the next example.

### If-Only.sh

```bash
#!/bin/bash

value-$1

if [ $value -gt "10" ]
then
    echo "Given argument is greater than 10."
fi
```

### If-Only.sh - Execution

```bash
trop3n@htb[/htb]$ bash if-only.sh 5
```
> No output, the condition was not met. 
```bash
trop3n@htb[/htb]$ bash if-only.sh 12

Given argument is greater than 10.
```

> When adding `Elif` or `Else`, we add alternatives to treat specific values or statuses. If a particular value does not apply to the first case, it will be caught by others. 

### If-Elif-Else.sh

```bash
#!/bin/.bash

value=$1

if [ $value -gt "10" ]
then
    echo "Given argument is greater than 10."
elif [ $value -lt "10" ]
then
    echo "Given argument is less than 10."
else
    echo "Given argument is not a number."
fi
```

#### If-Elif-Else.sh - Execution

```bash
trop3n@htb[/htb]$ bash if-elif-else.sh 5

Given argument is less than 10.
```

```bash
trop3n@htb[/htb]$ bash if-elif-else.sh 12

Given argument is greater than 10.
```

```bash
trop3n@htb[/htb]$ bash if-elif-else.sh HTB

if-elif-else.sh: line 5: [: HTB: integer expression expected
if-elif-else.sh: line 8: [: HTB: integer expression expected
Given argument is not a number.
```

> This script could be expanded and specify several conditions. This could look something like this:

#### Several Conditions - Script.sh

```bash
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
elif [ $# -eq 1 ]
then
	domain=$1
else
	echo -e "Too many arguments given."
	exit 1
fi

<SNIP>
```

> Here we define another condition (`elif [<condition>]; then`) that prints a line telling us (`echo -e "..."`) that we have given more than one argument and exits the program with an error. (`exit 1`).

#### Exercise Script

```bash
#!/bin/bash

# Count number of characters in a variable:
#     echo $variable | wc -c
# Variable to encode

var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..40}
do
        var=$(echo $var | base64)
        if [ $counter -eq 35 ];then
            echo $var | wc -c
        fi
done
```

> Create an `"If-Else"` condition in the `"For"-Loop` of the "Exercise Script" that prints you the number of characters of the 35th generated value of the variable "var". Submit the number as the answer.

Answer: 1197735

# Arguments, Variables and Arrays

> The advantage of bash scripts is that we can always pass up to 9 arguments (`$0-$9`) to the script without assigning them to variables or setting the corresponding requirements for these. 

- `9 arguments` because the first argument, `$0`, is reserved for the script. 

As we can see here, we need the dollar sign `$` before the name of the variable to use it at the specified position. The assignment would look like this in comparison.

```bash
trop3n@htb[/htb]$ ./script.sh ARG1 ARG2 ARG3 ... ARG9
       ASSIGNMENTS:       $0      $1   $2   $3 ...   $9
```

> This means that we have automatically assigned the corresponding arguments to the predefined variables in this place. 

These variables are called **special variables**. These special variables serve as *placeholders.*

- If we look at the code section again, we will see where each and which arguments have been used.

#### CIDR.sh

```bash
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

<SNIP>
```

> There are several ways how we can execute our script. However, we must first set the script's execution privileges before executing it with the interpreter defined in it.

```shell-session
trop3n@htb[/htb]$ chmod +x cidr.sh
```

> `chmod` stands for "**CHange MODe**" and is used to change permissions for a file or directory on a Unix machine.
#### Options Available for the Linux `chmod` Command

|Options|Description|
|---|---|
|`-R`|Apply the permission change recursively to all the files and directories within the specified directory.|
|`-v`|It will display a message for each file that is processed. while indicating the permission change that was made.|
|`-c`|It works same as ****`-v`**** but in this case it only displays messages for files whose permission is changed.|
|`-f`|It helps in avoiding display of error messages.|
|`-h`|Change the permissions of symbolic links instead of the files they point to.|
#### CIDR.sh - Execution without Arguments

```bash
trop3n@htb[/htb]$ ./cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```

#### CIDR.sh - Execution without Execution Permissions

```bash
trop3n@htb[/htb]$ bash cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```

### Special Variables

> Special variables use the `Internal Field Separator` (**IFS**) to identify when an argument ends and the next begins. Bash provides various special variables that assist while scripting. 

Some of these variables are:

| IFS  | Description                                                                                                                                                             |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$#` | This variable holds the number of arguments passed to the script.                                                                                                       |
| `$@` | This variable can be used to retrieve the list of command-line arguments.                                                                                               |
| `$n` | Each command-line argument can be selectively retrieved using its position. For example, the first argument is found at `$1`.                                           |
| `$$` | The process ID of the currently executing process                                                                                                                       |
| `$?` | The exit status of the script. This variable is useful to determine a command's success. The value 0 represents successful execution, while 1 is a result of a failure. |
> Of the ones shown above, we have 3 such special variables in our `if-else` condition.

| IFS  | Description                                                                                                                                                                                                                                            |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `$#` | In this case, we need just one variable that needs to be assigned to the `domain` variable. This variable is used to specify the target we want to work with. If we provide just an FQDN as the argument, the `$#` variable will return a value of `1` |
| `$0` | This special variable is assigned the name of the executed script, which is then shown in the `Usage:` example.                                                                                                                                        |
| `$!` | Separated by a space, the first argument is assigned to that special variable.                                                                                                                                                                         |
### Variables

> We also see at the end of the if-else loop that we assign the value of the first argument to the variable called `domain`. The assignment of variables takes place without the dollar sign `$`. 

The dollar sign is only intended to allow this variable's corresponding value to be used in other code sections. When assigning variables, there must be no spaces between the names and values.

```bash
else
	domain=$1
fi
```

*In contrast to other programming languages, there is no direct differentiation and recognition between the types of variables in Bash like `strings`, `integers`, and `boolean`.*

- All contents of the variables are treated as string characters. Bash enables arithmetic function depending on *whether only numbers are assigned or not.* 
- It is important to note when declaring variables that they do **not** contain a **space**.
	- Otherwise, the actual variable name will be interpreted as an internal function or command.

#### Declaring a Variable - Error

```bash
trop3n@htb[/htb]$ variable = "this will result with an error."

command not found: variable
```

#### Declaring a Variable - No Error

```bash
trop3n@htb[/htb]$ variable="Declared without an error."
trop3n@htb[/htb]$ echo $variable

Declared without an error.
```

### Arrays

> There is also the possibility of assigning several values to a single variable in Bash. 

- This can be beneficial if we want to scan multiple domains or IP addresses. These variables are called `arrays` that we can use to *store and process an ordered sequence of specific type values.* 

`Arrays` identify each stored entry with an index starting at `0`. 

- When we want to assign a value to an array component, we do so in the same way as with standard shell variables. 
- All we do is specify the field index enclosed in square brackets.

The declaration of `arrays` looks like this in Bash:
#### Arrays.sh
```bash
#!/bin/bash

domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)

echo ${domains[0]}
```

> We can also retrieve them individually using the index the variable with the corresponding index in curly brackets.
> 	**Curly brackets are used for variable expansion.**

```bash
trop3n@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com
```

> It is important to note that single quotes (`'` ... `'`) and double quotes (`"` ... `"`) prevent the separation by a space of the individual values in the array. **This means that all spaces between the single and double quotes are ignored and handled as a single value assigned to the array.**

```bash
#!/bin/bash

domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}
```

```shell-session
trop3n@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com
```

# Comparison Operators

> To compare specific values with each other, we need elements that are called `comparison operators`. 

- The `comparison operators` are used to determine how the defined values will be compared.

For these operators, we differentiate between:

- `string` operators
- `integer` operators
- `file` operators
- `boolean` operators

### String Operators

> If we compare strings, then we know what we would like to have in the corresponding value.

| Operator | Description                                 |
| -------- | ------------------------------------------- |
| `==`     | is equal to                                 |
| `!=`     | is not equal to                             |
| `<`      | is less than in ASCII alphabetical order    |
| `>`      | is greater than in ASCII alphabetical order |
| `-z`     | if the string is empty (null)               |
| `-n`     | if the string is not null                   |
> It is important to note here that we put the variable for the given argument `$1` in double quotes (`"$1"`). 
> 	This tells Bash that the content of the variable should be handled as a string. Otherwise, we would get an error.

```bash
#!/bin/bash

# Check the given argument
if [ "$1" != "HackTheBox" ]
then
	echo -e "You need to give 'HackTheBox' as argument."
	exit 1

elif [ $# -gt 1 ]
then
	echo -e "Too many arguments given."
	exit 1

else
	domain=$1
	echo -e "Success!"
fi
```

> String comparison operators "`< / >`" works only within the double square brackets `[[ <condition> ]]`. We can find the ASCII table on the Internet or by using the following command in the terminal:

```shell-session
trop3n@htb[/htb]$ man ascii
```
#### ASCII Table

|**Decimal**|**Hexadecial**|**Character**|**Description**|
|---|---|---|---|
|0|00|NUL|End of a string|
|...|...|...|...|
|65|41|A|Capital A|
|66|42|B|Capital B|
|67|43|C|Capital C|
|68|44|D|Capital D|
|...|...|...|...|
|127|7F|DEL|Delete|
`ASCII` stands for `American Standard Code for Information Interchange` and represents a 7-bit character encoding.

- Since each bit can take two values, there are `128` different bit patterns, which can also be interpreted as the decimal integers `0-127` or in hexadecimal values `00-7F`. 
- The first 32 ASCII character codes are reserved as so-called `control characters`.

### Integer Operators

> Comparing integer numbers can be very useful for us if we know what values we want to compare. Accordingly, we define the next steps and commands how the script should handle the corresponding value.

|**Operator**|**Description**|
|---|---|
|`-eq`|is equal to|
|`-ne`|is not equal to|
|`-lt`|is less than|
|`-le`|is less than or equal to|
|`-gt`|is greater than|
|`-ge`|is greater than or equal to|
```bash
#!/bin/bash

# Check the given argument
if [ $# -lt 1 ]
then
	echo -e "Number of given arguments is less than 1"
	exit 1

elif [ $# -gt 1 ]
then
	echo -e "Number of given arguments is greater than 1"
	exit 1

else
	domain=$1
	echo -e "Number of given arguments equals 1"
fi
```

### File Operators

> The file operators are useful if we want to find out specific permissions or if they exist.

| Operator | Description                                            |
| -------- | ------------------------------------------------------ |
| `-e`     | if the file exists                                     |
| `-f`     | tests if it is a file                                  |
| `-d`     | tests if it is a dictionary                            |
| `-L`     | tests if it is a symbolic link                         |
| `-N`     | checks if the file was modified after it was last read |
| `-0`     | if the current user owns the file                      |
| `-G`     | if the file's group id matches the current user's      |
| `-s`     | tests if the file has a size greater than 0            |
| `-r`     | tests if the file has read permission                  |
| `-w`     | tests if the file has write permission                 |
| `-x`     | tests if the file has execute permission               |
```bash
#!/bin/bash

# Check if the specified file exists
if [ -e "$1" ]
then
	echo -e "The file exists."
	exit 0

else
	echo -e "The file does not exist."
	exit 2
fi
```

### Boolean and Logical Operators

> We get a boolean value `false` or `true` as a result with logical operators. Bash gives us the possibility to compare strings by using double square brackets `[[ <condition> ]]`. To get these boolean values, we can use the string operators. 

Whether the comparison matches or not, we get the boolean value `false` or `true`.

```bash
#!/bin/bash

# Check the boolean value
if [[ -z $1 ]]
then
	echo -e "Boolean value: True (is null)"
	exit 1

elif [[ $# > 1 ]]
then
	echo -e "Boolean value: True (is greater than)"
	exit 1

else
	domain=$1
	echo -e "Boolean value: False (is equal to)"
fi
```

### Logical Operators

> With logical operators, we can define several conditions within one. This means that all the conditions we define must match before the corresponding code can be executed. 

| Operator | Description             |
| -------- | ----------------------- |
| `!`      | logical negotiation NOT |
| `&&`     | logical AND             |
| `\|\|`   | logical OR              |
```bash
#!/bin/bash

# Check if the specified file exists and if we have read permissions
if [[ -e "$1" && -r "$1" ]]
then
	echo -e "We can read the file that has been specified."
	exit 0

elif [[ ! -e "$1" ]]
then
	echo -e "The specified file does not exist."
	exit 2

elif [[ -e "$1" && ! -r "$1" ]]
then
	echo -e "We don't have read permission for this file."
	exit 1

else
	echo -e "Error occured."
	exit 5
fi
```

## Comparison Operators Question:

```bash
#!/bin/bash

var="8dm7KsjU28B7v621Jls"
value="ERmFRMVZ0U2paTlJYTkxDZz09Cg"

for i in {1..40}

do
        var=$(echo $var | base64)
        chars=$(echo $var | wc -c)

        if [[ "$var" == *"$value"* && $chars -gt 113469 ]];then
            echo $var | tail -c 20
        fi
done
```

#### Notes

> The `wc` command on line 9 is used to find the number of lines, characters, words and bytes of a file.

> Double brackets are used on line 11 due to the variables being processed as strings. 

> the `$chars` variable is created to hold the characters from the prior variables that are being generated by the script.

> `&&` means the AND logical operator.

# Arithmetic

> In Bash, we have seven different `arithmetic operators` we can work with. These are used to perform different mathematical operations or to modify certain integers.

### Arithmetic Operators

| Operator     | Description                             |
| ------------ | --------------------------------------- |
| `+`          | Addition                                |
| `-`          | Subtraction                             |
| `*`          | Multiplication                          |
| `/`          | Division                                |
| `%`          | Modulus                                 |
| `variable++` | Increase the value of the variable by 1 |
| `variable--` | Decrease the value of the variable by 1 |
We can summarize all of these operators in a small script:

```bash
#!/bin/bash

increase=1
decrease=1

echo "Addition: 10 + 10 = $((10 + 10))"
echo "Substraction: 10 - 10 = $((10 - 10))"
echo "Multiplication: 10 * 10 = $((10 * 10))"
echo "Division: 10 / 10 = $((10 / 10))"
echo "Modulus: 10 % 4 = $((10 % 4))"

((increase++))
echo "Increase Variable: $increase"

((decrease--))
echo "Decrease Variable: $decrease"
```

The output of this script looks like this:

```shell-session
trop3n@htb[/htb]$ ./Arithmetic.sh

Addition: 10 + 10 = 20
Substraction: 10 - 10 = 0
Multiplication: 10 * 10 = 100
Division: 10 / 10 = 1
Modulus: 10 % 4 = 2
Increase Variable: 2
Decrease Variable: 0
```

We can also calculate the length of the variable. Using this function `${variable}`, every character gets counted, and we get the total number of characters in the variable.

```bash
#!/bin/bash

htb="HackTheBox"

echo ${#htb}
```

> The `#` part of the function acts as a `len()` function in Python 3.

```shell-session
trop3n@htb[/htb]$ ./VarLength.sh

10
```

> If we look at our `CIDR.sh` script, we will see that we have used the `increase` and `decrease` operators several times.
> 	This ensures that the while loop, which will be discussed later, runs and pings the hosts while the variable `stat` has a value of `1`. 

If the ping command ends with code `0` (successful), we get a message that the `host is up` and the `stat` variable, as well as the variables `host_up` and `hosts_total` get changed.

```bash
echo -e "\nPinging host(s):"
	for host in $cidr_ips
	do
		stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
	done
```

# Input and Output Control

### Input Control

> We may get results from our sent requests and executed commands, which we have to decide manually on how to proceed. Another example would be that we have defined several functions in our script designed for different scenarios. 
> 	We have to decide which of them should be executed after a manual check and based on the results. 

It is also quite possible that specific scans or activities may not be allowed to be performed. Therefore, we need to be familiar with how to get a running script to wait for our instructions. 

If we look at our `CIDR.sh` script again, we see that we have added such a call to decide further steps. 

```bash
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```

- The first `echo` line serve as a display menu for the options available to us. 
- With the `read` command, the line with `Select your option:` is displayed, and the additional option `-p` ensures that our input remains on the same line. 
- Our input is stored in the variable `opt`, which then use to execute the corresponding functions with the `case` command. 
- Depending on the number we we enter, the `case` statement determines which functions are executed. 

### Output Control

> We have already learned about the output redirections of output in the `Linux Fundamentals` module. 

Nevertheless, the problem with redirections is that we do not get any output from the respective command. It will be redirected to the appropriate file. 

If our scripts become more complicated later, they can take much more time than just a few seconds. 

- To avoid sitting inactively and waiting for our script's results, we can use the `tee` utility. 
	- It ensures that we see the results we get immediately and that they are stored in the corresponding files. 
In our `CIDR.sh` script, we have used this utility twice in different ways.

```bash
# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}

<SNIP>

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)
```

> When using `tee`, we transfer the received output and use the `|` to forward it to `tee`.

The "`-a`/ `--append`" parameter ensures that the specified file is not overwritten but supplemented with the new results. At the same time, it shows us the results and how they will be found in the file.

```shell-session
trop3n@htb[/htb]$ cat discovered_hosts.txt CIDR.txt

165.22.119.202
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16
```

# Flow Control - Loops

> The control of the flow of our scripts is essential. We have already learned about the `if-else` conditions, which are also part of flow control. 

After all, we want our script to work quickly and efficiently, and for this, we can use other components to increase efficiency and allow error-free processing.

Each control structure is either a `branch` or a `loop`. Logical expression of boolean values usually control the execution of a control structure. These control structures include:

- Branches
	- `If-else` conditions
	- `Case` statements
- Loops:
	- `For` loops
	- `While` loops
	- `Until` loops

### For Loops

> The `For` loop is executed on each pass for precisely *one parameter*, which the shell takes from a list, calculates from an increment, or takes from another data source. The for loops runs as long as it finds corresponding data. 

This type of loop can be structured and defined in different ways. For example, the *for loops are often use when we need to work with many different values from an array.*

This can be used to scan different hosts or ports.

We can also use it to execute specific commands for known ports and their services to speed up our enumeration process.

### For Loop Syntax

```bash
for variable in 1 2 3 4
do
	echo $variable
done
```

```bash
for variable in file1 file2 file3
do
	echo $variable
done
```

```bash
for ip in "10.10.10.170 10.10.10.174 10.10.10.175"
do
	ping -c 1 $ip
done
```

> Of course, we can also write these commands in a single line. Such a command would look like this:

```shell-session
trop3n@htb[/htb]$ for ip in 10.10.10.170 10.10.10.174;do ping -c 1 $ip;done

PING 10.10.10.170 (10.10.10.170): 56 data bytes
64 bytes from 10.10.10.170: icmp_seq=0 ttl=63 time=42.106 ms

--- 10.10.10.170 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 42.106/42.106/42.106/0.000 ms
PING 10.10.10.174 (10.10.10.174): 56 data bytes
64 bytes from 10.10.10.174: icmp_seq=0 ttl=63 time=45.700 ms

--- 10.10.10.174 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 45.700/45.700/45.700/0.000 ms
```

Let's have another look at our `CIDR.sh` script. We have added several loops to the script, but let us stick with this little code section.
### CIDR.sh
```bash
# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}
```

> As in the previous example, for each IP address from the array `ipaddr` we make a `whois` request, whose output is filtered for `NetRange` and `CIDR`. 

- This helps us to determine which address range our target is located in.
- We can use this information to search for additional hosts during a penetration test, `if approved by the client`. 
- The results that we receive are displayed accordingly and stored in the file `CIDR.txt`.

### While Loops

The `while` loop is conceptually simple and follows the following principle:

- **A statement is executed as long as a condition is fulfilled (`true`).**

We can also combine loops and merge their execution with different values. It is important to note that the excessive combination of several loops in each other can make the code very unclear and lead to errors that can be hard to find and follow. 

Such a combination can look like this in our `CIDR.sh` script:

```bash
	stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
```

> The `while` loops also work with conditions like `if-else`. A while loop needs some sort of a counter to orient itself when it has to stop executing the commands it contains.

- Otherwise, this leads to an endless loop. Such a counter can be a variable that we have declared with a specific value or a boolean value.
- `While` loops run while the boolean value is `"True"`. Besides the counter, we can also use the command `break`, which interrupts the loop when reaching this command like in the following example.

```bash
#!/bin/bash

counter=0

while [ $counter -lt 10 ]
do
  # Increase $counter by 1
  ((counter++))
  echo "Counter: $counter"

  if [ $counter == 2 ]
  then
    continue
  elif [ $counter == 4 ]
  then
    break
  fi
done
```

```shell-session
trop3n@htb[/htb]$ ./WhileBreaker.sh

Counter: 1
Counter: 2
Counter: 3
Counter: 4
```

### Until Loops

> There is also the until loop, which is relatively rare. Nevertheless, the `until` loop works precisely like the `while` loop, but with the difference:

- The code inside a `until` loop is executed as long as the particular condition is `false`.

The other way is to let the loop run until the desired value is reached. 

The `until` loops are very well suited for this. This type of loop works similarly to the `while` loop but, as we already mentioned, with the difference that it runs until the boolean value is `false`.

```bash
#!/bin/bash

counter=0

until [ $counter -eq 10 ]
do
  # Increase $counter by 1
  ((counter++))
  echo "Counter: $counter"
done
```

```shell-session
trop3n@htb[/htb]$ ./Until.sh

Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
Counter: 6
Counter: 7
Counter: 8
Counter: 9
Counter: 10
```

# Flow Control - Branches

> As we have already seen, the branches in flow control include `if-else` and the `case` statements. 

We have already discussed the `if-else` statements in detail and know how this works. Now we will take a closer look at the case statements.

### Case Statements

> `Case` statements are also known as `switch-case` statements in other languages, such as C/C++ and C#. The main difference between `if-else` and `switch-case` is that `if-else` constructs allow us to check any boolean expression, while `switch-case` always compares only the variable with the exact value.

Therefore, the same conditions as for `if-else`, such as "greater-than", are not allowed for `switch-case`. The syntax for the switch-case statements looks like this:

#### Syntax - Switch-Case

```bash
case <expression> in
	pattern_1 ) statements ;;
	pattern_2 ) statements ;;
	pattern_3 ) statements ;;
esac
```

> The definition of switch-case starts with `case`, followed by the variable or value as an expression, which is then compared in the pattern. If the variable or value matches the expression, then the statements are executed after the parenthesis and ended with a double semicolon (`;;`).

In our `CIDR.sh` script, we have used such a `case` statement. Here we defined four different options that we assigned to our script, how it should be proceed after our decision.

```bash
# Available options
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```

# Functions

The bigger our scripts get, the more chaotic they become. If we use the same routines several times in the script, the script's size will increase accordingly. 

In such cases, `functions` are the solution that improves both the size and the clarity of the script many times. 

- We combine several commands in a block between curly brackets ( `{...}`) and call them with a function name defined by us with `functions`.
- Once a function has been defined, it can be called and used again during the script. 

`Functions` are an essential part of scripts and programs, as they are used to execute recurring commands for different values and phases of the script or program. Therefore, we do not have to repeat the whole section of code repeatedly but can create a single function that executes specific commands. 

- The definition of such functions *makes the code easier to read and helps keep the code as short as possible*. 
- It is important to note that functions must always be defined logically `before` the first call since a script is also processed from top to bottom. Therefore the definition of a function is always `at the beginning` of the script. There are two methods to define the functions:
#### Method 1 - Functions

```bash
function name {
	<commands>
}
```
#### Method 2 - Functions

```bash
name() {
	<commands>
}
```

> We can choose the method to define a function that is most comfortable for us. In our `CIDR.sh` script, we used the first method because it is easier to read with the keyword `function`.

```bash
# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}
```

> The function is called only by calling the specified name of the function, as we have seen in the case statement.
#### Function Execution - CIDR.sh

```bash
<SNIP>
case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```
### Parameter Parsing

> Such functions should be designed so that they can be used with a fixed structure of the values or at least only with a fixed format. 

Like we have seen in our `CIDR.sh` script, we used the format of an IP address for the function `"network_range"`. 

The parameters are optional, and therefore we can call the function without parameters. In principle, the same applies to the passed parameters as to parameters passed to a shell script.

- These are `$1 - $9 (${n})`, or `$variable` as we have already seen. 
- Each function has its own set of parameters , so they do not collide with those of other functions or the parameters of the shell script. 

> An important difference between bash scripts and other programming languages is that **all defined variables are always processed `globally`** unless otherwise declared by `local`. 
> 	This means that the first time we have defined a variable in a function, we will call it in our main script (outside the function). 
> 	Passing the parameters to the functions is done the same way as we passed the arguments to our script and looks like this:

#### PrintPars.sh

```bash
#!/bin/bash

function print_pars {
	echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"
```

```shell-session
trop3n@htb[/htb]$ ./PrintPars.sh

First parameter Second parameter Third parameter
```

### Return Values

> When we start a new process, each `child process` (for example, a `function` in the executed script) returns a `return code` to the `parent process` (`bash shell` through which we executed the script) at it's termination, informing it of the status of the execution.

- This information is used to determine whether the process ran successfully or whether specific errors occured. 

Based on this information, the `parent process` can decide on further program flow.

| Return Code | Description                    |
| ----------- | ------------------------------ |
| `1`         | general errors                 |
| `2`         | Misuse of shell builtins       |
| `126`       | Command invoked cannot execute |
| `127`       | Command not found              |
| `128`       | Invalid argument to exit       |
| `128+n`     | Fatal error signal "`n`"       |
| `138`       | Script terminated by Ctrl-C    |
| `255\*`     | Exit status out of range       |
> To get the value of the function back, we can use several methods like `return`, `echo`, or a `variable`. 

In the next example, we will see how to use `$?` to read the `return code`, how to pass the arguments to the function and how to assign the result to a variable.
#### Return.sh

```bash
#!/bin/bash

function given_args {

        if [ $# -lt 1 ]
        then
                echo -e "Number of arguments: $#"
                return 1
        else
                echo -e "Number of arguments: $#"
                return 0
        fi
}

# No arguments given
given_args
echo -e "Function status code: $?\n"

# One argument given
given_args "argument"
echo -e "Function status code: $?\n"

# Pass the results of the funtion into a variable
content=$(given_args "argument")

echo -e "Content of the variable: \n\t$content"
```

# Debugging

> Bash gives us an excellent opportunity to find, track and fix errors in our code. The term `debugging` can have many different meanings. Nevertheless, `Bash debugging` is the process of removing errors (bugs) from out code. 
> 	Debugging can be performed in many different ways. For example, we can use our code for debugging to check for typos, or we can use it for code analysis to track them and determine why specific errors occur.

**This process is also used to find vulnerabilities in programs.** 

- For example, we can try to cause errors using different input types and track their handling in the CPU through the assembler, which may provide a way to manipulate the handling of these errors to insert our own code and force the system to execute it. 
- **This topic will be discussed in detail in other modules.**

Bash allows us to debug our code by using teh `-x` (`xtrace`) and `-v` options. 

Now let's look at an example in our `CIDR.sh` script.

```shell-session
trop3n@htb[/htb]$ bash -x CIDR.sh

+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```

> Here Bash shows us precisely which function or command was executed with which values. This is indicated by the plus sign (`+`) at the beginning of the line. If we want to see all the code for a particular function, we can set the `-v` option that displays the outputs in more detail.

#### CIDR.sh - Verbose Debugging

```shell-session
trop3n@htb[/htb]$ bash -x -v CIDR.sh

#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi
+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```

> In comparison to normal debugging, we see the entire code section that has been processed so far and then the individual steps that have been taken.


