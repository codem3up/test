# Unit Test Guide

The NUnit framework is used for testing all .NET languages. You can visit [NUnit](https://github.com/nunit) on git and for more reference when using NUnit visit there documentation page [here]()

### NUnit Attributes

NUnit offers many different kinds of attributes for marking test methods and classes. The ones that we'll most likely be focusing on are the `[TestFixture]`, `[Test]`, and `[TestCase(...)]`

`[TestFixture]` declares a class as a test fixture. All the methods in this class will be invoked if they have the `[Test]` or `[TestCase(...)]` attributes.


### Best Practices
According to Microsoft, a unit test should be split up in to three main categories. These are arrange, act, and assert. Most unit tests should be short and easy to read and understand. Comments are usually not needed because the test itself should be descriptive through its code.

1. Arrange – This is where you declare any of the variables that will be needed throughout the testing of each method. Everything but the method we’re testing should be set in this category.

2. Act – This is where the logic happens. All of the pieces that are required to run the method(s) have already been created, so it’s time to run the method in question. This will generally contain 1-2 lines of code.

3. Assert – This is the test itself. We will assert that the result of the method is supposed to either be equal to, or not equal to, the expected result defined by the user. This will generally only contain one or two lines of code.

``` C#
[TestFixture]
public class MathHelperTest
 {
      [TestCase(10, 20, 30)]
      [TestCase(-5, 15, 10)]
      public void AddNumbersTest(int a, int b, int expected)
      {
           //Arrange
           MathHelper helper = new MathHelper();

           //Act
           int result = helper.Add(a, b);

           //Assert
           Assert.That(result, Is.EqualTo(expected));
       }

       // Not ideal for this kind of test, multiple assertions
       [Test]
       public void AddNumbersTest()
       {
                
           MathHelper helper = new MathHelper();

           int result = helper.Add(10, 20);
           Assert.That(result, Is.EqualTo(30));

           result = helper.Add(15, -10);
           Assert.That(result, Is.EqualTo(5));
       }

       // Not ideal, multiple test methods with unnecessary test names would be needed
       [Test]
       public void AddPositiveNumbers()
       {
           MathHelper helper = new MathHelper();

           int result = helper.Add(10, 20);
           Assert.That(result, Is.EqualTo(30));
       }
       [Test]
       public void AddNegativeNumbers()
       {
           MathHelper helper = new MathHelper();

           int result = helper.Add(-10, -20);
           Assert.That(result, Is.EqualTo(-30));
       }
}

```

The above example is ideal to what Dr. Beaty and Dr. Dollard said when it comes to testing arguments. A test method can be written generically and then test cases with data can be easily passed in without having to write up multiple test methods for different kinds of data or writing a very long test method with many types of data and assertions.



### Naming conventions
When a large group is working on a project, it is always a good idea to use universal naming conventions. This does not only apply to the code itself, but to the names of the classes and functions as well.

1. Methods - Each testing method should be named by giving a brief description of what exactly it is testing for using the “MethodName_Description” format. 

2. Classes - The naming convention here is to simply add “Test” to the name of the class which contains the method(s) we are testing. In the previous example, the Add function was part of the MathHelper object, so we named the test class **MathHelperTest**.

Because of this naming convention, we will know exactly what portion of the test either passes or fails without having to expand each individual test case. Without even knowing any code, we would understand exactly what to look at if “EmailHasValidEmailAddress” in the “StudentTest” class failed the unit test.




### Authors

It makes more sense to tag an author in the creation of a test fixture and the test methods. Other authors can come in and edit the test fixture by adding a new test method or changing a test method. The `[Author("Joe Doe", "Amanda Doe")] would be ideal for adding multiple authors.

```C#
[TestFixture]
    [Author("Richard")]
    public class Test1
    {
        [TestCase(10, 20, 30)]
        [TestCase(-5, 15, 10)]
        [Author("Joe")]
        public void AddNumbersTest(int a, int b, int expected)
```

Richard was the one who created the test fixture but Joe added the test method later. If both Richard and Joe made the fixture then naturally they would both be in there as well.




### Direct help
For other problems or questions you can contact the following

* Richard - rdesilve@msudenver.edu 
* Andrew - abecke11@msudenver.edu 
* Nick - nbeier@msudenver.edu 
