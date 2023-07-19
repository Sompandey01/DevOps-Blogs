---
title: "Basic Linux Commands 🐧💻"
datePublished: Wed Jul 19 2023 08:48:42 GMT+0000 (Coordinated Universal Time)
cuid: clk9hel5d001909jx79ksaj16
slug: basic-linux-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689756096236/298c36f6-fab1-46af-b774-65c0cdf6e77c.jpeg
tags: linux, devops, linux-for-beginners, 90daysofdevops, tws

---

## What is the Linux command to:

### **To view what's written in a file.**

To view what's written inside a file, you can use the `cat` command.

```bash
cat filename.txt
```

### **To change the access permissions of files.**

In Linux, `chmod` command is used to change the access permissions of files.

```bash
chmod 777 [file_name]
```

### To check which commands you have run till now.

To check how many commands you had run till now, use `history` command. This command is used to view the previously executed commands.

```bash
history
```

### To remove a directory/ Folder.

To remove a directory/folder in Linux you can use `rm` command with `-r` option. This `-r` is used to remove or delete a folder permanently.

```bash
rm -r myfiles
```

### To create a fruits.txt file and to view the content.

To create a file use `touch` command and to view the content use `cat` command.

```bash
touch fruits.txt
cat fruits.txt
```

### Add content in devops.txt (One in each line) - Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava.

To add the content "Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava" in "devops.txt" with each fruit on a new line, you can use the `cat` command.

```bash
cat >> devops.txt
Apple
Mango
Banana
Cherry
Kiwi
Orange
Guava
```

### To Show only top three fruits from the file.

To show only top three fruits from the file you can use `head` command with `-n` option.

```bash
head -n 3 devops.txt
Apple
Mango
Banana
```

### To Show only the bottom three fruits from the file.

To show only the bottom three fruits from the file you can use the `tail` command with `-n` option. **For example** tail -n 3 devops.txt. This command will display the last three lines (fruits) from the "devops.txt" file:

```bash
tail -n 3 devops.txt
Kiwi
Orange
Guava
```

### To create another file Colors.txt and to view the content.

To create another file again use the `touch` command to create a "colors.txt" file and to view the content inside it, use `cat` command.

```bash
touch Colors.txt
cat Colors.txt
```

### Add content in Colors.txt (One in each line) - Red, Pink, White, Black, Blue, Orange, Purple, Grey.

To add content in Colors.txt (One in each line) you can use the `cat` command.

```bash
cat >> Colors.txt
Red
Pink
White
Black
Blue
Orange
Purple
Grey
```

### To find the difference between fruits.txt and Colors.txt files.

To find the differences between the "fruits.txt" and "Colors.txt" files and display the differences, you can use the `diff` command.

```bash
diff fruits.txt Colors.txt
```

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))