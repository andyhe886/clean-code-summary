# clean-code-summary
Clean code: a Handbook of Agile Software Craftmanship by Robert C. Martin Series

## Meaningful names

### Use Intentional-Revealing Names
The name of a variable, function, or class. It should tell why it exists, what it does, how it is used. Usually it doesn't need to have comment.

**Example**
```
    public List<int[]> getThem() {
        List<int[]> list1 = new ArrayList<int[]>();
        for (int[] x : theList)
            if (x[] x : theList)
                list1.add(x);
        return list1;
    }
```

Question to ask:

    1.What kinds of things are in theList?
    2.What is the significance of the zeroth subscript of an item in theList?
    3.What is the significance of the value 4?
    4.How would I use the list being returned?
    
It can become more easier to read
```
    public List<int[]> getFlaggedCells() {
        List<int[]> flaggedCells = new ArrayList<int[]>();
        for (int[] cell : gameboard)
            if(cell[STATUS_VALUE] == FLAGGED)
                flaggedCells.add(cell);
        return flaggedCells;
    }
```

## Avoid disinformation
Example: do not refer to a grouping of accounts as an accountList unless it's actually a list.

## Make Meaningful distinctions
Example: Number-series naming (a1, a2, ... aN) is the opposite of intentional naming and Noise words are another meaningless distinction.

## Use searchable names
Example: Grep MAX_CLASSES_PER_STUDENT

## Class names
Classes and objects should have noun or noun phrase like Customer, WikiPage, Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name of a class.

## Method Names
Methods should have verb or verb phrase names like postPayment, deletePage, or save. 

## Unit Tests

### The Three Laws of TDD
    1.First law: You may not write production code until you have written a failing unit test.
    2.Second law: You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
    3.Third law: You may not write more production code than is sufficient to pass the currently failing test.
    
### Keeping Tests Clean
Dirty tests is equivalent to having no tests at all, By having **Quick and dirty** tests means that the variables is not well named, the functions is not short and descriptive and the test code is not need to be well designed and thoughtfully partitioned.
Also, without a test suite, they cannot know if by changing a part of the application will break other parts of the application. Therefore, the defect rate began to rise which leads to fear making some changes. Even in production code.

Unit tests are here to keep your code **flexible**, **maintainable** and **reusable**.
### Clean tests (Readability)

There's a pattern call **Arrange, Act, Assert** to make the test code more readable. 

    1.Arrange: Builds up the test data.
    2.Act: Operates on that test data.
    3.Assert: Checks that operation yielded expected results.

Read **BUILD-OPERATE-CHECK** [FitNesse.AcceptanceTestPatterns](http://fitnesse.org/FitNesse.FullReferenceGuide.UserGuide.WritingAcceptanceTests.AcceptanceTestPatterns.BuildOperateCheck)

### F.I.R.S.T
    -Fast: Tests should be fast, run very quick. If it's slow, then you won't run them frequently then you won't be able to find problems early enough to fix them.
    -Independant: Test should never be dependant to each other. If one test failed then it will be like a waterfall to the rest of the tests.
    -Repeatable: Tests should be repeatable in any environnement. It can run in any environnement.
    -Self-validating: The tests should have a boolean output, Pass or failed.
    -Timely: Unit tests should be writtent just beforethe production code, If you write tests after the production code, then it's harder to test. Therefore, you may not design the production code to be testable.
    
