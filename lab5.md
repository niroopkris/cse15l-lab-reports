# Lab 5 Report

## Part 1: Debugging Scenario

### Student Post:
Hello,

I'm getting a weird null pointer error from my `testFilter` method in which I'm told it cannot invoke some `List iterator()` because `<parameter1>` is null. The issue might be related to the arguments I pass in during line 34, but I double checked and I'm pretty sure I initialized all my variables properly in my `setup()` method.

![Image](lab5-img/error.png)

### TA Response:

Can you double check your code for your `setup()` method one more time and make sure the variable names match with the names you pass into `filter()` as an argument? Make sure there are no syntax errors or value resets. If you still have issues send a screenshot of your code for `testFilter()` and `setup()`.

### Screenshot After Trying Fixes + Bug Description
![Image](lab5-img/second-try.png)

Turns out the error was indeed with my `setup()` method, but it wasn't due to naming mistakes. I had declared all the variables and their types outside the method (like so: `List<String> expected1;`), but I accidently declared all their types yet again when initializing them in `setup()` (I was doing this: `List<String> input1 = Arrays.asList("a", "ab", "moon", "bcd");` when it should have simply been `input1 = Arrays.asList("a", "ab", "moon", "bcd");`). After removing the double declaration, my variables were initialized properly and my code worked again.
`

## Setup Info:

### File Structure

```
report5/
|-  lib
     |-  hamcrest-core-1.3.jar
     |-  junit-4.13.2.jar
|-  grade.sh
|-  ListExamples.java
|-  TestListExamples.java
(NOTE: FILES AFTER THIS POINT ARE CLASS FILES GENERATED AFTER RUNNING)
|-  IsMoon.class
|-  ListExamples.class
|-  StringChecker.class
|-  TestListExamples.class
```

## Contents of Files
Note: Will ignore lib and the class files since they were not touched.

TestListExamples.java
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {

  List<String> input1;
  List<String> expected1;
  
  @Before
  public void setup() {

    List<String> input1 = Arrays.asList("a", "ab", "moon", "bcd");
    List<String> expected1 = Arrays.asList("moon");

  }

  @Test 
	public void testFilter() {
    setup();

    IsMoon contains = new IsMoon();

    List<String> output1 = ListExamples.filter(input1, contains);


    List<String> input2 = Arrays.asList("a", "b", "c");
    List<String> expected2 = Arrays.asList();

    List<String> output2 = ListExamples.filter(input2, contains);

    
    assertEquals(expected1, output1);
    assertEquals(expected2, output2);
  }

  public void testFilterEmpty() {
    List<String> input = Arrays.asList();

    List<String> expected = Arrays.asList();

    IsMoon contains = new IsMoon();


    List<String> output = ListExamples.filter(input, contains);


    assertEquals(expected, output);
  }

  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");

    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");

    List<String> merged = ListExamples.merge(right, left);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);  
  }

  @Test(timeout = 500)
  public void testMergeEmpty() {
    List<String> left = Arrays.asList();
    List<String> right = Arrays.asList();
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList();
    assertEquals(expected, merged);
  }
}
```

ListExamples.java
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }
}
```

grade.sh
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

set +e
javac -cp $CPATH *.java 
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 
```

### Command Triggering Bug

### Description of Edit to Fix


## Part 2: Reflection





