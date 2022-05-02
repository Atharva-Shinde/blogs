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

Your file now should look similar to

```
#! /bin/bash
``` 

5.
```
echo "You are logged in as $(whoami)"
``` 
`$(whoami)` displays the current username of your machine.

6.
Now to display an introductory message with a freeze time of 2 seconds write

```
echo "Hello!!!!"
read -p "$(sleep 2) My name is Cherry, and what's yours? -" name
``` 
The message Hello is followed by a freeze time of 2 seconds and then the prompt: "My name is Cherry, and what's yours?" is displayed.

`read` is a built-in command that converts the content on the line to a "variable", and we use that variable to display a message using $ symbol.
`-p` is a keyword for accepting prompt message, this allows user to write their input on the same line and the result is stored in "variable" `name`

> To check if the script you've created is working: Save the file and simply open a new terminal window and be sure you are in the same directory where your file is present, in my case I'll check if I'm in my Desktop directory, and type -
```
bash (your_file_name.sh)
``` 

7. 

```
echo " $(sleep 3) Choose between options (type your option letter):"
echo -e "Question 1: What would you prefer:\na] Staying at home\nb] At outings "
read answer1
echo -e "Question 2: Where would you prefer to live rest of your life:\na]In a dense forest b]Centre of New-York City" 
read answer2
echo -e "Question 2: Where would you prefer to live rest of your life:\na]In a dense forest b]Centre of New-York City" 
read answer2
``` 

7. 
Time for some Iterations:

We are writing a script where user can either answer life questions asked by Cherry or play a trivia.
```
read -p "You know what, I am curious about human life, maybe you can help me with that, what say? If no you can play a trivia " answer

while true; do
  case $answer in
    # case 1 
    Yes | yeah | yes | YES | Y | y  ) echo "$(sleep 1) Wohoo thanks for accepting my request"
    break;;
   # case 2
    no | No | NO | N | n | trivia ) echo "$(sleep 1)ok, let's have a trivia!!!"
    break;;
    #case 3
    exit ) echo"You've exited successfully"
    exit 0;;
    # default
    * ) echo "choose either one by saying yes or no"
    break;;
  esac
done
``` 
In the above code we run case statements  inside do-while loop which checks whether user have typed yes, no or exited the program. 
If any one of the case statement is fulfilled, our script prints its respective message and breaks out of the iteration.
In Bash we need to declare a closing syntax after every iteration, thus the keywords `esac`: for case statement and `done`: for do-while loop.

I used case-statements for easy-understanding of what exactly is happening inside the script. If user wants to play trivia and therefore types `n` or `trivia` or ` NO`, case 2 is triggered and the message `ok, let's have a trivia!!!` is displayed.

-----
Your script now should look like-

```
#! /bin/bash

echo "You are logged in as $(whoami)"
echo "Hello!!!!"
read -p "$(sleep 2) My name is Cherry, and what's yours? -" name
echo "Hey $name, it's nice to have you here!"

read -p "You know what, I am curious about human life, maybe you can help me with that, what say? If no you can play a trivia " answer

while true; do
  case $answer in
    # case 1 
    Yes | yeah | yes | YES | Y | y ) echo "$(sleep 1) Wohoo thanks for accepting my request"
    break;;
   # case 2
    no | No | NO | N | n | trivia ) echo "$(sleep 1)ok, let's have a trivia!!!"
    break;;
    #case 3
    exit ) echo"You've exited successfully"
    exit 0;;
    # default
    * ) echo "choose either one by saying yes or no"
    break;;
  esac
done
``` 
-----

<!-- 8. Let's write code for if user decides to go with Cherry's request.


```
if[$answer =]
```  -->
