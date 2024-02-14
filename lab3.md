# Lab 3 Report

## Part 1: Bugs

### Failure-Inducing Input
``` 
@Test 
public void testReverseInPlace1() {
  int[] input2 = {1, 2, 3, 4};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{4, 3, 2, 1}, input2);
}
```

### Input That Doesn't Induce a Failure
```
@Test 
public void testReverseInPlace2() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```

### Symptoms (Test Output)

![Image](lab3-img/junit-tests.png)

As we can see, only `testReverseinPlace1` failed, because the method returned `{4, 3, 3, 4}` rather than `{4, 3, 2, 1}`.

### The Bug (Before-and-After Code)
Before:
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```

After:
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length/2; i += 1) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i - 1]; 
    arr[arr.length - i - 1] = temp;
  }
}
```

The main bug with the original code is that it iterates through the entire array and sets the current element equal to the element on the opposing 
side. For an array of size 1 (as in `testReverseInPlace2`), this causes no issues because that singular element is just assigned to itself. 
But for arrays with sizes greater than 1, elements past `arr.length / 2` are assigned the values of the opposing, earlier elements which have already been
changed, or "reversed." The fix addresses this by iterating through only half of the array (`array.length / 2`) and creating a `temp` value containing the 
current element's value. This way, after changing the value of the current element, we can then assign its old value, `temp`, to the element on 
the opposing side of the array. Thus, we end up with a properly-reversed array.


## Part 2: Researching the `find` Command

### Option 1: `-type`
Source: learned through these 2 linked articles: [article1](https://www.redhat.com/sysadmin/linux-find-command) , [article2](https://alvinalexander.com/unix/edu/examples/find.shtml)

Example 1:
```
Niroops-MacBook-Pro:docsearch nkris$ find technical -type d
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
technical/plos
technical/biomed
technical/911report
```

The `-type` option lets us filter our search results by type. In this example, we look within the `./technical` directory but use the `-type d` option to specify that we want only list of the directories within the provided path. This can be useful when we don't want to see every single file in a directory (knowing it could be hundreds or thousands) but simply want an idea of how big a directory is by looking at its subdirectories.

---

Example 2:
```
Niroops-MacBook-Pro:docsearch nkris$ find technical/911report -type f
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-2.txt
technical/911report/chapter-1.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-8.txt
technical/911report/preface.txt
technical/911report/chapter-12.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
```

Here, by using `-type f`, we're saying we want the `find` command to return ONLY files within the `./technical/911report` directory. There is usefulness to this option considering that, by default, the `find` command returns all files, directories, and other file types which might not be as well known (like pipes, device files, etc) in a specified path. 

---

### Option 2: `-iname`
Source: used the `man find` command  

Example 1:
```
Niroops-MacBook-Pro:docsearch nkris$ find . -iname "*Chapter*txt"
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```

The `-iname` option does a case-insensitive search for us when we can't remember the exact file name (which is very useful when there are a ton of file names, like in this `docsearch` project!). Here, we're looking for every `.txt` file within our home directory (and sub-directories) with the word "Chapter" in its name. As you can see by the output, uppercase/lowercase is not important (every `.txt` file containing "chapter" was listed).

---

Example 2:
```
Niroops-MacBook-Pro:docsearch nkris$ find technical/government -iname "*state*.txt"
technical/government/About_LSC/State_Planning_Report.txt
technical/government/About_LSC/State_Planning_Special_Report.txt
technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
technical/government/Media/State_funding.txt
technical/government/Media/The_State_of_Pro_Bono.txt
```

Here, we search for `txt` files containing `state` somewhere in their name within the `./technical/government` directory specifically. So his option can  be quite useful when we know what directory to look in and want to search for a file based on our best recollection of what its name is!

---

### Option 3: `-not <<expression>>`
Source: used the `man find` command 

Example 1:
```
```

In this example, we are looking for every file in our home directory that is NOT 

---

Example 2:
```
```

---

### Option 4: `-exec`
Source: learned through this linked [article](https://www.redhat.com/sysadmin/linux-find-command) 

Example 1:
```
```

Example 2:
```
```

