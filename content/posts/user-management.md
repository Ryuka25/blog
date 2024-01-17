+++
title = 'User management'
date = 2024-01-16T14:46:12+03:00
summary = 'User management in linux OS'
+++

## Delete user

```sh
userdel [options] username
```

Option  | Description
--------|------------
-r      | Delete the user's home directory and files
-f      | Force the deletion of the user's account, even if processes are still running
-Z	    | Remove the user's SELinux security context

**Exemple**: `sudo userdel -r babakoto`. This cmd will delete the user `babakoto` and delete his home directory

## Create user and Setting up user

```sh
useradd USERNAME
useradd -m -d /PATH/TO/FOLDER USERNAME
```

**Exemple**: `sudo useradd -m -d /opt/app app`. This cmd will add the user `app` and define `/opt/app` as is home directory. By default, home directory is set to `/home/USERNAME`

### Add user to sudo group

```sh
adduser USERNAME sudo
```

After this cmd, user should restart his session.

### Change User password

```sh
passwd USERNAME
```