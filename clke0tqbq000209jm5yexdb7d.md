---
title: "Day 6: File Permissions and Access Control Lists"
datePublished: Sat Jul 22 2023 13:03:26 GMT+0000 (Coordinated Universal Time)
cuid: clke0tqbq000209jm5yexdb7d
slug: day-6-file-permissions-and-access-control-lists
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690030958759/c8be6755-fadf-45eb-8567-e3b1925c125d.png
tags: linux, learning, devops, linux-for-beginners, 90daysofdevops

---

## Create a simple file and do `ls -ltr` to see the details of the files.

Each of the three permissions are assigned to three defined categories of users. The categories are:

```bash
 owner   —   The owner of the file or  application.
```

* "chown" is used to change the ownership permission of a file or directory.
    

```bash
 group   —   The group that owns the file or application.
```

* "chgrp" is used to change the group permission of a file or directory.
    

```bash
 others  —   All users with access to the system. (outised the users are in a group)
```

## Changing ownership and group:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690027398272/c352b665-2260-40ff-bbd7-69cb1cdf3cdf.png align="center")

## File Permissions in Linux

There are 3 types of file permissions in Linux:

1. Read (r)
    
2. Write (w)
    
3. Execute (x)
    

**You can check the permission allotted to a file using**

```bash
ls -l [file_name]
```

**To change the file permissions**

To change file permissions in Linux, you can use the `chmod` command. This command allows you to modify the read, write, and execute permissions for the owner, group, and others. The permissions are represented using three characters: `r` for read, `w` for write, and `x` for execute.

```bash
chmod u=rwx, g=rwx, o=rwx [file_name]
```

Here, **u** stands for **user**; **g** for **group** and **o** for **others**.

## **Changing File Permissions with** `chmod`:

1. `chmod +`: Adds permissions.
    
2. `chmod -`: Removes permissions.
    
3. `chmod =`: Sets permissions explicitly.
    

## If you wanna use a number instead of u,g,x then:

**Numeric Representation**:

* `0`: No permissions.
    
* `1`: Execute permission.
    
* `2`: Write permission.
    
* `3`: Write and execute permissions.
    
* `4`: Read permission.
    
* `5`: Read and execute permissions.
    
* `6`: Read and write permissions.
    
* `7`: Read, write, and execute permissions.
    

```bash
chmod 777 [file_name]
```

## **Access Control Lists Command (ACL )**

Access Control Lists (ACL) allow you to set more specific permissions to a file or a directory without changing the ownership and group. With ACL you can grant or deny permissions to individual users and groups, even when they don't belong to the owner group of the file or directory.

**ACL Commands**:

1. View ACL for a file or directory:
    

```bash
getfacl filename_or_directory
```

1. Set ACL for a file or directory:
    

```bash
setfacl -m u:user:rwx,g:group:rx filename_or_directory
```

1. Remove ACL from a file or directory:
    

```bash
setfacl -b filename_or_directory
```

1. For adding the permission for user:
    

```bash
setfacl -m u:user:rwx <target_file>
```

1. For adding permission for the group:
    

```bash
setfacl -m g:group:rwx <target_file>
```

1. To remove a specify entry:
    

```bash
setfacl -x u:user:rwx <target_file>
```

1. To remove all entries:
    

```bash
setfacl -b <target_file>
```

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))