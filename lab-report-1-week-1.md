# Week 1 Lab Report - Remote Access

## **Installing VScode**
*In this section, we will be installing VScode, whose terminal we will be using to conduct our remote access.*
1. To install, follow this [link](https://code.visualstudio.com/) and download the appropriate version for your operating system.

2. Once installed, a window resembling the following should appear when opening VSCode: 

![Image](/images/VSCodewelcome.png)

## **Remotely Connecting**
*In this section, we will be using the VScode terminal to connect to a remote server using a course-specific account for CSE 15L.*

1. If you are on Windows, check to make sure a program called OpenSSH client is installed on your computer. It should be there by default, but if not follow this [link](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse).

2. In VScode, open a new terminal using Ctrl or Command + and input the following command:
    
     `$ ssh cs15lfa22zz@ieng6.ucsd.edu`

    * Note that `zz` will be replaced by the letters in your own account.

3. A message similar to the following should appear if this is your first time connecting to this server:
    ```
    ⤇ ssh cs15lfa22zz@ieng6.ucsd.edu
    The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
    RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```
    * Type `yes` and press enter. Then, type in the password that you set for your CSE15L account.

4. Once you are logged in, an output similar to the following, except with your own account should appear: 

![Image](/images/image15.png)

## **Trying Some Commands**
*In this section, we will be experimenting with some commands used to access and modify filesystems*

1. Try out some commands that incorporate `cd`, `ls`, `pwd`, `mkdir`, and `cp`.

2. For example, the following commands will copy over an existing file called `Hello.txt` over to your home directory, and then display its contents.

    ```
    cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/
    cat /home/linux/ieng6/cs15lfa22/public/hello.txt
    ```

3. The image below shows an example of some commands being run:

![Image](/images/image17.png)

## **Moving Files with `scp`**
*In this section, we will by coping a file over from your computer to the remote server.*

1. Create a file called `WhereAmI.java` with the following contents: 

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
2. Then, compile and run the program with the following commands: 

```
javac WhereAmI.java
java WhereAmI
```
3. Now, to copy this file over to the remote server, input the following command from the directory that contains `WhereAmI.java`.

    `scp WhereAmI.java cs15lfa22zz@ieng6.ucsd.edu:~/`
    * Again, the `zz` will be replaced by the letters in your account.
    * You will also need to input your password again.

4. Login to the remote server with `ssh` again, and use the `ls` command to verify that the file has been copied over to your home directory.
5. Once that has been confirmed, you can now run `WhereAmI.java` from the remote server with the same commands as in step 2.
6. The image below shows the process from steps 2 to 5:

![Image](/images/image26.png)

## **Setting an SSH Key**
*In this section, we will be creating SSH keys that can be used to log in to the remote server without a password.*
1. To begin, run the following commands:

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
2. When prompted with `Enter file in which to save the key (/Users/joe/.ssh/id_rsa):`, pressing enter will create the key within a default directory whose name is the same as above except with your user.
3. Windows users must input the following additional commands as well from your own computer. 

```
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
Get-Service ssh-agent
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```
4. Make sure to run VScode as Adminstrator while using these commands, and replace `USERPROFILE\.ssh\id_ed25519` with the Path for your own SSH key.
5. Now, run the `ssh` command again from your computer to access the remote server. Then, type `mkdir .ssh` and `logout` to get back to your own client.
6. Finally, you can `scp` your SSH key over with the following command:
    `$ scp /Users/joe/.ssh/id_rsa.pub cs15lfa22@ieng6.ucsd.edu:~/.ssh/authorized_keys`
    * Use the path for your own SSH key

7. The image below shows an example of accessing the remote server without a password.

![Image](/images/image14.png)
## **Optimizing Remote Running**
*In this section, we will be discussing tips on how to optimize the process of copying files and running them on a remote server*

* If you put quotation marks around a command following an `ssh` command, such as below, the command will be run on the server and then log you out.

* Semicolons can be used to run multiple commands on 1 line

* Combining the above two with the up-arrow key to access previously run commands can be used to speed up the process.

The image below shows an example: 

![Image](/images/OptimizationSSH.png)