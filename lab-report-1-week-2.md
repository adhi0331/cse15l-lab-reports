# Accessing Remote Servers
In this blog, we will explore how to remotely access servers from our local computer. Understanding how to do this is important because in our future careers we will be required to access organizations servers to do various tasks. The following sections provide a step-by-step guide on how to use ssh/scp technologies.

---

## Step 1: Installing VScode
VScode is commanly used IDE that allows you to write programing scripts. To install VScode go to this [*link*](https://code.visualstudio.com/download) and download it based on the computer you are using (Windows, Linux, or Mac). 
![](/lab1-screenshots/VSCode_Installation_Page.png)
Then open the file you downloaded. You should then be prompted to follow some instructions to complete the installation of VScode. When you install VScode you should be able to open the app to page that looks like this.
![](/lab1-screenshots/VScode_Installation.png)
You may need to install certain extensions in order to use certain languages. For using ssh/scp no additional extensions are necessary.

---

## Step 2: Remotely Connecting
After installing VScode you are ready to connect to a remote server. Before you begin make sure you know to login creditinals for the accound you're logging into. For this class the username is in the form of **cs15lsp22xx@ieng6.ucsd.edu**. If you need to find your account information for cs15l class go to this [*link*](https://sdacs.ucsd.edu/~icc/index.php).

Open a terminal in VScode by clicking Terminal --> New Terminal. You can also do this on your computers default terminal as well. Once at the terminal type in the following code `ssh username@ieng6.ucsd.edu`.