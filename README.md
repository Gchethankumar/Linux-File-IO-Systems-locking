# Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:
Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:
Write the C Program using Linux IO Systems locking

### Step 3:
Execute the C Program for the desired output. 

# PROGRAM:
Developed By: G Chethan kumar

Register no.: 212222240022
## 1.To Write a C program that illustrates files copying 
```
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
int main()
{
char block[1024];
int in, out;
int nread;
in = open("filecopy.c", O_RDONLY);
out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
while((nread = read(in,block,sizeof(block))) > 0)
write(out,block,nread);
exit(0);}

```
## 2.To Write a C program that illustrates files locking
```
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>
int main (int argc, char* argv[])
{ char* file = argv[1];
 int fd;
 struct flock lock;
 printf ("opening %s\n", file);
 /* Open a file descriptor to the file. */
 fd = open (file, O_WRONLY);
// acquire shared lock
if (flock(fd, LOCK_SH) == -1) {
    printf("error");
}else
{printf("Acquiring shared lock using flock");
}
getchar();
// non-atomically upgrade to exclusive lock
// do it in non-blocking mode, i.e. fail if can't upgrade immediately
if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
    printf("error");
}else
{printf("Acquiring exclusive lock using flock");}
getchar();
// release lock
// lock is also released automatically when close() is called or process exits
if (flock(fd, LOCK_UN) == -1) {
    printf("error");
}else{
printf("unlocking");
}
getchar();
close (fd);
return 0;
}

```
## OUTPUT:

## 1. Output of C program that illustrates files copying:

![osimg1](https://github.com/Gchethankumar/Linux-File-IO-Systems-locking/assets/118348224/5da727de-2a79-4252-a689-39f33e4dbd67)
 

## 2.To Write a C program that illustrates files locking:

![osimg2](https://github.com/Gchethankumar/Linux-File-IO-Systems-locking/assets/118348224/94bb96a7-c114-4bd3-91dc-23114d8d712d)


# RESULT:
The programs are executed successfully.
