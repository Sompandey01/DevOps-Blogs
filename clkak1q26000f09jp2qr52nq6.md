---
title: "Day 4: Basic Linux Shell Scripting for DevOps Engineers."
datePublished: Thu Jul 20 2023 02:50:27 GMT+0000 (Coordinated Universal Time)
cuid: clkak1q26000f09jp2qr52nq6
slug: day-4-basic-linux-shell-scripting-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689821024504/2243bd30-b1eb-4c7c-81cd-57f3e191b21f.jpeg
tags: linux, devops, linux-for-beginners, 90daysofdevops, tws

---

## What is Shell?

A shell in Linux is a command line interface that will take all my commands as input and convert those to tell the operating system what to do basically. **Example:** Bourne Shell, Bash etc.

## What is Shell Scripting for DevOps?

Shell scripting in DevOps is like creating a magical recipe that automates tasks and makes things happen effortlessly. It's a way to give instructions to the computer that it can follow to perform various tasks automatically.

Shell scripting is used to create a script of commands that can be executed in sequence and perform various operations. Shell scripting involves writing scripts using a specific shell's scripting language to automate tasks. These scripts can perform various tasks, automate processes, and execute complex operations by combining multiple commands, control structures (like loops and conditionals), variables, and functions.

## What is `#!/bin/bash?` can we write `#!/bin/sh` as well?

`#!/bin/bash` is called a **shebang** or **hashbang**. It is the first line in a shell script and is used to specify the interpreter or shell that should be used to execute the script. When you use `#!/bin/bash` at the beginning of a shell script, it indicates that the script should be executed using the Bash shell, Bash shell is a popular and powerful shell available on most Unix-like systems, including Linux. Shebang is important to ensure the script runs correctly and consistently. Similarly, you can use `#!/bin/sh` should be executed using any default shell, it's depends upon the operating system, it can be bash,dash,zsh etc.

## Write a Shell Script which prints `I will complete #90DaysOofDevOps challenge`

```bash
#!/bin/bash

echo "I will complete #90DaysOfDevOps challenge"
```

To run the above script, follow these steps:

1. Open a text editor (e.g., Notepad on Windows, or Nano/Vim on Linux).
    
2. Copy and paste the above script into the text editor.
    
3. Save the file with a .sh extension, for example, `devops_script.sh`
    
4. Now, open your terminal or command prompt.
    
5. Navigate to the directory where you saved the script.
    
6. Run the script with the following command:
    

```bash
./devops_script.sh
```

Now, the script will display the message "I will complete #90DaysOfDevOps challenge" on the screen. 🚀

## Write a Shell Script to take user input, input from arguments and print the variables.

### Shell Script:

```bash
#!/bin/bash

echo"Enter your name"
read name 
echo"Hello! ${name}! welcome to my blog"
```

### Output:

```bash
Enter your name
Ravi
Hello! Ravi! welcome to my blog
```

## Write an Example of If else in Shell Scripting by comparing 2 numbers

### Shell Script:

```bash
#!/bin/bash

read num1
echo "num1 is ${num1}"
read num2
echo "num2 is ${num2}"
if ["$num1" -eq "$num2" ]; then
   echo "The numbers are equal."
elif [ "$num1" -gt "$num2" ]; then
  echo "num1 is greater than num2."
else
  echo "num2 is greater than num1."
fi
```

### Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689819490768/cc698860-60f1-4b99-8aea-d504fac75323.png align="center")

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))