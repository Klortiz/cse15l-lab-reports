# Lab Report 3
## Researching Commands

![image](https://user-images.githubusercontent.com/122419405/218331294-82fceef0-2f40-430c-ba43-40fdf6ce97ab.png)

Besides the well-known `-name` command-line option, the `find` command-line has A LOT more options to offer.  
Here are four of them:

1)  -empty
According to [*GeeksForGeeks*](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/#:~:text=4.-,Search%20for%20empty%20files%20and%20directories.,-%24%20find%20./GFG%20%2Dempty), the `-empty` command-line option searches for all empty files AND directories.  
This is extremely useful to maintain your directories organized and less overwhelming to the users.  
Here's how it works (Syntax)  
To find a file
`$ find -empty `

To 


2)  -delete
Let's say you found those empty files and want to delete them. Well, that's exactly what `-delete` can do for you!
**Warning:** According to [*Linode*](https://www.linode.com/docs/guides/find-files-in-linux-using-the-command-line/#how-to-find-and-delete-a-file-in-linux), you need to be VERY careful with this, as you can delete ANYTHING that matches what you specified.

3)  -mtime (***m***odified ***time***stamp)  
This is that *ChatGPT* search the professor is so excited about.  
For his sake, I'm going to include a screenshoot of the important output:  
> Basically, I'll let *ChatGPT* take over the explanation of `-ntime`

![image](https://user-images.githubusercontent.com/122419405/218333822-d9003497-2576-402b-9b1c-783f5e8c4861.png)

> (I want a full grade so I'm taking over again wuajaja)  

In other words, `-ntime` outputs the time that the speficied file was ***modified***.  
I emphasize that because it's easy to confuse with time of creation.  
Here's how it works!



4)  -regex (***reg***ular ***ex***pression)


