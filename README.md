# PA 1 - Spam Checker

## Due
All files are due by 11:59pm on Wednesday 8/17/2022 

See "Grading” and “Submission” sections for more details.


## Overview
In this assignment, you will write an interactive program meant to check if an email is in a list of spam addresses or not. This program will read in email data files and populate a hash table with these email addresses, then allow for user interaction with the data. The user will enter email addresses to check if they are spam by looking into the hash table.

The educational purpose of this programming assignment is to introduce you to the C programming language, hashtables with closed addressing, file I/O, and command line arguments.


## Tutorials and readings

Here are a few helpful links in case you need to read up to get familiar with the languages and tools.

- Unix Tutorial http://www.ee.surrey.ac.uk/Teaching/Unix/
- Vim Tutorial https://www.openvim.com/
- Git Basics Chapter http://git-scm.com/book/en/Git-Basics
- Learn C https://www.learn-c.org/
- C for Java Programmers http://www.cs.columbia.edu/~hgs/teaching/ap/slides/CforJavaProgrammers.ppt
- Debugging with GDB http://www.delorie.com/gnu/docs/gdb/gdb_toc.html
- GDB Tutorial video https://youtu.be/bWH-nL7v5F4

## Style Guidelines
We will follow these style guidelines for every assignment in this class. Please familiarize yourself with them. We will not be grading points for style. Nonetheless, it's advantageous to follow proper style in order to keep your code organized and make it easier for staff to help.

http://cseweb.ucsd.edu/~ricko/CSE30StyleGuidelines.pdf

## Getting started
Follow these steps to acquire the starter files and prepare your Git repository.

### Gathering Starter Files
The first step is to gather all the appropriate files for this assignment. First connect to ieng6 via ssh, then, on ieng6, connect to the pi-cluster via ssh. Make sure to use your own account name (cs30s222__ followed by two letters).

```
$ ssh cs30s222yx@ieng6.ucsd.edu
$ ssh cs30s222yx@pi-cluster.ucsd.edu
```
Create and enter the pa1 working directory.
```
$ mkdir ~/pa1
$ cd ~/pa1
```
Copy the starter files from the public directory.
```
$ cp -r ~/../public/pa1StarterFiles/* ~/pa1/
```

### Files provided
Files provided:
```
launchUserQuery.c
util.c
pa1.h
pa1Strings.h
test.h
testhash.c
Makefile
```
Spam emails provided:
```
~/../public/emails/emails_<num>
~/../public/emails/emails_all
```
- `num` is the number of spam email addresses in the file
- You can assume no duplicates in the email list

### Preparing Git Repository
You are required to use Git with this and ALL future programming assignments. You may not appreciate Git now, but at least once a quarter a student will accidentally delete all of their files on the day the assignment is due. Git can help save you from this terrible fate! In your future jobs and projects knowledge of Git and Github will be assumed. Not only that, but also you will have to option to use Git combined with GitHub to submit your assignment on Gradescope, so get to know Git and GitHub! Check out the Tutorials and Readings section above for more info on Git.

**You must make your Github repository private.**

#### 1. Setting up a local repository

Navigate to your pa1 directory and initialize a local git repository:

```bash
cs30s220yx@pi-cluster-001:~/pa1$ git init
```

If you haven't already set your global git user info, go ahead and do that now:

```bash
cs30s220yx@pi-cluster-001:~/pa1$ git config --global user.name "John Doe"
cs30s220yx@pi-cluster-001:~/pa1$ git config --global user.email "johndoe@ucsd.edu"
```

#### 2. Adding and committing files

Now add the starter files to your local git repository:
```bash
cs30s220yx@pi-cluster-001:~/pa1$ git add .
cs30s220yx@pi-cluster-001:~/pa1$ git commit -m "Some message"
```

As you're developing, you can see the status of the files in your directory with the following command:

```bash
cs30s220yx@pi-cluster-001:~/pa1$ git status
```

After you edit a file with meaningful changes, you should add and commit it to the repository:

```bash
cs30s220yx@pi-cluster-001:~/pa1$ git add filename
cs30s220yx@pi-cluster-001:~/pa1$ git commit -m "Some message describing the changes"
```

You can commit multiple files at the same time by calling `git add` on several files before calling commit:

```bash
cs30s220yx@pi-cluster-001:~/pa1$ git add file1
cs30s220yx@pi-cluster-001:~/pa1$ git add file2
cs30s220yx@pi-cluster-001:~/pa1$ git add file3
cs30s220yx@pi-cluster-001:~/pa1$ git commit -m "Changed things in three files"
```

You must do a `git add` on each file you wish to commit before every `git commit`! It is not enough to do a `git add` once at the beginning. `git commit` will only collect files that have been added (`git add`) since the last commit.

There are other ways to do this, including some that make it substantially quicker for simple projects like those in this class, so it is worth looking at a few Git tutorials and/or references. From this point forward it is up to you when to add and commit to take your Git snapshots. There are other things that can be done with Git (quite a lot of things) and those are also up to your discretion.

#### Ignoring file with `.gitignore`

You may notice as you're developing your program that Git really wants to keep track of `.o` files, `.swp` files, executables, etc. which you don't really need to track. You can get it to stop bugging you about them by creating a `.gitignore` file. Simply open `.gitignore` in vim/gvim:

```
cs30s220yx@pi-cluster-001:~/pa1$ vim .gitignore
```

And add the following lines to it:

```gitignore
*.o
*.sw*
*~
a.out
core
```

Now when you use `git status`, those pesky files won't show up in the list of untracked files.  You also might want to commit the `.gitignore` file into the repository.

## Sample output
A sample stripped executable provided for you to try and compare your output against is available in the public directory, run them using the following commands (where you will also pass in the command line arguments):
```
cs30s220yx@pi-cluster-001$ ~/../public/pa1testspamFilter
```

#### Warning
1. The output of your program MUST match exactly as it appears in the `pa1testspamFilter` output. You need to pay attention to **everything** in the output, from the order of the error messages to the small things like extra newlines at the end (or beginning, or middle, or everywhere)!
2. We are giving you few sample test cases with outputs, but this list is not exhaustive. See the [Grading](#Grading) section for an exhaustive list of test cases we will be testing you on.

### Sample Test Case 1

Prompt the short usage message and `INVALID_ARGS` because the user doesn't input the required arguments.


Usage for spamFilter:
```
cs30s222yx@pi-cluster-001:pa1$ ./spamFilter
Incorrect number of args.

Usage: ./spamFilter {-i dataFile | -h}

cs30s222yx@pi-cluster-001:pa1$
```

### Sample Test Case 2

The program prompts the user for input and correctly outputs based on that input.

```
cs30s222yx@pi-cluster-001:pa1$ ./spamFilter -i ~/../public/emails/emails_10
Enter a word: jazz@hack.co
jazz@hack.co is SPAM!
Enter a word: paul@gmail.com
paul@gmail.com is not SPAM!
Enter a word:
```

### Sample Test Case 3

Prompt the long usage message because the user input the help flag.

```
cs30s222yx@pi-cluster-001:pa1$ ./spamFilter -h

Usage: ./spamFilter {-i dataFile | -h}
    -i dataFile -- The file containing the data
    -h          -- Displays this long usage message

cs30s222yx@pi-cluster-001:pa1$
```

### Tips

**Diffing**

An easy way to check your output against the sample executable is by using diff:
```
cs30s222yx@pi-cluster-001:pa1$ ./spamFilter -i ~/../public/emails/emails_10 < queries > myOutfile
cs30s222yx@pi-cluster-001:pa1$ ~/../public/pa1testspamFilter -i ~/../public/emails/emails_10 < queries > refOutfile
cs30s222yx@pi-cluster-001:pa1$ diff -s myOutfile refOutfile
```
Where `queries` is a file of emails you want to check for potential spammers.

**Testing with different table sizes**

As you test your program, you might find it difficult to debug your code with small data sets on such a large table. To make it easier to debug, you may want to make your table size smaller. You can change your table size by opening the provided `Makefile` and changing the `SIZE` variable at the very top.

```Makefile
# inside the Makefile

# You may change me for debugging purposes.
SIZE = 2003
```

Note that we will only test you with the default size, 2003. Also note that you don't have to worry about changing this variable back before submitting your code. We will use **our** Makefile when compiling your code for grading.

## Detailed overview

The function prototypes for the various C functions are as follows.

### C routines
```c
// The following functions should be written in modules with identical names.

int main(int argc, char* argv[]); // (in the file spamFilter.c)
int checkTable(char* str, linkedListNode_t** hashtbl);
unsigned int hash(char* str);
void populateTable(linkedListNode_t** hashtbl, FILE* dataFile);
void llTableAddString(linkedListNode_t** hashtbl, char* string);
linkedListNode_t *retrieveLinkedList(linkedListNode_t** hashtbl, char* string);
void prependNode(linkedListNode_t** head, char* str);
```
### Process Overview
The following is an explanation of the main tasks of the assignment, and how the individual functions work together to form the whole program.

**spamFilter workflow:**
1. Parse all the command line arguments passed into the program. Do all the required error checking.
2. Instantiate a new hash table with `newLinkedListArray()` (see pa1.h) and populate the hash table with the passed in data file.
3. Begin the interactive user query mode that allows the user to search the table.
4. When the user ends the search with ctrl-d, call the provided `cleanup()` function, close any open files, and exit the program.
![](https://i.imgur.com/xkmb68u.png)

[Link to image](https://i.imgur.com/xkmb68u.png)

### Hash Table

There is one hash table which uses `hash()` as the hash function. This is a separate-chaining hash table. When an item is hashed to index `i`, it should be pushed to the linked list pointed by the pointer at index `i` in `hashtbl`

### Memory Diagram
At any moment of a normal program execution, we have a hashtable of type
`linkedListNode_t**`.

This hashtable stores `DEFAULT_SIZE` number of `linkedListNode_t*`. These `linkedListNode_t` form a linked list by storing one string in `value` and pointing `next` to any next node.

Your task is to use the predefined structs to populate these data structures

![](https://i.imgur.com/nNB0x6S.png)


## Detailed Implementation
Listed below are all the modules to be written. **Please read the entire writeup before writing any code.**

### hash.c
```c
unsigned int hash(char* str);
```
This function will be used to create the hash key of a string. This function creates an integer hash key from str with the following hashing algorithm. Your task is to translate this algorithm into C. The return value can [overflow](https://en.wikipedia.org/wiki/Integer_overflow), that’s fine.

1. Assign `HASH_START_VAL` to an unsigned int `hashVal`.
2. For all characters on **even** indices of the string, perform the following:
    2.1. Compute the product of `hashVal` and `HASH_PRIME`.
    2.2. Set `hashVal` to the sum the character's ascii value and the result from 2.1.
4. Repeat step 2, but this time for all characters on **odd** indices of the string.
5. Return `hashVal`.

You may find the `strlen()` function useful here (see `man -s3 strlen`).

**Example:**

```
hashVal:   11
HASH_PRIME: 37

index: 0    str: paul    ascii value: 112    hashVal: (11 * 37) + 112 = 519
                 ^

index: 2    str: paul    ascii value: 117    hashval: (519 * 37) + 117 = 19320
                   ^

index: 1    str: paul    ascii value: 97     hashval: (19320 * 37) + 97 = 714937
                  ^

index: 3    str: paul    ascii value: 108    hashval: (714937 * 37) + 108 = 26452777
                    ^
```

**Return Value:** The hash key of `str`.


---
### prependNode.c
```c
void prependNode(linkedListNode_t** head, char* str);
```

This function takes in a pointer to the head of a linked list (i.e. a pointer to a pointer to a `linkedListNode_t`) and a string to insert and then pushes the element onto the front of the linked list. Another way can you conceptualize this is by thinking of `head` as pointing to the bucket which contains the linked list and `*head` as pointing to the first node in the linked list. To implement this function, you will need to create a new linked list node. In `util.c` we have provided you some utility functions such as `newLinkedListNode()` which you should use to create new nodes. Take a look at the function prototypes in `pa1.h` to get an idea of how you use these utility functions. You don't have to understand any of the code in `util.c` (yet) and you should **not** change any of the functions in that file.

Perform the following steps:
1. Create a new linked list node
2. Create a copy of the passed in string (see `pa1.h` for the provided `strcp()` function's prototype).
3. Assign the node's value to be the *copy* of `str`.
4. Attach the old list to the new node
5. Attach the new node to be the new head

![](https://i.imgur.com/WSY0R1V.png)
![](https://i.imgur.com/aKQ7cco.png)
[Link to images for steps 0 - 3](https://i.imgur.com/WSY0R1V.png)
[Link to images for steps 4 - 5](https://i.imgur.com/aKQ7cco.png)

---
### llTableAddString.c
```c
void llTableAddString(linkedListNode_t** hashtbl, char* string);
```
Call `hash()` to hash string. Note that the hashkey returned by the hash function will not necessarily be an index within the size of the hash table. In order to guarantee that the indices are within the size of the hashtable, use the modulus (%) operator.

The hash table contains a linked list at each hash bucket, so when an element hashes to that location, the string is pushed to the front of that linked list, and we do so by calling `prependNode()` with the address of the element at `index` in `hashtbl`.

---

### populateTable.c

```c
void populateTable(linkedListNode_t** hashtbl, FILE* dataFile);
```

This function populates the hash table by reading in `dataFile`, grabbing each
line using `fgets()`, and calling the `llTableAddString()` function. When
reading in line by line, use `strchr()` to find the newline character in the
resulting buffer from `fgets()`, and replace it with a null character. Next, in
order to allow our strings to be case-insensitive, use `tolower()` on every
character of each string to fully convert all characters in it to lower-case.
Following this, we will call `llTableAddString()`.  The maximum length of the
email addresses is 30 characters.

**Tip for testing:** One way of writing your unit tests for this function is by
calling `populateTable()` on a file of your choice and checking if each string
you expected to be in the table is, in fact, in the table.

---

### retrieveLinkedList.c
```c
linkedListNode_t *retrieveLinkedList(linkedListNode_t** hashtbl, char* string);
```
Call `hash()` to hash string. Note that the hashkey returned by each of the hash functions will not necessarily be an index within the size of the hash table. In order to guarantee that the indices are within the size of the hashtable, use the modulus (%) operator.

**Return value:** The element of `hashtbl` at `index`.

---

### checkTable.c
```c
int checkTable(char* str, linkedListNode_t** hashtbl);
```
This function reports if the string is seen in the hash table.

Perform the check on the table by calling `retrieveLinkedList()`. If no such linked list exists, return 0. If the linked list does exist, then you must also look inside the linked list. If the input string itself is also found in the linked list, return 1, otherwise return 0.

You may find the `strcmp()` function useful here (see `man -s3 strcmp`).

**Return Value:** 0 if no linked list exists at the value hashed into using `str` or the linked list does exist and `str` is not in the linked list. 1 if the string is in the linked list at the value hashed into using `str`.

---
### spamFilter.c
```c
int main(int argc, char* argv[]);
```

This is the main driver of your program. Its main tasks are to parse the command line arguments, build the hashtable of email data, and perform an interactive search.

__Parsing command line arguments:__

For this assignment, the functionality of the program will be determined by the number of arguments passed in from the command line. That is, if 2 arguments are passed into the program from the command line, you may assume that they are the infile flag and infile name, respectively. And if only 1 flag is passed in, you may assume that it is the help flag.

This is regardless of what letter is used for each flag (e.g. the convention for the help flag is `-h`, but as long as the user only passes in 1 command line argument, the full usage statement will be printed). Although in the table below we will follow this naming convention, your program does not have to.

The following table details how to handle these flags:

| Flag Options | Required Argument | How to Handle |
|-----------|-------------------|------------------------------------------------------------------------------------------------------------------|
| -h         | None | Print out `LONG_USAGE` to stdout and return   indicating success.                                              |
| -i         | infile name | Try to open the file (list of emails) of this name |

**Notes**
- The only valid number of command line arguments that can be passed in is either 1 or 2.
- You may assume that no poorly formatted input files will be passed in as an argument to the infile flag.
- All strings that you need to print out for this function can be found in `pa1Strings.h`.

**Detailed overview**

Now let’s take a closer look at each step of the program.
1. Parse command line arguments and process any errors. More on error processing below.
2. Initialize and populate your hashtable with `DEFAULT_SIZE`(see `pa1.h` for the provided `newLinkedListArray()` function's prototype). Be sure to use the `populateTable()` function you wrote.
3. Perform interactive search by calling `launchUserQuery()` (see `launchUserQuery.c` and do **not** change any of the code in this file).
4. Finally, call the `cleanup()` routine we provide for you, passing in your hash table of type `linkedListNode_t **`. After calling `cleanup()`, **do not** attempt to access any part of your hash table! Don't forget to close any open files (man -s3 fclose).

You are free to add your own helper functions as you wish.

**Note:** You are guarenteed that there will be no trailing / leading white spaces when reading emails or when reading user queries.

__Reasons for error__

In this file, as soon as an error is detected, print the appropriate error message(s), then print the short usage `SHORT_USAGE` (see `pa1Strings.h`) to `stderr` using `fprintf()` (see `man -s3 fprintf`), and return indicating failure. See the above sample test case 1 for reference.

The following are error messages (numbers indicate the order of error checking) you need to print for each case, make sure you don’t forget to print the short usage in each case! **If either error occurs, stop processing, print the respective error message, print the short usage, and return immediately.**

1. Number of command line arguments
    - The number of command line arguments passed into the program is invalid. If this happens, print `INVALID_ARGS` to `stderr` using `fprintf()`.
2. Infile
    - Error encountered when opening the file. If this happens, call `perror()` with the `FILTER_ERR`.

__Memory leaks__

It is best practice to clean up resources you use in the duration of your program before ending it. In PA 1, such resources are dynamic memory and open files. The former is handled for you this time (via `cleanup()`), but you must close your files yourself. Be sure to close all your files and call `cleanup()` every time before exiting!

## Unit Testing

You are provided with only one basic unit test file for testhash. This file only has minimal test cases and is only meant to give you an idea of how to write your own unit test files.

**You must write unit test files for some of the functions (as listed below), as well as add several of your own thorough test cases to all of the unit test files. You need to add as many unit tests as necessary to cover all possible use cases of each function. You will lose points if you don’t do this!**

You are responsible for making sure you thoroughly test your functions. Make sure you think about boundary cases, special cases, general cases, extreme limits, error cases, etc. as appropriate for each function. The Makefile includes the rules for compiling these tests. Keep in mind that your unit tests will not build until all required files for that specific unit test have been written.

These test files will be collected and count as part of the correctness of your program.

**Unit tests you need to complete:**
```
testprependNode.c
testhash.c
testpopulateTable.c
```

**To compile:**
```
$ make testhash
```
**To run:**
```
$ ./testhash
```

(Replace `testhash` with the appropriate file names to compile and run the other unit tests)


#### Vim Questions
1. You realized you made a spelling error when using one of the constants from the pa1.h file. Instead of DEFAULT_SIZE, you’ve been typing DEFAUL_SIZE (without the T). How would you find and replace all occurrences of DEFAUL_SIZE in your file to be DEFAULT_SIZE?

#### Git Questions
2. What Git command(s) would you use to list files with changes since the last commit?
3. What Git command would you use to undo a bad commit that has been already pushed?  
4. What Git command would you use to see the history of all your commits?

#### Academic Integrity Question
5. You finished the PA since you started early, but your friend hasn’t and just started working on it even though it’s due tonight at 11:59 pm. Your friend knows you are done with the PA and has asked you to help them so they can finish in time. What do you do to act with integrity?  

## Extra credit

There are 15 points possible for extra credit on this assignment. The two extra credit sections do not depend on one another, so none, either, or both may be done. Do not begin this extra credit until your non-extra credit assignment is completed and you have tested it thoroughly.

### Multiple Email Search (5 points)

You will need to modify the provided `launchUserQuery()` to accept multiple emails entered at the same time. There will be no changes to how the non-extra credit program operates: you will be making a separate `spamFilterEC` program. To begin, make a copy of the provided `launchUserQuery.c` file. Do not make changes to any other files (also do not worry about the usage message, keep it the same as the normal program).

```
$ cp ~/pa1/launchUserQuery.c ~/pa1/launchUserQueryEC.c
```
To make the extra credit:
```
$ make spamFilterEC
```
There is a public executable for you to test with.
```
$ ~/../public/pa1testspamFilterEC -i ~/../public/emails/emails_all
```

#### launchUserQueryEC.c
```c
void launchUserQuery(linkedListNode_t** hashtbl);
```

First note that you should NOT change the name of the function, only the name of the file is different. You will need to make a few changes to this function in order to properly deal with multiple emails entered at the same time. As an example, this is what the program output should look like with multiple emails entered:

```
Enter a word: hijack@spam.me jello grad@hack.co
hijack@spam.me is SPAM!
jello is not SPAM!
grad@hack.co is SPAM!
Enter a word:
```
Thus, you will need to so some form of looping over the emails entered. Make sure that your new functionality is displaying the same stats as in the normal program.

Be sure to test well with the public executable to ensure your output is correct. For simplicity, you are guaranteed that each email will be separated by a single space.

### Command Line Arguments and Statistics (10 points)

You will need to modify your `spamFilter.c` to do the following:

- This program must be able to parse command line flags. In the main assignment, the functionality of your program was dependent on the *number* of arguments passed in from the command line. In this extra credit, you must be able to determine what flags were passed in (more on that in the table below).
- You will also print out various hash table statistics.


To begin, make a copy of the your `spamFilter.c` file called `spamFilterEC2.c`. Do not make changes to any other files.

```
$ cp ~/pa1/spamFilter.c ~/pa1/spamFilterEC2.c
```
To make the extra credit:
```
$ make spamFilterEC2
```
There is a public executable for you to test with.
```
$ ~/../public/pa1testspamFilterEC2 -i ~/../public/emails/emails_100
```

#### spamFilterEC2.c
```c
int main(int argc, char* argv[]);
```

##### Command Line Arguments

The following flags and **only** the following flags will result in the following behavior:

| Flag | Required Argument | How to Handle                                                                                                    |
|----------------------|------------|-----------|
|  -h | None              | Print out `LONG_USAGE_EC2` to stdout and return   indicating success.                                              |
| -s | None       | Print out hash table statistics (more on that below).  |
| -i | infile name       | Try to open the file of this name                                                                                |

The workflow is now as follows. A new step has been added in bold:

1. Parse command line arguments and process any errors. More on error processing below.
2. Initialize and populate your hashtable (see `pa1.h` for the provided `newLinkedListArray()` function's prototype). Be sure to use the `populateTable()` function you wrote.
3. **If the `-s` flag was passed in from the command line, collect the hash table statistics and print them out (see the Statistics section below).**
4. Perform interactive search by calling `launchUserQuery()` (see `launchUserQuery.c` and do not change any of the code in this file).
5. Finally, call the `cleanup()` routine we provide for you, passing in your hash table of type `linkedListNode_t **`. After calling `cleanup()`, **do not** attempt to access any part of your hash table! Don't forget to close any open files (man -s3 fclose).

**Note that the error checking differs from the main assignment as well!**

In this file, as soon as an error is detected, print the appropriate error message(s), then print the short usage `SHORT_USAGE_EC2` (see `pa1Strings.h`) to `stderr` using `fprintf()`, and return indicating failure. See the below sample output for reference.

The following are error messages (numbers indicate the order of error checking) you need to print for each case, make sure you don’t forget to print the short usage in each case! **If either error occurs, stop processing, print the respective error message, print the short usage, and return immediately.**

1. Infile
    - Error encountered when opening the file. If this happens, call `perror()` with the `FILTER_ERR`.
2. Missing the infile flag
    - Print `ARG_ERR` to `stderr` using `fprintf()`.

You may perform this parsing however you like, but we highly recommend using `getopt()` as it is easy to use and is in widespread use. To encourage you to do so, we have provided you the optstring `FLAGS` to use as well as several other constants you may find useful.

**Notes:**
- You may assume that `-i` is always followed by a file name (although this file might not exist).
- You may assume that if `-i` is present, it will be the first flag.
- You may assume that the only flags passed in will be `-i`, `-h`, and / or `-s`.

**Sample Output**

Prompt the short usage message and `ARG_ERR` because the user doesn't input the required arguments.

```
cs30s220yx@pi-cluster-001:pa1$ ./spamFilterEC2 -s
Missing file args

Usage: ./spamFilterEC2 -i dataFile [-h] [-s]

cs30s220yx@pi-cluster-001:pa1$
```

##### Statistics

When the `-s` flag is passed in through the command line, you should gather the following statistics:

We define a hash chain to be a linked list with at least 1 element.

| Statistic | Type |
|-----------|------|
| Number of empty hash table entries. | int |
| Length of the longest hash chain, or 0 if the table is empty. | int |
| Length of the shortest hash chain, or 0 if the table is empty. | int |
| Average length of the hash chain, or 0 if the table is empty. This is `N / M` where `N` is the number of elements in the table and `M` is the number of non-empty entries. | int |

Once you have these statistics, use them to print the provided `STATISTICS` string and proceed with the rest of the program.

**Sample Output**

```
cs30s220yx@pi-cluster-001:pa1$ ./spamFilterEC2 -i ../emails/emails_1000 -s

Hash Table Statistics:

Number of empty entries: 1219
Longest chain length: 5
Shortest chain length: 1
Average chain length: 1

Enter a word:
```

Note: Please test this portion against the provided example solution as formatting matters.

## Grading

#### Correctness: 135 points
The following is an exhaustive list of test cases that you will be graded on. When the submission box on Gradescope is open, upon submission, you will be able to see which cases you got wrong and which you got right. Please do not make it a habit to test your code on Gradescope, as we currently have no plans on giving your score at submission time in future PAs. Also, in the industry, you will have to be the one to test your own code, so it's best to get practice now!

We've split correctness testing into three parts. First, we allocate 0.5 points for each of your testers that compile. The other two parts are as follows:


**Unit Tests**

These will test each individual function. Note that for every function that is dependent on the correctness of another function, we will use our solution code as the dependencies to compile with. For example, `retrieveLinkedList()` is dependent on the correctness of `hash()`. Therefore we will compile your code with a correct implementation of `hash()`.

| Test Name | Description | Points |
|-----------|-----------------------------|----|
| hash_empty_string | Call `hash()` with an empty string. | 2.0 |
| hash_single_char  | Call `hash()` with a string with only one character. | 2.0 |
| hash_numeric | Call `hash()` with a numeric string. | 2.0 |
| hash_alphanumeric | Call `hash()` with an alphanumeric string. | 2.0 |
| hash_all_visible_ascii | Call `hash()` with a string containing all visible ascii characters. | 2.0 |
| populateTable_no_emails | Call `populateTable()` with an empty file. | 5.75 |
| populateTable_few_emails | Call `populateTable()` with a file containing few emails. | 5.75 |
| populateTable_many_emails | Call `populateTable()` with a file containing many emails. | 5.75 |
| checkTable_no_collision | Call `checkTable()` with a string that hashes into a bucket that does not contain a linked list. | 5.75 |
| checkTable_collision_str_dne | Call `checkTable()` with a string does not exist in the table but hashes into a bucket containing a linked list. | 5.75 |
| checkTable_str_ll_start | Call `checkTable()` with a string that exists in the table and is the first node of a linked list. | 5.75 |
| checkTable_str_ll_middle | Call `checkTable()` with a string that exists in the table and is in the middle of a linked list. | 5.75 |
| checkTable_str_ll_end | Call `checkTable()` with a string that exists in the table and is the last node of a linked list. | 5.75 |
| prependNode_one_empty_ll | Call `prependNode()` once on an empty linked list. | 5.75 |
| prependNode_one_short_ll | Call `prependNode()` once on a linked list containing one element. | 5.75 |
| prependNode_one_long_ll | Call `prependNode()` once on a linked list containing multiple elements. | 5.75 |
| prependNode_mult_empty_ll | Call `prependNode()` multiple times on an empty linked list. | 5.75 |
| prependNode_mult_long_ll | Call `prependNode()` multiple times on a linked list containing multiple elements. | 5.75 |
| retrieveLinkedList_no_collision | Call `retrieveLinkedList()` with a string that hashes into a bucket which does not contain a linked list. | 5.3 |
| retrieveLinkedList_collision | Call `retrieveLinkedList()` with a string that hashes into a bucket which contains a linked list. | 5.3 |
| llTableAddString_no_collision | Call `llTableAddString()` with a string that hashes into a bucket which does not contain a linked list. | 5.3 |
| llTableAddString_collision | Call `llTableAddString()` with a string that hashes into a bucket which contains a linked list. | 5.3 |

**Integrated Tests**

These will test your main function. Unlike the unit tests, the compilation and correctness of **all** of your functions matter here. That is, we will **not** compile your code with our solution code.

| Test Name | Description | Points |
|-----------|-----------------------------|----|
| no_emails_few_searches | Read in an empty file and query for a few strings. | 2.45 |
| 10_emails_few_searches | Read in `emails_10` and query for a few strings. | 2.45 |
| 100_emails_few_searches | Read in `emails_100` and query for a few strings. | 2.45 |
| 10000_emails_few_searches | Read in `emails_10000` and query for a few strings. | 2.45 |
| 10_emails_all_search_outcomes | Read in `emails_10` and query the program for all possible outputs. | 2.45 |
| 1000_emails_many_searches | Read in `emails_1000` and query for many strings. | 2.45 |
| all_emails_many_searches | Read in `emails_all` and query for many strings. | 2.45 |
| error_file_dne | Attempt to read in a file that doesn't exist. | 2.6 |
| error_help | Prompt the long usage statement | 2.6 |
| error_extra_arg | Attempt to pass in more than 2 command line arguments | 2.6 |
| error_checking_no_arg | Attempt to pass in no command line arguments | 2.6 |


#### Unit Tests: 15 points
- Various unit test files manually graded on test case completeness and quality.

#### Extra Credit: 15 points
- View the Extra Credit section for more information.
- Tests for these are hidden until we release grades.

#### Style: Not Graded
- See style requirements [here](http://cseweb.ucsd.edu/~ricko/CSE30StyleGuidelines.pdf).
- You are required to style **all** files you submit. See [Submission](#Submission) for more details.
- Note that testers are excluded from the magic number rule.
- Tabs are 8 characters that will count towards the 80-character limit. If you are using tabs, please set your size accordingly so that you will not get points marked off for lines being too long.

#### Compile!
- If what you turn in does not compile with the given Makefile, you will receive 0 points for functionality. Do not modify the given Makefile except when specified.


## Submission

**Super important warning:** If your code does not compile or crashes immediately when run, we will not be able to grade it or reward you functionality points.

Log in to gradescope.com using your @ucsd.edu email address, select the CSE 30 course, assignment PA 1, and upload the following files.  Your file names must match the below *exactly* otherwise our Makefile will not find your files.

We will grade using our `Makefile`, `pa1Strings.h`, `test.h`, `util.c`, `launchUserQuery.c`, and all other files from you. When submitting, please check that Gradescope shows “compile success” to confirm you code works with the given Makefile.

```
pa1.h
hash.c
prependNode.c
populateTable.c
llTableAddString.c
retrieveLinkedList.c
checkTable.c
spamFilter.c
testhash.c
testpopulateTable.c
testprependNode.c
```
For extra credit, also submit `launchUserQueryEC.c` and/or `spamFilterEC2.c`.

If there is anything in these procedures which needs clarifying, or any mistake in this write-up (it's long, we probably made some), please feel free to ask any tutor, the instructor, or post on EdStem.
