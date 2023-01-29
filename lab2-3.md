# Lab Report 2 - Servers and Bugs

## Part 1
### This is the code of my `StringServer` 
![image](https://user-images.githubusercontent.com/122419405/215237900-c6a23e14-16dc-4862-a824-831d6b6589f0.png)

### Here is two screenshots of using `/add-message`
![image](https://user-images.githubusercontent.com/122419405/215237926-6071ba0d-70c2-4607-81fe-aff5b936fd8c.png)  
The methods called in my code are `getPath()` and `contains()` to check whether you're using the `/add-message` command to add your string to my `word` string.
I then use an if statement to execute two possible situations (first screenshot prooves the first situation).
If word is null, set it equal to whatever your first input is. Without this if statement, you would be adding your string to null. In other words, `/add-message?s=hiii` would return `nullhiii` and not `hiii`

![image](https://user-images.githubusercontent.com/122419405/215237960-dc46be95-542e-417c-89df-e3d817b46e01.png)  
The second part of the if statement is executed and showed in this second screenshot.  
If `word` is not null, then just += whatever your second, third...n input is.
Finally, I use `+ System.lineSeparator()` after the input you want to add to perform the function of what `String.format("%s \n")` does. 

I know strings are immutable, so what's happening is that the String variable `word` changes its pointer to a new String that contains the sum of what was currently stored and whatever your input is. We're seeing a new String every time you add a message, and the `System.lineSeparator()` helps with line breaks to make your input look like it's a new and individual one (but in reality is just a big string with all those inputs).

- Here, I tried to input non-string values such as URIs and ints.
![image](https://user-images.githubusercontent.com/122419405/215237987-0861b494-0c0b-4a8e-8289-2e9153755ad1.png)

![image](https://user-images.githubusercontent.com/122419405/215238004-9f0d1346-b8a2-4fde-ae18-22956749fd0e.png)

Turns out, they were just turned into strings and added perfectly!
This is because `System.lineSeparator()` is the same as `"\n"`, and when you add [any variable] + [a string] you get a string back.


## Part 2

### I will use append bug from the LinkedListExamples.java
(before pick)

If you look carefully at the while loop, it will never end because it will keep creating new objects that return its condition true all the time. Thus, a failure-inducing input would be using append once, twice... until we get the one that triggers the infinite loop.
(Note that we're lucky here because it breaks after appending three times, but if there were to be a million appends to do, then a for loop should do this).

(junit pic that breaks the code) - in markdown

According to the code, appending once doesn't induce a failure because if LinkedList is null, then it just makes your input its first value. Adding two times doesn't induce a failure because there's code built for that specific case of having one element already when append gets called. 

(junit that don't breaks the code) - in markdown

So, after running these tests we find the symptom:
(junit after running) - ss

The bug is located at the end of the while loop, that `n.next = new Node(value, null);`
Because it will keep expanding the list, the loop will keep running true because it's programmed to keep looking for the end. But if you keep expanding the end as you go, you'll never reach it. 

Solution: Moving it to the outside, so you can first find the end, and then expand the list (append) at that index (at `n.next`).

(after code) - in markdown

![image](https://user-images.githubusercontent.com/122419405/215238434-28d487c4-527b-4669-b7bc-59f3fb89fa49.png)

# Part 3
I learned so much from lab 2 and 3, I'll do a bulleted list!
* I learned how to `ssh` to a server.
* I learned how to `scp`, how to copy files from my computer to the server and vicevesa (this is what hackers do!)
* I learned how to deploy a webserver!
* I learned what all those letters in the search bar mean.
* I learned how to change a website through the search bar (as if the search bar was a little terminal!)
* I learned about URI and how to use some of its methods like `getPath()` and `getQuery()`
* 
* 
