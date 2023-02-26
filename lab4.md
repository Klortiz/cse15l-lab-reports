# Lab Report 4 - Kristhian Ortiz
## Competition Tasks On My Own
![DALL·E 2023-02-22 18 06 31 - a student sitting in a desk with a laptop working on code in a room with the sunset through the window](https://user-images.githubusercontent.com/122419405/221385926-139309c1-c5c0-4fc8-b7ed-007e5560b9a9.png)  
> This picture was made by the Open AI DALL-E

### There are nine steps on this competition:
(((For each numbered step take a screenshot, and write down exactly which keys you pressed to get to that step.)))  

## 1) Setup - Delete any existing forks of the repository from your account.  
If you have a fork already, go to its settings in github and scroll all the way down to delete it:
![image](https://user-images.githubusercontent.com/122419405/220795828-09b36163-aa98-4582-847e-803a14accb0e.png)  
![image](https://user-images.githubusercontent.com/122419405/220795947-e3555972-7136-4fb2-9ddc-cec8deb48a20.png)  
If you didn't have a fork, or you just deleted the old one, go to the [original repository ](https://github.com/ucsd-cse15l-w23/lab7) to fork it (details below).  

## 2) Setup - Fork the repository.   
Once you clicked [that link](https://github.com/ucsd-cse15l-w23/lab7), click the `Fork` button in the upper right hand corner.  

![image](https://user-images.githubusercontent.com/122419405/221386285-38ec0078-a659-4b80-96c4-ff574b7ca982.png)  

The last step to create the fork is to give it a name (there's one by default already) and an optional description.  
![image](https://user-images.githubusercontent.com/122419405/221386407-1b86d5b0-ffff-49bc-9436-04fc8e3290c5.png)
Click the `Create Fork` button.

## 3) The real deal - Start the timer!  
![image](https://user-images.githubusercontent.com/122419405/221386475-7ef3c06c-74a2-408f-a58e-348531349398.png)  
> It's a big image so you know where this competition actually starts among all the easy-to-get-lost pictures in this lab report.

## 4) Log into ieng6.   
- Open Visual Studio Code's terminal using `Ctrl + back-quote`. 
- Type `ssh` `cs15lwi23[your unique letters here]@ieng6.ucsd.edu` 
- Press `Enter`
- Type your password.
- Press `Enter`
> Note that if you want to avoid all of this, you can refer to the class website to [set up ssh keys for ieng6 and github](https://ucsd-cse15l-w23.github.io/week/week7/#:~:text=Command%2DLine%20Setup-,Generating%20SSH%20Keys%20for%20ieng6,-With%20the%20setup).  

## 5) Clone your fork of the repository from your Github account.   
Because you will work with the fork you just made, on its main page, click on `code` to copy the `ssh` link to clone.  
![image](https://user-images.githubusercontent.com/122419405/221386972-614837d4-8bf3-4158-8467-4123d5ba6689.png)  

On the terminal, already connected to the server, type `git clone` and paste the ssh link. Hit `Enter`.  
![image](https://user-images.githubusercontent.com/122419405/221387045-7d9dbdae-60fd-42bd-b0c3-6b8c858fd136.png)  
> I always type `ls` to know what changed, where I'm at, and to display the names of what I will be working on. It's a good habit.  

## 6) Run the tests, demonstrating that they fail.   
cd into lab7 (like this: `cd lab7`) so we can compile its java files and run junit. (Remember to `ls`)  

![image](https://user-images.githubusercontent.com/122419405/221387196-00007ddf-ea2b-40a6-ae56-20a475582811.png)   

If you go to [week 3](https://ucsd-cse15l-w23.github.io/week/week3/#:~:text=you%20run%20them%3A-,MAC%20USERS%3A,-local%20%24%20javac%20%2Dcp), you can find the code needed to compile all java files and run Junit.  
The code is the following: 
To compile, I typed `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`
To run Junit, I typed `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore` + the name of the junit file (in this case, is `ListExamplesTests`.

![image](https://user-images.githubusercontent.com/122419405/221387385-e86a9a65-b005-4cfb-931f-7f9f15698661.png)  
> Notice how you don't write `.java` when you run the tester.  
Next, debugging!

## 7) Edit the code file to fix the failing test.  
If we analyze the error message, we can track down the problem.  

![image](https://user-images.githubusercontent.com/122419405/221387634-6fc24e27-36ee-4d8a-b103-97a4e9491b3e.png)  
> I'm just using visual studio code to show what I mean, but this can be read from the same error message: "` at ListExamplesTests.testMerge2(ListExamplesTests.java:19)`".  

Junit says that there's a problem with line 19, which uses the merge method.
There's many ways to determine the problem with the merge method from the command line.
I typed `cat ListExamples.java` to locate the merge method.  

![image](https://user-images.githubusercontent.com/122419405/221387859-eb2f7671-c9c1-4867-b53a-3674c6fa2dbe.png)   

If we look at the failure message, the problem is in line 42 of the ListExamples.java file.  
I typed `wc -l ListExamples.java` to see how many lines I was dealing with.  

![image](https://user-images.githubusercontent.com/122419405/221388009-7a44d241-98fb-4435-8c2e-5cb84d2f4b37.png)  

To make sure I counted the lines right (and edit the error later on), I typed `nano ListExamples.java` and manually counted the lines from bottom up.  
> Also, nano displays the number of lines of the file before you start moving around.  

So, this is line 42.  

![image](https://user-images.githubusercontent.com/122419405/221388092-aa9cbd21-cced-463d-b2c8-bf4ab34a9729.png)  

My logic was: "The first while loop was tested in the Junit test and passed, what's different from the while loop that failed?"  
A picture says more than a thousand words, so here is what I found:  

![image](https://user-images.githubusercontent.com/122419405/221388151-0a6bea6e-1089-40f0-b385-fdd13927ea75.png)  

I changed that `1` for a `2` using `nano ListExamples.java` (I was already there).  
To do that, I moved the `left` arrow key until the white pointer was on the right side of the `1` I wanted to delete.  
> The white (square) pointer deletes and types on the space before it.  

![image](https://user-images.githubusercontent.com/122419405/221388264-2e374cb5-1a19-4c56-81bc-68dc3a95bd4f.png)  
I pressed the `delete` key and typed `2` instead.
I pressed `Ctrl + O` to save the file.
I pressed `Enter` to save the file with the same name.
I pressed `Ctrl + X` to exit.

Thank you, next!

## 8) Run the tests, demonstrating that they now succeed.  
I didn't want to type the above command to compile all java files and run the JUnit files (`javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` and `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTest`) so I just move the `up` arrow key until I found them in my history and pressed `Enter` for both of them.  

![image](https://user-images.githubusercontent.com/122419405/221388691-14819aad-c77f-4783-a8d9-41bb09883362.png)  
It passes!  

## 9) Commit and push the resulting change to your Github account (you can pick any commit message!)  



For special characters like <enter> or <tab>, write them in angle brackets with code formatting. 
Then, summarize the commands you ran and what the effect of those keypresses were.
