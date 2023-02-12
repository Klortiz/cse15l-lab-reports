# Lab Report 3
## Researching Commands

![image](https://user-images.githubusercontent.com/122419405/218331294-82fceef0-2f40-430c-ba43-40fdf6ce97ab.png)

Besides the well-known `-name` command-line option, the `find` command-line has A LOT more options to offer.  
Here are four of them:

`1) find -empty`  
According to [*GeeksForGeeks*](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/#:~:text=4.-,Search%20for%20empty%20files%20and%20directories.,-%24%20find%20./GFG%20%2Dempty), the `-empty` command-line option searches for all empty files AND directories.  
This is extremely useful to maintain your directories organized and less overwhelming to the users.  
Here's how it works (Syntax)  
To find a file
`$ find -empty `

`2) find -delete`  
Let's say you found those empty files and want to delete them. Well, that's exactly what `-delete` can do for you!
**Warning:** According to [*Linode*](https://www.linode.com/docs/guides/find-files-in-linux-using-the-command-line/#how-to-find-and-delete-a-file-in-linux), you need to be VERY careful with this, as you can delete ANYTHING that matches what you specified.

`3) find -mtime` (***m***odified ***time***stamp)  
This is that *ChatGPT* search the professor is so excited about.  
For his sake, I'm going to include a screenshoot of the important output:  
> (Basically, I'll let *ChatGPT* take over the explanation of `-ntime`)

![image](https://user-images.githubusercontent.com/122419405/218333822-d9003497-2576-402b-9b1c-783f5e8c4861.png)

> (I want a full grade so I'm taking over again wuajaja)  

In other words, `-ntime` outputs the time that the speficied file was ***modified***.  
I emphasize that because it's easy to confuse with time of creation.  
Here's how it works!



`4) find -regex` (***reg***ular ***ex***pression)  
[*ss64.com*](https://ss64.com/bash/find.html#:~:text=to%20using%20%27/%27%20instead.-,%2Dregex%20pattern,-File%20name%20matches)'s explanation is a little off, so I'll try to say what I got from that. Basically, `-regex` matches the word (input) with all the files, directories, and sub-directories in the current working directory. The tricky part is that this matches the whole path, not just the word, and that it's not a word you're actually inputting, it's a specific *patten*.  
This was the hardest to figure out, I had to resort to [*StackOverflow*](https://stackoverflow.com/questions/6844785/how-to-use-regex-with-find-command#:~:text=The%20%2Dregex%20find%20expression%20matches%20the%20whole%20name%2C%20including%20the%20relative%20path%20from%20the%20current%20directory.) to see the how this command-line option actually works. The problem with that is that *StackOverflow* gave an example of an image, not a file.

So, according to me (after playing around with `-regex`), I found that the input should be the *last syllable* of the last word in the file you want to find/match.
Also, If the file you want to find ends in a file-type (i.e. *.pdf*, *.txt*) then you don't have to include a dot at the end of the input (before the single quote).
You'll see what I'm talking about with some examples:

To search for a file with no specific type-file at the end of its name, you have to follow this syntax:  
`$ find -regex '.*syllable.'` (Note that there's a dot at the end of the syllable)


To search for a file with a file-type at the end of its name, you do this:
`$ find -regex '.*fileType'` (Note that there's no period at the end of the file-type)



