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

### Avoid disinformation
Example: do not refer to a grouping of accounts as an accountList unless it's actually a list.

### Make Meaningful distinctions
Example: Number-series naming (a1, a2, ... aN) is the opposite of intentional naming and Noise words are another meaningless distinction.

### Use searchable names
Example: Grep MAX_CLASSES_PER_STUDENT

### Class names
Classes and objects should have noun or noun phrase like Customer, WikiPage, Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name of a class.

### Method Names
Methods should have verb or verb phrase names like postPayment, deletePage, or save. 

## Functions

### Do One Thing
_FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY._

### Reading Code from Top to Bottom: _The Stepdown Rule_

Read code like top-down narrative, every function should be followed by those at the next level of abstraction. TO paragraph that describe the current level of abstraction.

Example: 

    To do something, we include setup and teardown, we include setups, then we include test content, and then we include teardown.
        To include the setups, we include the suite setup
        To include Test content
        To include teardown
        
### Switch Statements
By nature, _switch_ statements always do _N_ things. Often _polymorphism_, we can make sure that each _switch_ statement is buried in a low-level class and is never repeated.

```
    public Money calculatePay(Employee e) throws InvalidEmployeeType {
        switch (e.type) {
            case: COMMISIONNED:
                return calculateCommissionPay(e);
            case: HOURLY:
                return calculateHourlyPay(e);
            case: SALARIED:
                return calculateSalariedPay(e);
            default:
                throw new InvalidEmployeeType(e.type);
        }
    }
```

    1.It's large, and when new employee types are added, it will grow
    2.It does more than one thing
    3.Violates the Single Responsibility Principle (SRP)
    4.Violates the Open Closed Principle
    5.Unlimited number of other functions that will have the same structure

To fix this mess: the general rule
```
    public abstract class Employee {
        public abstract boolean isPayday();
        public abstract Money calculatePay();
        public abstract void deliverPay(Money pay);
    }
    
    public interface EmployeeFactory {
        public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
    }
    
    public class EmployeeFactoryImpl implements EmployeeFactory {
        public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
            switch(r.type) {
                case COMMISSIONED:
                    return new CommnissionedEmployee(r);
                case HOURLY: 
                    return new HourlyEmployee(r);
                case SALARIED: 
                    return new SalariedEmployee(r);
                default:
                    throw new InvalidEmployeeType(r.type);
            }
        }
    }
```

### Use Descriptive Names
A long descriptive name is better than a short enigmatic name or comment. Be consistent in your names. Use the same phrases, nouns, and verbs in the names you choose for your modules.

### Function Arguments
The ideal number of arguments for a function is zero(niladic), one(monadic), two(dyadic), three(triadic) should be avoided where possible. More than three(polyadic) requires very special justification.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all various combinations of arguments work properly.

### Flag arguments

Flag argument are ugly. Passing a boolean into a function is a truly terrible practice.

### Have No Side Effects

```
    public boolean checkPassword(String userName, String password) {
        ...
        if ("Valid Password".equals(phrase)) {
            Session.initialize();
            return true;
        }
    }
```

The side effect is called sessions.initialize(). Function should rename to checkPasswordAndInitializeSession.

## Comments
Code changes and evolves, Chunk of it move from here to there. Those chunks bifurcate and reproduce and come together again to form chimeras. Unfortunately the comments don't always follow them.
 
### Comments Do Not Make Up for Bad Code
Writing comments is for bad code, Clear and expressive code with few comments is way better than cluttered and complex code with lots of comments.

### Informative Comments
```
    // format matched kk:mm:ss EEE, MMM dd, yyyy
    PAttern timeMatcher = Pattern.compile(
    "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

In this case the comment lets us know that the regular expression is intended to match a time and a date that were formatted with SimpleDateFormat.format function using the specified format string.

### TODOs Comments

```
    //TODO-MdM these are not needed
    // We expect this to go away when we do the checkout model
    protected VersionInfo makeVersion() throws exception {
        return null;
    }
```

TODOs are jobs that the programmer thinks should be done, but for some reason can't do at the moment. It might be a reminder to delete a deprecated feature or a plea for someone else to look at the problem.
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
    
