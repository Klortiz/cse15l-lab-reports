# Lab Report 3
## Researching Commands

![image](https://user-images.githubusercontent.com/122419405/218331294-82fceef0-2f40-430c-ba43-40fdf6ce97ab.png)

Besides the well-known `-name` command-line option, the `find` command-line has A LOT more options to offer.  
Here are four of them:


`1) find -empty`  
According to [*GeeksForGeeks*](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/#:~:text=4.-,Search%20for%20empty%20files%20and%20directories.,-%24%20find%20./GFG%20%2Dempty), the `-empty` command-line option searches for all empty files AND directories.  
This is extremely useful to maintain your directories well organized and less overwhelming to the users.  

Here's how it works (Syntax):  
To find an empty file among all the files of all directories and sub-directories, you simply:  
`$ find -empty `  

![image](https://user-images.githubusercontent.com/122419405/218336223-157b7996-f285-470b-935a-0a76bfecca71.png)  

To find an empty file within a specific directory,  
you specify the path up to that directory before calling `-empty` like this:  
`$ find ./directory -empty`  

![image](https://user-images.githubusercontent.com/122419405/218336247-c1c3b7f2-3adf-4a1d-8fa0-0edf40aa3bad.png)  
> no-uwu.txt is an empty file I added for test purposes only. It's empty because there's no uwu on it.


`2) find -delete`  
Let's say you found those empty files and want to delete them. Well, that's exactly what `-delete` can do for you!  
**Warning:** According to [*Linode*](https://www.linode.com/docs/guides/find-files-in-linux-using-the-command-line/#how-to-find-and-delete-a-file-in-linux), you need to be VERY careful with this, as you can delete ANYTHING that matches what you specified.  

To use it, we need to combine `-delete` with the already known `-name` command-line option to make sure we're deleting the correct files.  
Hence, the code looks like this:  
`$ find -name "file" -delete`  

Let's say we want to delete my `no-uwu.txt` file, the syntax will be this:  
`$ find -name "no-uwu.txt" -delete`  

![image](https://user-images.githubusercontent.com/122419405/218337136-94a66ee8-9a48-4425-ac14-dda301d671ae.png)  

But this still would delete all files that fall into the name you searched for,  
if you want to delete a specific file that has a unique difference (i.e. delete uwu from a directory that has Uwu1, uWu-34, uwu, and uwU_awa),  
you can use `-iname` instead of `-name`. According to [*StackExchange*](https://unix.stackexchange.com/questions/230952/what-is-the-difference-when-using-find-between-name-and-iname#:~:text=but%20the%20match-,is%20case%20insensitive,-.%20%20For%20example%2C%20the) and [*cyberciti.biz*](https://www.cyberciti.biz/faq/linux-unix-how-to-find-and-remove-files/#:~:text=ADVERTISEMENT-,Find%20And%20Remove%20Files%20With%20One%20Command%20On%20Fly,-The%20basic%20find), the syntax is this:  
`$ find -iname "specificCaseSensitiveName" -delete`  

![image](https://user-images.githubusercontent.com/122419405/218339434-d1b1555d-bf41-4095-a231-e5615742f67c.png)


`3) find -mtime` (***m***odified ***time***stamp)  
This is that [*ChatGPT*](https://openai.com/blog/chatgpt/) search the professor is so excited about.  
For his sake, I'm going to include a screenshoot of ChatGPT's relevant output:  
> (Basically, I'll let *ChatGPT* take over the explanation of `-mtime`)

![image](https://user-images.githubusercontent.com/122419405/218333822-d9003497-2576-402b-9b1c-783f5e8c4861.png)

> (I want a full credit, so I'm taking over again wuajaja)  

In other words, `-mtime` outputs the time that the speficied file was last ***modified***.  
> Note: I emphasize that because it's easy to confuse this with *time of creation.*  

Here's how it works!  
`$ find -mtime daysUpToToday-1`  

I say that the argument after `-mtime` is `((days up to today) - 1)` because `-mtime` counts one day after 24 full hours of the time it's been modified (or created if you never modified it).  

For instance, I **just** imported the `/skill-demo1-data` directory to my personal computer to make this lab report.  
Hence, passing an argument of `0` will give me all the files within that directory.  

![image](https://user-images.githubusercontent.com/122419405/218340459-04bb59fd-1b4f-4342-9ca5-da0f5231319d.png)  

A more detailed example would be this:  
![image](https://user-images.githubusercontent.com/122419405/218340535-477081f0-c2db-41ab-a887-bd8b7d058b72.png)

> See where it says *date modified*? That's where you're going to count the 24 full hours.  

Right now is 2:16pm in 2/12/23. So it's technically been 16 days since 1/27/23.  
But since I last modified my StringServer.java file at 5:46pm, the argument I need to pass on is ((16) -1) which is 15.  

![image](https://user-images.githubusercontent.com/122419405/218340646-ff009df8-9aea-4cff-99f0-b8a44e17c8ab.png)

And there u go;)








`4) find -regex` (***reg***ular ***ex***pression)  
[*ss64.com*](https://ss64.com/bash/find.html#:~:text=to%20using%20%27/%27%20instead.-,%2Dregex%20pattern,-File%20name%20matches)'s explanation is a little off, so I'll try to say what I got from that.  
Basically, `-regex` matches the word (input) with all the files, directories, and sub-directories in the current working directory.  
The tricky part is that this matches the whole path, not just the word, and that it's not a word what you're actually inputting, it's a specific *patten*.  

What I just said was the hardest to figure out, I had to resort to [*StackOverflow*](https://stackoverflow.com/questions/6844785/how-to-use-regex-with-find-command#:~:text=The%20%2Dregex%20find%20expression%20matches%20the%20whole%20name%2C%20including%20the%20relative%20path%20from%20the%20current%20directory.) to see the how this command-line option actually works.  
The problem with *StackOverflow* is that it gave an example of an image, not a file.

So, according to me (after playing around with `-regex`),  
I found that the input should be the *last syllable* of the last word in the file you want to find/match.  
Also, If the file you want to find ends in a file-type (i.e. *.pdf*, *.txt*) then you don't have to include a dot at the end of the input  
(before the single quote).  
You'll see what I'm talking about with some examples:

To search for a file with no specific type-file at the end of its name, you have to follow this syntax:  
`$ find -regex '.*syllable.'` (Note that there's a dot at the end of the syllable)  

There's a file inside `/written_2` that I know ends with `berlitz1` and `berlitz2`, let's match them!
![image](https://user-images.githubusercontent.com/122419405/218335359-84194a6d-0c22-4e2c-ab9d-10fb307ab769.png)

> Notice how it doesn't work without a period

Let's say you want the specific file, but instead of a syllable, it has a number at the end.  
For the input, you need to include the **FIRST** letter of the last syllable **AND then** the number to get the specific file you want.
We know that there's a `berlitz1` somewhere, so we match it like this:  

![image](https://user-images.githubusercontent.com/122419405/218335675-7ae3a863-0a5f-4539-8ce4-26d376c601b1.png)
> There's NO period before single quote.
> You know what else doesn't want periods at the end of their input? 
> Type-files! (That's next bonus example).

To search for a file with a file-type at the end of its name, you do this:
`$ find -regex '.*fileType'` (Note that there's no period at the end of the file-type)  
![image](https://user-images.githubusercontent.com/122419405/218335773-dfee7a1b-e1c6-4b7b-872d-b7ae7bce58a5.png)






