# Github and SSH

## By: Adhithya Ananthan
In this lab report I will go over ways to use github on a remote computer. I will also cover how to streamline ssh configuration and efficiently moving files through scp. The overall learning goals of this lab are to become more familiar with using git and github on a remote server

## Objective 1: Streamlining SSH Configuration
![](/labreport3-screenshots/option1/addingConfig.png)

In order to ssh into remote servers using only the host name (in this case ieng6) we need to add a config file to the `.ssh` directory. We can use the `cat` command to create a config file. Shown above is the config file added to my `.ssh` directory. 

![](/labreport3-screenshots/option1/editingConfig.png)

We can then use the `vim` command to edit the file. `vim` is a text-editor that allows you to edit files on the command line. In the picture above, we can see that I used `vim` to edit my configurations.

![](/labreport3-screenshots/option1/loginSSH.png)

Once the configurations are set we can then ssh into the server easily. The picture above shows me connecting to the remote server using only `ssh ieng6`.

![](/labreport3-screenshots/option1/loginSCP.png)

And this is me doing a similar thing but using `scp` instead of `ssh`. The full command that I wrote was `scp someText.txt ieng6:~/`.


## Objective 2: Setup Github Access from ieng6

![](/labreport3-screenshots/option2/gitPushNotWorking.png)
Intially when trying to push a change to github via a remote server we get this error message. This is because we need to configure a remote server, in this case ieng6, to be able to do pushes to github.

![](/labreport3-screenshots/option2/usingKeygen.png)
In order to configure the remote server we need to create rsa keys on the remote server. Shown above is me using `ssh-keygen` to create the keys needed.

![](/labreport3-screenshots/option2/keyInRemoteComputer.png)

![](/labreport3-screenshots/option2/validKeyGithub.png)

The two images show where the public key is set in the remote server and github respectively. The first image also shows where the private key is stored on the remote server. We need these keys in order for us to commit and push changes made on the remote server to github. 

![](/labreport3-screenshots/option2/usingCommitandPush.png)

Once we added the keys and configured everything properly, I was able to commit and push changes to github to the remote server. The link for this commit can be found [here](https://github.com/adhi0331/markdown-parser/commit/a1d1fd8eceb693334070e98d96471910676b76fb)


## Objective 3: Copy Whole Directories with `scp -r`

It can be tedious transferring files to a remote server using `scp` since we have to do it one by one. Luckily there is a way to transfer entire directories to a remote server using `scp -r`

![](/labreport3-screenshots/option3/scpMarkdownParse.png)

In the above picture I used the command `scp -r . cs15lsp22aud@ieng6.ucsd.edu:~/copied-markdown-parse` to move the markdown parse directory from my local computer to the remote sever. When using the `scp -r` it tells the computer to work through the files recursively. Hence all the files one by one to the remote server.

![](/labreport3-screenshots/option3/runningCopiedMarkdownParse.png)

We can then see in this image that I was able to run the copied markdown parse file test in the remote server after I ssh into it. However doing this could be tedious since it requires me to move it, wait for the server to connect, and then run additional tests to run the tests. 

![](/labreport3-screenshots/option3/oneLine1.png)

![](/labreport3-screenshots/option3/oneLine2.png)

Luckily there is a way to do all of this in one line as shown in the image above. I won't write out the whole command I used since its really long, but essentially I combined the two `scp` and `ssh` commands. To tell the console which commands to run on the remote server I used `--`. This is why we see that the tests ran on the server and not my local computer. 


## Conclusion:

Overall, this lab showed us ways to efficently use a remote server and github. Everything presented in this lab is important in the real-world because it saves time in working on a programming project. Moreover, it allows us to use more powerful tools without comprisiming time. 