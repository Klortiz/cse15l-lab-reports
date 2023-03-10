# Lab Report 2 - Servers and Bugs By Kristhian Ortiz

![image](https://user-images.githubusercontent.com/122419405/215300493-75df1c8a-e04e-47a7-9cb8-cdb94e6468d7.png)


## Part 1
### This is my `StringServer` 
![image](https://user-images.githubusercontent.com/122419405/215237900-c6a23e14-16dc-4862-a824-831d6b6589f0.png)

Besides getting a port number to start up the server, the main methods called in my code are found in the second if statement.  
Both `getPath()` and `contains()` check whether you're using the `/add-message` command to add your string to my `word` string.  
I then use an if statement to execute two possible situations (first screenshot proves the first situation).  
If `word` is null, set `word` equal to whatever your first input is. 

> Note: Without this if statement, you would be adding your string to null.  
> In other words, `/add-message?s=hiii` would return `nullhiii` and not `hiii`

Typing http://localhost:1313/ `add-message?s=hiii` returns:  

![image](https://user-images.githubusercontent.com/122419405/215237926-6071ba0d-70c2-4607-81fe-aff5b936fd8c.png)  

The second part of the if statement is executed and showed in the next second screenshot.  
If `word` is not null, then `+=` whatever your second, third, (...), n input is.  
Lastly, I use `+ System.lineSeparator()`, after the parameter string index, that's holding the input you want to add, to perform a `String.format("%s \n")` function. 

> I know strings are immutable, so what's happening is that the String variable `word` changes its pointer to a new String that contains the sum of what was currently stored with whatever your input is.  
> Therefore, we're seeing a new String every time you add a message.  
> The `System.lineSeparator()` helps with line breaks to make your input look like it's a new and individual one (but in reality is just a big string with all those inputs).

Typing http://localhost:1313/ `add-message?s=how r you??` returns:  

![image](https://user-images.githubusercontent.com/122419405/215237960-dc46be95-542e-417c-89df-e3d817b46e01.png)  


### Here, I tried to input non-string values such as URIs and ints.
Typing http://localhost:1313/ `add-message?s=13` returns:  

![image](https://user-images.githubusercontent.com/122419405/215237987-0861b494-0c0b-4a8e-8289-2e9153755ad1.png)  


Typing http://localhost:1313/ `add-message?s=[URL]` returns:  

![image](https://user-images.githubusercontent.com/122419405/215238004-9f0d1346-b8a2-4fde-ae18-22956749fd0e.png)


Turns out, they were just turned into strings and added perfectly!  
> This is because `System.lineSeparator()` is the same as `"\n"`, and when you add [any variable] + [a string] you get a string back.

## Part 2

### I will use the `append` bug from `LinkedListExamples.java`
![image](https://user-images.githubusercontent.com/122419405/215297559-fa3b2a23-e146-49bb-87b2-02158ad91d51.png)

```
  while(n.next != null) {
    n = n.next;
    n.next = new Node(value, null);
  }
```

If you look carefully at the while loop, it will never end because it will keep creating new objects that return a true condition all the time.   

Thus, a failure-inducing input would be using append once, twice... until we get the one that triggers the infinite loop.  
> (Note that we're lucky here because it breaks after appending three times, but if there were to be a million appends to do, then a for loop should do this).

``` 
@Test (Never ended)
    public void testAppend() {
        LinkedList app = new LinkedList();
        app.append(13);
        app.append(133); // maximum
        app.append(46); // append three times = infinite loop
        app.append(37);
        app.append(777);
    }
```

According to the code, appending **once** doesn't induce a failure because if LinkedList is null, then it just makes your input be its first value.  
Adding **two times** doesn't induce a failure either because there's code built for that specific case of having one element already when append gets called. 

```
 @Test (Passed)
    public void testAppendShouldPass() {
        LinkedList app = new LinkedList();
        app.append(13);
        app.append(133); // maximum
    }
```

So, after running these tests we find the symptom:

![image](https://user-images.githubusercontent.com/122419405/215297901-77a1832e-83a2-4020-bc57-2f441c9c97dd.png)

The bug is located at the end of the while loop ??? meaning, at `n.next = new Node(value, null);`
Because the while loop will keep expanding the list, the loop will keep running true.  
This while loop is programmed to keep looking for the end, and if you keep expanding the end as you go, you'll never reach it. It must stop. 

Solution: Moving the loop's last statement to the outside, so you can first find the end and then expand the list (append) from that end (at `n.next`).

```
  while(n.next != null) {
    n = n.next;
  }
  n.next = new Node(value, null);
```
![image](https://user-images.githubusercontent.com/122419405/215238434-28d487c4-527b-4669-b7bc-59f3fb89fa49.png)

# Part 3
I learned so much from lab 2 and 3. I'll do a bulleted list!
* I learned how to `ssh` to a server.
* I learned how to `scp` ??? how to copy files from my computer to the server and vicevesa (this is what hackers do!)
* I learned how to deploy a webserver!
* I learned what all those letters in the search bar mean.
* I learned how to change a website through the search bar (as if the search bar was a little terminal!)
* I learned about URI and how to use some of its methods like `getPath()` and `getQuery()`
* Last but not least, I learned how to use Github in general, with VS Code, in my desktop, and in the server.  
> (I've never used github before, I think I got this!)
