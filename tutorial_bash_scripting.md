This is a quick tutorial for making a bash script for fun.
I'll be using terminal to write my script, you can code yours using VSCode or other IDE's as well.

Those who are familiar with coding quickly create a file with extension `.sh`, open your file in your IDE and skip to Step 4

Others follow along from Step 1
1. 
Open terminal and change your directory to where you want to keep your Bash script using `cd`, I want to keep my script on my Desktop, so.

```
cd Desktop
```

2.
Next create a file with extension `.sh` this will be the file we are going to write our script.

```
touch myscript.sh
```

3.
Now open the file with either `vim` or `nano`. I'm using vim. 
```
vim myscript.sh
```
You should see a blank screen as currently the file is empty.

Note: If you are using vim, To write : enter `i`, to stop writing/editing: press `esc`(escape), to quit  vim without saving: enter `:q!`, to quit vim with saving: enter `:x`

----

Again Note: Here I'm using Vim terminal but you can open your .sh file in your preferred IDE (VSCode etc) and code along.

Let's Start Scripting!!!!

4. 
The first line should start with a syntax: **Shebang*  followed by the path where interpreter i(n this case Bash) is located on your machine.

> To find out where your bash is located: type `which bash`. It's generally located here: `/bin/bash`

*Shebang is a keyword for the syntax `#!`

That means your file now should look similar to

```
#! /bin/bash
``` 

5.
Now to display a introductory message with a freeze time of 5 seconds write

```
echo "Hello"
echo "$(sleep 3) My name is Cherry, and what's yours?"
``` 
The message Hello is followed by a freeze time of 3 seconds and then the message: "My name is Cherry, and what's yours?" is displayed

> To check if the script you've created is working: Save the file and simply open a new terminal window and be sure you are in the same directory where your file is present, in my case I'll check if I'm in Desktop directory, and type -
```
bash (your_file_name.sh)
``` 

6.
Now to accept the input for "... and what's yours?".
Go again to your vim terminal or IDE and continue typing

```
read name
echo "Hey $name, it's nice to have you here!"
```
read is a built-in command that converts the content on the line to a variable, and we use that variable to display a message using $ symbol.

-----
Your script till now should look similar to-

```
#! /bin/bash
echo "Hello"
echo "$(sleep 3) My name is Cherry, and what's yours?"
read name
echo "Hey $name, it's nice to have you here!"
``` 
-----

7.
