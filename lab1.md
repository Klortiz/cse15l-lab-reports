# Lab Report 1

## How to get remote access to your class's computer using ***ieng6.***

![image](https://user-images.githubusercontent.com/122419405/212500401-3d154f70-efa4-48fa-81aa-8fe2d4eab585.png)

Buenas! I'm Kristhian Ortiz, and this is a tutorial about how to log into a course-specific account on ieng6.
You will have to go through this process every time you take a new class that requires you to access their folders remotely.
Note: Make sure you have your class account ready to rock!

### 1) Installing VS Code and Git.

> Here's where to download [Visual Studio Code.](https://code.visualstudio.com/)
> 
> Here's where to download [Git for Windows.](https://gitforwindows.org/)

After downloading, open both files and follow the prompts so you have the actual applications installed.
Note: You need to login with an account for VS Code, I'd reccommend doing so with your class account.

Next Step will be to migrate Git into VS Code so we can use them together.
(Git is a terminal, so we're basically changing VS Code's terminal so it alligns with the class language).

### 2) Setting up Git in VS Code to access your class computer remotely - using ***ieng6***.

(Technically, we're doing SSH - Secure Shell - which is a secure way to access computers remotely)
> Open VS Code original terminal (so we can override it with git) using ``Ctrl + ` ``
> 
> Open Command Pallete using `Ctrl + Shift + P`
> 
> Type: `Select Default Profile.`
> 
> Select `Git Bash.`
> 
> (You just set up Git terminal in VS Code!)
> 
> There's a `+` icon in the upper right hand corner of the VS Code original terminal, click it.
> 
> Select `Git Bash` to start using git terminal instead!

#### Now let's establish that remote connection!

> Type: `ssh [name of account]@***ieng6***.[domain].edu` (For me, it would be cse15lwi23aue@ieng6.ucsd.edu).

(What u just typed creates a ssh connection from the name of account to the ieng6 server on the specified domain).

> Type `yes` to affirm connection and log in with your password.

(Note that the password will not show, even if you think you're not typing, trust me, you are. Just invisibly type it and press enter).

> 
> 




### 3) Testing out some commands.


