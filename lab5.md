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

Then we use rm -rf to recursively remove any previous submission we stored in the student-submission directory.  
Immediately after, I git clone the student submission into that folder and print "Finished cloning" usinng echo.  
> I cd into the student-submission directory that I just created (where the student submission is stored) so the code after this can work around the student submission.  
> In other words, I made the student submission's directory my new working directory so I can work with it.  

```
rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

cd student-submission
```  
Here is a screenshot of it working!  
![image](https://user-images.githubusercontent.com/122419405/224583725-a6fb6b1e-c117-485c-89df-3fd846e5dd05.png)   

I have 4 if statements:  
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



```  
cp ../TestListExamples.java 'TestListExamples.java'

javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > out.txt 2>&1
```

```
if grep -Fq "OK" out.txt
then 
    echo "You passed!"
    else echo "No Bueno, Try Again!" "$(cat out.txt)" 
        exit 3
fi  
```  

