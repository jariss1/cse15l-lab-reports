*Preface: I completed the lab before lab day not knowing the lab was supposed to be done in groups, thus some screenshots will be from groupmates as I assisted them in completing the steps*

# Connect to Remote via SSH

## Installing VS Code
1. Go to [Link](https://code.visualstudio.com/) and download the correct version for your operating system

> Once installed, you're window should look like this: 
 \
 [Image](VSCode.jpeg)

---

## Connecting to Remote via SSH
1. type `$ ssh cs15lfa22zz@ieng6.ucsd.edu` and replace zz with your user id

This will be returned:

```
⤇ ssh cs15lfa22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```

2. Enter `yes` and your password:

```
# On your client
⤇ ssh cs15lfa22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Password: 
```
```
#Now on remote server
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lfa22zz, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lfa22
```

*Now you're connected to the remote server!*

[Image](SSH.png)

---
## Run some commands!
Try out some commands from the list below:
 * `cd ~`
 * `cd`
 * `ls -lat`
 * `ls -a`
 * `ls` directory where directory is /home/linux/ieng6/cs15lfa22/cs15lfa22abc, where the abc is one of the other group members’ username
 * `cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/`
 * `cat /home/linux/ieng6/cs15lfa22/public/hello.txt`

 [Image](Commands.png)

---
## Copying Files from Client to Remote
* `scp` : secure copy, always run from client

1. Create a file called `WhereAmI.java`
```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
2. Compile and run WhereAmI using `javac` and `java`
```
javac WhereAmI.java
java WhereAmI
```

3. In terminal, run `scp WhereAmI.java cs15lfa22zz@ieng6.ucsd.edu:~/`
using your username id and enter your password

4. Log into `ieng6` using ssh

[Image](SCP.jpeg)

---
## SSH Keys
Having to login using your password everytime you SSH can become annoying *quickly*. Thankfully, a program `ssh-keygen` uses a file called **public key** on the remote server and a file called **private key** on the client server for the SSH command to use.

1. run the command `ssh-keygen` and this will generate a public & private key

2. Hit Enter when prompted to save the key to the *default* path, and take note of it

```
# on client (your computer)
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/joe/.ssh/id_rsa): /Users/joe/.ssh/id_rsa
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/joe/.ssh/id_rsa.
Your public key has been saved in /Users/joe/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:jZaZH6fI8E2I1D35hnvGeBePQ4ELOf2Ge+G0XknoXp0 joe@Joes-Mac-mini.local
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|       . . + .   |
|      . . B o .  |
|     . . B * +.. |
|      o S = *.B. |
|       = = O.*.*+|
|        + * *.BE+|
|           +.+.o |
|             ..  |
+----[SHA256]-----+
```

3. Log into SSH 
```
#on client
$ ssh cs15lfa22zz@ieng6.ucsd.edu
<Enter Password>
```
```
# now on server
$ mkdir .ssh
$ <logout>
```
```
#back on client
$ scp /Users/joe/.ssh/id_rsa.pub cs15lfa22@ieng6.ucsd.edu:~/.ssh/authorized_keys
#You use your username and the path you saw in the command above
```
Now you can login via SSH w/o entering your password

---
## Making Remote Run even Faster
* Use the up arrow to load previous commands
* Write a command in quotes at the end of an ssh command to directly run it on the remote server
* Use semicolons to run multiple commands on the same line in most terminals

Using the up arrow, your terminal would look something like this:
[Image](SCP.jpeg)

---
## Questions!?!
What happens when you rerun a scp file with the same name?

How can you consider how long it takes to update and reupload a file when the time it takes to make changes to a file is completely volatile?
