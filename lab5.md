# Lab Report 5 - Kristhian Ortiz
## Putting It All Together - Lab 6: Creating a Grading Script
![image](https://user-images.githubusercontent.com/122419405/224521421-a56028b6-8774-4141-b322-94347e1d4da1.png)  

This is my grading script, I will go in detail about what each part of it does, and how and why it works.  

```
CPATH='.;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar'

rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

cd student-submission
if [[ -f ListExamples.java ]]
then
  echo "found ListExamples.java!"
  else exit 1
fi

cat ListExamples.java > class.txt
if grep -Fq "class ListExamples {" class.txt 
then
    echo "found Class ListExamples"
    else exit 2
fi

if grep -Fq "static List<String> filter(List<String> list, StringChecker sc)" class.txt 
then
    echo "found filter method!"
    else exit 2
fi

if grep -Fq "static List<String> merge(List<String> list1, List<String> list2)" class.txt 
then
    echo "found merge method!"
    else exit 2
fi

cp ../TestListExamples.java 'TestListExamples.java'

javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > out.txt 2>&1

if grep -Fq "OK" out.txt
then 
    echo "You passed!"
    else echo "No Bueno, Try Again!" "$(cat out.txt)" 
        exit 3
fi  
```  

First, we store the path we want need to compile the junit tests into a variable so we don't have to type it again.  
```
CPATH='.;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar'
```  

Then I use `rm -rf` to recursively remove any previous submission we stored in the `student-submission` directory.  
Immediately after, I `git clone` the student submission into that folder and print `"Finished cloning"` usinng `echo`.  
> I `cd` into the `student-submission` directory that I just created (where the student submission is stored) so the code after this can work around the student's submission.  
> In other words, I made the student submission's directory my new working directory so I can work with it.  

```
rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

cd student-submission
```  
Here is a screenshot of it working!  
![image](https://user-images.githubusercontent.com/122419405/224583725-a6fb6b1e-c117-485c-89df-3fd846e5dd05.png)   

I then have 4 if statements that check the files inside the student's submission:  
If a file called `ListExamples.java` is found, print so.  
Else, exit 1 (which means there was a general, small error. In this case, there was no file with the exact name `ListExamples.java` found.
```
if [[ -f ListExamples.java ]]
then
  echo "found ListExamples.java!"
  else exit 1
fi
```  

If there is a `ListExamples.java`, I cat that file into one called `class.txt` just so I have access to all the characters comprising this document.  
Why would I need that? For my next if statement!  

If `grep` finds the fixed string I put there (which is a class signature I want the student to have), then it means the class I want the student to have exists, and I can move on to grade it.

``` 
cat ListExamples.java > class.txt
if grep -Fq "class ListExamples {" class.txt 
then
    echo "found Class ListExamples"
    else exit 2
fi  
```  
> ChatGPT got a really good explanation of what `grep -Fq` does, so I'll put that here!  
> 
> ![image](https://user-images.githubusercontent.com/122419405/224584802-67e9e71d-4097-42eb-b5a4-bf67c1d38129.png)  

Then, I want to know if the student has a specific method (the filter method), so I apply the same `grep -Fq` logic.
```
if grep -Fq "static List<String> filter(List<String> list, StringChecker sc)" class.txt 
then
    echo "found filter method!"
    else exit 2
fi
```  

Same for this one, I check that key classes and methods are there.
```
if grep -Fq "static List<String> merge(List<String> list1, List<String> list2)" class.txt 
then
    echo "found merge method!"
    else exit 2
fi  
```  
Here's a screenshot of it working!  
![image](https://user-images.githubusercontent.com/122419405/224585336-10f91b07-dc70-4039-a35e-67354890e03a.png)  

Finally, I proceed to actually grade the assignment — run JUnit tests on it.  

To grade, I copy my tester (which is **one** directory before the current directory (that's why I used `../` and then the name of my tester)) using `cp` into the current directory.  

```  
cp ../TestListExamples.java 'TestListExamples.java'
```

After everything I need (my tester and the student submission) is in my current working directory, I proceed to compile it all, using thae stored path I created at the beginning of my script.
```
javac -cp $CPATH *.java
```  

I run my tester (I grade the student submission) and redirect the output to `out.txt` so I can show the results.  
I use the error redirection `2>&1` so it doesn't throw everything at the terminal, and so that I can show the student what went wrong and why.
```
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > out.txt 2>&1
```  

With the same `grep -Fq` logic that I used in previous if statements, I know that an `OK` will only appear if you passed all the tests, so I aimed to look for that.  
Therefore, If there's an `OK` in `out.txt`, you passed!  
Else, I let the student know that there's something wrong, to try again, and then I show the output using `cat`, which contains the error information.  

```
if grep -Fq "OK" out.txt
then 
    echo "You passed!"
    else echo "No Bueno, Try Again!" "$(cat out.txt)" 
        exit 3
fi  
```  
> The format to use `cat` here is `"$(cat out.txt)"` because the output of the command inside the parenthesis will replace the entire thing.  
> ChatGPT actually explains it really well, too!  
> ![image](https://user-images.githubusercontent.com/122419405/224587411-db3f7333-a81e-47ed-9d3e-38fc81eb9a86.png)  

Here's the screenshot of a submission that failed the test!   

![image](https://user-images.githubusercontent.com/122419405/224587537-038b15eb-68f2-4847-bcbb-b57eebf5ab62.png)   

So, putting it all together, here's a cheap, Gradescope imitation!  

![image](https://user-images.githubusercontent.com/122419405/224590548-47a67164-6e2b-458a-ad5f-6ba307061ee2.png)  
> Fails  

![image](https://user-images.githubusercontent.com/122419405/224590655-e375b97a-f46c-4a99-bb34-e6dc067f2885.png)  
> Passes, like this Last Lab Report 😎





