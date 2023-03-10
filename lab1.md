# Lab Report 1

## How to get remote access to your class's computer using ***ieng6.***

![image](https://user-images.githubusercontent.com/122419405/212500401-3d154f70-efa4-48fa-81aa-8fe2d4eab585.png)

Buenas! I'm Kristhian Ortiz, and this is a tutorial about how to log into a course-specific account on ieng6.  
You'll have to go through this process every time you take a new class that requires you to access their computers remotely.  
Note: Make sure your class account is ready to rock!

### 1) Installing VS Code and Git.

> Here's where to download [Visual Studio Code.](https://code.visualstudio.com/)
> 
> Here's where to download [Git for Windows.](https://gitforwindows.org/)

After downloading, open both files and follow the prompts so you have the actual applications installed.  
Note: You need to login with an account for VS Code, I'd reccommend doing so with your class account.

![image](https://user-images.githubusercontent.com/122419405/212501909-892b0b1a-667b-470e-8e68-253c75076278.png)

Next Step will be to migrate Git into VS Code so we can use them together.  
(Git is a terminal, so we're basically changing VS Code's terminal so it alligns with the class language).

### 2) Setting up Git in VS Code to access your class computer remotely - using ***ieng6***.

(Technically, we're doing SSH - Secure Shell - which is a secure way to access computers remotely).  
* Open VS Code original terminal (so we can override it with git) using ``Ctrl + ` ``
* Open Command Pallete using `Ctrl + Shift + P`
* Type: `Select Default Profile.`  

![image](https://user-images.githubusercontent.com/122419405/212502441-55707948-a1b7-408a-8232-b2de330e0825.png)

* Select `Git Bash.`  

![image](https://user-images.githubusercontent.com/122419405/212502453-34d9ed02-8540-48c7-b496-2887af74a2fa.png)

#### You just set up Git terminal in VS Code!  
There's a `dropdown` next to the `+` icon in the upper right hand corner of the VS Code original terminal, click it.  
Select `Git Bash` to start using git terminal instead!

![image](https://user-images.githubusercontent.com/122419405/212502487-36cd01c9-91c3-4f60-a5de-4ac8e86552bc.png)


#### Now let's establish that remote connection!  
* Type: `ssh [name of account]@***ieng6***.[domain].edu` (For me, it would be cse15lwi23aue@ieng6.ucsd.edu).  
(What u just typed creates a ssh connection from the name of account to the ieng6 server on the specified domain).  
* Type `yes` to affirm connection if this is your first time logging in.  
* Log in with your password.  
(The password will not show, even if you think you're not typing, trust me, you are. Just invisibly type it and press enter).

![image](https://user-images.githubusercontent.com/122419405/212502558-59c8ca23-f9ad-4ab0-b7fc-a76bcaa62022.png)


#### You are now logged into your class' computer!  
Let's test that out!

### 3) Testing out some commands.
Here's a list of some commands you can try with your computer (using VS Code original terminal), and with the class computer (using git bash).
* cd
* ls -lat
* ls -a
* pwd
* cp
* mkdir

![image](https://user-images.githubusercontent.com/122419405/212502715-5cda5e17-3c9a-4419-8624-9591210adc42.png)

> To terminate connection simply type `Ctrl + D` or `exit`



