# Accessing Remote Servers
## By: Adhithya Ananthan
In this blog, we will explore how to remotely access servers from our local computer. Understanding how to do this is important because in our future careers we will be required to access organization's servers to do various tasks. The following sections provide a step-by-step guide on using ssh/scp technologies.

---

## Step 1: Installing VScode
VScode is commonly used IDE that allows you to write programing scripts. To install VScode go to this [*link*](https://code.visualstudio.com/download) and download it based on the computer you are using (Windows, Linux, or Mac). 
![](/lab1-screenshots/VSCode_Installation_Page.png)
Then open the file you downloaded. You should then be prompted to follow some instructions to complete the installation of VScode. When you install VScode you should be able to open the app to page that looks like this.
![](/lab1-screenshots/VScode_Installation.png)
You may need to install certain extensions in order to use certain languages. For using ssh/scp no additional extensions are necessary.

---

## Step 2: Remotely Connecting
After installing VScode you are ready to connect to a remote server. Before you begin make sure you know to login creditinals for the accound you're logging into. For this class the username is in the form of **cs15lsp22xx@ieng6.ucsd.edu**. If you need to find your account information for cs15l class go to this [*link*](https://sdacs.ucsd.edu/~icc/index.php).

Open a terminal in VScode by clicking Terminal --> New Terminal. You can also do these steps on your computers default terminal as well. Once at the terminal type in the following code `ssh username@ieng6.ucsd.edu` and press enter. Here is an example

```
$ ssh cs15lsp22abc@ieng6.ucsd.edu
```

You will then recieve a message similar to this on the terminal
```
The authenticity of hosy 'ieng6.ucsd.edu (128.54.70.227)' can't be established
RSA Key fingerprint is
SHA256:ksruakjkwerakjlaewrjlaskdjfjjoweSDLAJkjkLA/1x99asjkelwa
Are you sure you want to continue connecting (yes/no)?
```
Type `yes` into the terminal and press enter. The terminal will then ask for your password and you should type it in. Note the cursor will not move when typing the password. Once you enter the password you would have successfully connected with the remote server! The full process should look something similar to this. *Note this image was taken after my first log in attempt. I had already answered the prompt above hence it doesn't appear in this image.*

![](/lab1-screenshots/Remote_Connecting.png)

---

## Step 3: Trying Some Commands

After connecting with the server you should try some unix commands to see if you're able to interact with the server properly. Here is a table of unix commands for you to try.

| Syntax      | Description |
| ----------- | ----------- |
| ls          | Lists the files in the current directory       |
| cd   | Changes the directory        |
| cd~   | Change to the home directory |
| cp    | Copy a file |
| cat   | view or create a file |
| mkdir | make a directory |
| pwd   | print a working directoy |

Here is an example of me running commands on the server shell.
![](/lab1-screenshots/Trying_Commands.png)

---
## Step 4: Moving Files with scp
SCP is a tool that can be used to move a file from a local computer to a server. To use SCP first create a file in a local directory. Then open the terminal in the current directory the file is stored in (Hint: use cd to achieve this). Then in the terminal type in the following command.
```
scp JavaFile.java cs15lsp22xx@ieng6.ucsd.edu:~/
```
Lets break down this code a bit. `scp` calls the scp command which as we explained previously allows you to move files from local computer to remote server. `JavaFile.java` is the name of the file being move. `cs15lsp22xx@ieng6.ucsd.edu` is the server that we want to send it to. `~/` refers to the directory that we want the file to be stored in. In this case the home directory. 

Once you enter this command you will need to type in your password like you did for using ssh. After typing in your password you should get an output of the name of the file that was moved. For example,
```
JavaFile.java
```

In order to check if the file was moved to the remote server its good to log into the server using the instructions in [step 2](#step-2-remotely-connecting). An example of this process can be found in the image below. *Note this image was created after setting an SSH Key ([step 5](#step-5-setting-an-ssh-key))*. 
![](/lab1-screenshots/Using_SCP%3ASSH.png)

---

## Step 5: Setting an SSH Key
As you may have noticed, using ssh and scp can sometimes be annoying because you have to constantly type in your password to use it. Well, there is a way to set up your computer so you don't have to do that. You can use a program called `ssh-keygen` which creates public and private keys on your computer. 

On the terminal type and enter in the following command
```
ssh-keygen
```
You will then be asked to enter passphrase. **DO NOT ENTER A PASSPHARSE.** Just click enter and it will ask you to verify your passphrase. Click enter again and you should get an output similar to this.
![](/lab1-screenshots/keygen_output.png)

Next we need to copy the *public* key and move it to the .ssh directory of the server. First log in to the server using ssh. Then enter `mkdir .ssh` on the server terminal. Then log out of the server.

Once you logged out enter the following command on the terminal
```
scp /Users/<user-name>/.ssh/id_rsa.pub cs15lsp22xx@ieng6.ucsd.edu:~/.ssh/authorized_keys
```
You will need to enter your password to exectute this command. Once this command is executed you should be able to use ssh and scp without entering a password. Note that it may take a few minutes before you're able to log in without a password. Here is an image of me doing the process listed above. 
![](/lab1-screenshots/keygen.png)

---

## Step 6: Optimizing Remote Running
From using ssh and scp you'll eventually notice that it can be tedious creating a file, saving it, and moving it between the remote server and local computers. In this section I will illustrate a method that I found to be efficient is moving files between computer and server.
The first command that should be entered is the following.
```
scp fileName.java cs15lsp22xx@ieng6.ucsd.edu:~/; ssh cs15lsp22xx@ieng6.ucsd.edu
```
This will move the file to the server and log you into the server.
Next you should enter the following command on the server terminal.
```
javac fileName.java; java fileName
```
This will then run the file on the server computer. I found that using these commands were the most efficient in doing remote running. An image of this process can be found below.
![](/lab1-screenshots/Optimization.png)

---
## Wrapup
I hope you found this blog to be of use to you. The main steps illustrated in this blog are important for being able to work with a server computer. SSH/SCP is one of many technologies that allow you to connect and work with a server computer. It is important as computer scientists to gain some familiarty of these technologies. 