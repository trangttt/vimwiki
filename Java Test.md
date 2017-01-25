## JUnit
### Fixtures
```java
public class JavaTest extends TestCase {
    protected void setUp(){

    }
    protected void tearDown(){

    }
}
```
### Test Suites
```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.SuiteClass({
    TestJunit1.class, TestJunit2.class
})

public class JunitTestSuite {

}
```


### Ignore Test/ Test Selection
### Parameterized Test
### Timing Test
### Dependency Test
### Exception Test

## JUnit vs TestNG
1. Annotation/Fixtures
- `@BeforeClass`, `@AfterClass`
- `@Before`, `@After`
- `@Test`
2. Ignore test
- `@ignore`
3. Exception Test
- `@Test(expected = ArithmeticException.class)`
4. Timing
- `@Test(timeout = 100)`
6. Test Suite
```java
@RunWith(Suite.class)
@Suite.SuiteClasses({
    JUnitTest1.class,
    JUnitTest2.class
})
class SuiteTest {

}
```
7. Parameterized Test
```java
@RunWith(Parameterized.class)
class TestClass {
    @Parameters
    public static Collection(Object[]) method(){
        Object[][] data = new Object[][]{ { 1, 2 },
                                          { 3, 4 }
                                        };
    }
}
```
9. Dependency Test/Integration Test

