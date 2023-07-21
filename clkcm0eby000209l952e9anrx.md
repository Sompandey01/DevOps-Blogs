---
title: "Day 5: Advanced Linux Shell Scripting for DevOps Engineers with User management"
datePublished: Fri Jul 21 2023 13:20:56 GMT+0000 (Coordinated Universal Time)
cuid: clkcm0eby000209l952e9anrx
slug: day-5-advanced-linux-shell-scripting-for-devops-engineers-with-user-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689945606002/9490b0f7-6794-4b08-a1b7-d48666d059cc.webp
tags: linux, devops, linux-for-beginners, 90daysofdevops, tws

---

## Introduction:

In this blog, we'll learn some advanced concepts of Linux shell scripting that every aspiring DevOps engineer should know. We'll gonna learn how to automate tasks using cron/crontab, how to create and manage users and write functions in bash. Let's dive in and embark on this exciting journey of automation in Linux! 🚀💻

## Write a bash script [`createDirectories.sh`](http://createDirectories.sh) that when the script is executed with three given arguments (one is directory name and second is start number of directories and third is the end number of directories ) it creates specified number of directories with a dynamic directory name.

```bash
#!/bin/bash

# Check if three arguments are provided
if [ "$#" -ne 3 ]; then
  echo "Usage: $0 <directory_name> <start_number> <end_number>"
  exit 1
fi

# Get the arguments
directory_name=$1
start_number=$2
end_number=$3

# Function to create directories
create_directories() {
  for ((i=start_number; i<=end_number; i++)); do
    dir_name="${directory_name}_${i}"
    mkdir -p "$dir_name"
    echo "Created directory: $dir_name"
  done
}

# Call the function
create_directories
```

**To run the script:**

1. Copy the above script into a text editor.
    
2. Save the file with the name [`createDirectories.sh`](http://createDirectories.sh).
    
3. Open your terminal or command prompt.
    
4. Navigate to the directory where you saved the script.
    
5. Give execute permission to the script:
    

```bash
chmod 777 createDirectories.sh
```

1. Run the script with three arguments (directory name, start number, and end number):
    

```bash
./createDirectories.sh Day 1 90
```

The script will create 90 directories with names like `Day_1`, `Day_2`, and so on, up to `Day_90`. Each directory will be created in the current working directory.

## Create a Script to backup all your work done till now.

```bash
#!/bin/bash

# Check if the directory name is provided as an argument
if [ $# -ne 1 ]; then
  echo "Usage: $0 <directory_name>"
  exit 1
fi

# Extract the directory name from the argument
directory_name="$1"

# Validate if the directory exists
if [ ! -d "$directory_name" ]; then
  echo "Error: Directory '$directory_name' not found."
  exit 1
fi

# Create a backup directory with the current date and time
backup_dir="backup_$(date +%Y%m%d_%H%M%S)"

# Create the backup directory
mkdir "$backup_dir" || { echo "Failed to create backup directory."; exit 1; }

# Copy the content of the specified directory to the backup directory
cp -r "$directory_name"/* "$backup_dir" || { echo "Failed to create backup."; exit 1; }

echo "Backup created successfully at: $backup_dir"
```

Give execute permission to the script:

```bash
chmod 777 backup_script.sh
```

Run the script with the directory name you want to back up, for example:

```bash
./backup_script.sh my_directory
```

The script will create a backup of the specified directory, ensuring your important data is safe and secure. 🚀📂💾

## Automate the backup Script

To automate the backup script using Cron, follow these steps:

1. Open your terminal or command prompt.
    
2. Type `crontab -e` and press Enter. This will open the crontab file in the default text editor.
    
3. Add the following line at the end of the crontab file to schedule the script to run daily at a specific time (replace `/path/to/backup_script.sh` with the actual path to your script):
    

```bash
0 2 * * * /bin/bash /path/to/backup_script.sh my_directory >> /path/to/backup.log 2>&1
```

Save the crontab file and exit the text editor.

## Create 2 users and just display their Usernames

To create a user, we can use the following command:

1. Create the first user:
    

```bash
sudo adduser user1
```

1. Create the second user:
    

```bash
sudo adduser user2
```

1. Display the usernames:
    

```bash
echo "User 1: user1"
echo "User 2: user2"
```

You'll have to set passwords and other details for the two users during the creation process. After executing the commands, the script will display the usernames of the two newly created users.

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))