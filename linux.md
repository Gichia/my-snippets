# My Linux Command Snippets
> These are the Linux command snippets to perform various tasks.

## Basic Commands

1. The __ls__ command:

Lists out the files and directories in the path you are in

```linux
    $ ls
```
The __ls__ command has some *flags* that add functionality.

* __-a__ --> Does 
* __-h__ --> Does  
* __-l__ --> Does 


```linux
    $ ls 
```

## Basic Yum Commands
More commands to follow here


## Yum Installs

1. Install Java OpenJDK 8

```linux
    sudo yum install java-1.8.0-openjdk-devel 
```

## How to create partitions a HDD in CentOS 7 using **fdisk** command.

1. Create the partition.

```linux
# List out all the device blocks on the system.
$ fdisk -l

# Detailed info about a device
$ fdisk -l /dev/sda1

# Enter the fdisk command
$ fdisk /dev/sda1
```

2. Format the partition.
