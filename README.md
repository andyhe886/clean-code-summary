# clean-code-summary
Clean code: a Handbook of Agile Software Craftmanship by Robert C. Martin Series

##Unit Tests

###The Three Laws of TDD
    1.First law: You may not write production code until you have written a failing unit test.
    2.Second law: You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
    3.Third law: You may not write more production code than is sufficient to pass the currently failing test.
    
###Keeping Tests Clean
Dirty tests is equivalent to having no tests at all, By having **Quick and dirty** tests means that the variables is not well named, the functions is not short and descriptive and the test code is not need to be well designed and thoughtfully partitioned.
Also, without a test suite, they cannot know if by changing a part of the application will break other parts of the application. Therefore, the defect rate began to rise which leads to fear making some changes. Even in production code.

Unit tests are here to keep your code **flexible**, **maintainable** and **reusable**.
###Clean tests (Readability)

There's a pattern call **Arrange, Act, Assert** to make the test code more readable. 

    1.Arrange: Builds up the test data.
    2.Act: Operates on that test data.
    3.Assert: Checks that operation yielded expected results.

Read **BUILD-OPERATE-CHECK** [FitNesse.AcceptanceTestPatterns](http://fitnesse.org/FitNesse.FullReferenceGuide.UserGuide.WritingAcceptanceTests.AcceptanceTestPatterns.BuildOperateCheck)

###F.I.R.S.T
    -Fast: Tests should be fast, run very quick. If it's slow, then you won't run them frequently then you won't be able to find problems early enough to fix them.
    -Independant: Test should never be dependant to each other. If one test failed then it will be like a waterfall to the rest of the tests.
    -Repeatable: Tests should be repeatable in any environnement. It can run in any environnement.
    -Self-validating: The tests should have a boolean output, Pass or failed.
    -Timely: Unit tests should be writtent just beforethe production code, If you write tests after the production code, then it's harder to test. Therefore, you may not design the production code to be testable.
    
