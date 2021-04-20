#### My notes from Robert Cecil Martin's Clean Code book 
# 

# Contents

   [Introduction](#introduction)
1. [Clean Code](#cleancode)
2. [Meaningful Names](#meaningfulnames)
3. [Functions](#functions)


# <a name="introduction"> Introduction</a>

Measurement of code quality: WTF/minute

# <a name="cleancode">1. Clean code</a>
Wading on bad code decreases productivity. After a time, teams require for a redesign due to odious code base. After a time since redesing started, new teams may demand another redesign. So keeping the code clean is not just cost-effective - is also a matter of professional survival.

Change of requirements or schedule are not excuses for make a mess in code and this mess is our problem not managers or other stakeholders. 

Understanding the risks of making messes is programmer's mission.

Messes slow down the programmers. 

Bjarne Stroustrup (inventor of C++): the logic should be straightforward to make it hard for bugs to hide. Code should be elegant and efficient.

Changing or adding bad code tempts the mess to grow. Error handling is important for elegant and efficient code. 

Each function, each class, each module exposes a single-minded attitude.

Grady Booch (author ofOOA and design with applications): Clean code should be well-readable. It never obscures designer's intent. 

Clean code should containt only what is necessary.

Dave Thomas (Programmer and author): Clean code ehanced by a developer other than its original author. It has unit, acceptance tests, meaningful names. <b> It provides one way rather than many ways of doing one thing </b>. Minimal dependencies which are explicitly defined and a clear minimal API.

There is a difference between code that is easy to read and code that is easy to change. 

<b>Code without tests is not clean. TDD impacts!</b>
Smaller code is better.  

Micheal Feathers (author of Working Effectivelt with Legacy Code): Clean code is code that has been taken care of.

Ron Jeffries (author of XP Installed and XP Adventures in C#): Simple code runs all the test, no duplication, expresses all the design ideas that are in the system. Minimizes number of entities classes, methods, funcs etc..
 
 Expressiveness is meaningful naming.
 One object or one method does the one thing. Objects can be broken into two or more objects. Methods can be extracted to submethods that expresses how job is done.

 Abstraction has significant advantages to implement particular functionalities.

 Ward Cunningham (inventor of Wiki): Clean code is the code that you expected while you're reading it. Clean code is not surprising, it is simple, tells you what will happen next and obvious. 

You cannot write code if you cannot read the surrounding code. 

Always leave the campground cleaner than you found it. The Boy Scout Rule. Leave the code cleaner than you found it. Therefore code could not rot. Little clean ups are enough to achieve code simply got better. 


# <a name="meaningfulnames"> 2. Meaningful Names</a>

## Use intention-Revealing Names

Name should tell why it exists, what it does, how it is used. If name requires comment it is bad naming.

```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceMofification;
int fileAgeInDays;
```
<hr/>

```java
public List<int[]> getThem() {
   List<int[]> list1 = new ArrayList<int[]>();
   for (int[] x : theList)
      if (x[0] == 4)
         list1.add(x);
   return list1;
 }
```
Indentation is reasonable but above code tells nothing about what it is doing. Doesn't answer any questions about its entities. What kind of things inside theList? What is the 0th item is? What about value 4? How would I use the list being returned?

<hr/>

Let's say we are working on a mine sweeper game. The board is a list of cells called theList. We can rename that to gameBoard.

Each cell on the board is represented by a simple array. 0th index holds the value of status and if value of status equals to 4 then it means cell is "flagged".

```java
public List<int[]> getFlaggedCells() {
   List<int[]> flaggedCells = new ArrayList<int[]>();
   for (int[] cell : gameBoard)
      if (cell[STATUS_VALUE] == FLAGGED)
         flaggedCells.add(cell);
   return flaggedCells;
 }
```
Simplicity of code has not changed. Same number of operators and constants. Same nesting levels. But code now tells more about itsel, it is more explicit. 

We can make it more explicit by adding simple class for cells and include an intention-revealing function (<code>isFlagged</code>).

```java
public List<Cell> getFlaggedCells() {
   List<Cell> flaggedCells = new ArrayList<Cell>();
   for (Cell cell : gameBoard)
      if (cell.isFlagged())
         flaggedCells.add(cell);
   return flaggedCells;
 }
```
<hr/>

## Avoid Disinformation

Avoid leaving false clues when naming like hp, aix, sco. They're the name of Unix plaforms or variants. 

If accountList is not actually a <code> List</code> don't name that as accountList. If it is a container but not a list <code>accountGroup</code>, <code>bunchOfAccounts</code> or <code> accounts</code> would be better. 

<i>Even container is a List better not to encode container type into the name.</i> 

Using names which vary in small ways is not good. It is hard to spot difference between <code>XYZControllerForEfficientHandlingOfStrings</code> and <code>XYZControllerForEfficientStorageOfStrings</code> 

Beware of using lower case <code>L</code> and upper-case <code>O</code>.

<hr/>

## Make Meaningful Distinctions

If names must be different, then they should also mean something diferrent.


<code>(a1, a2, .. aN)</code> are non-informative. They provide no clue about intention of the author. 


```java
public static void copyChars(char a1[], char a2[]) {
   for (int i = 0; i < a1.length; i++) {
      a2[i] = a1[i];
   }
}
```
Above  would be better as below,

```java
public static void copyChars(char source[], char destination[]) {
   for (int i = 0; i < source.length; i++) {
      destination[i] = source[i];
   }
}
```
<hr/>

<code>Info</code> and <code>Data</code> are indistinct noise words like <code>a</code>, <code>an</code> and <code>the</code>.

There is nothing wrong using prefix conventions like <code>the</code>, <code>a</code> the problem is using them when just trying to escape from duplicates etc.

<code>NameString</code>, <code>CustomerObject</code> are bad namings of classes. Name can't be floating point anyway. If so, there is disinformation. What is the difference between <code>Customer</code> and <code>CustomerObject</code> if both namings exist?

<hr/>

```java
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```
How do we know which to call above functions?

Beware of indistinguishable namings. <code>customer</code> is indistinguishable from  <code>customerInfo</code>, <code>message</code> is indistiguishable from <code>theMessage</code>

<hr/>

## User Pronounceable Names

<code>gnymdhms</code> (generation date, year, month, day, hour, minute, second) 

```java
class DtaRcrd102 {
   private Date genymdhms;
   private Date modymdhms;
   private final String pszqint = "102";
}
```
Pronunciation is very hard, unmeaningful and silly for above namings. Just makes us waste time to pronounce it!


```java
class Customer {
   private Date generationTimeStamp;
   private Date modificationTimeStamp;
   private final String recordId = "102";
}
```
<i>There is a funny joke in the book at this part, check it out :D</i>

## Use Searchable Names

Don't use single-letter names, it is hard to search them. Robert's personal preference is using single-letters <b>only</b> as local variables inside short methods. <b>The lenght of a name should correspond to the size of its scope.</b>

It is imperative to give search-friendly names to constants if they are used in body of code many times.

Compare,
```java
for (int j=0; j<34; j++) {
   s += (t[j]*4)/5;
}
```

to

```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
   for (int j=0; j < NUMBER_OF_TASKS; j++) {
      int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
      int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
      sum += realTaskWeeks;
   }
```

Although <code>sum</code> is not particularly useful name it is easy to search. Good naming makes the function longer but at least it is very easy to search for constants. 

## Avoid Encodings

Encoding type or scope information to names just adds an extra burden to other programmers. And encoded names are seldom pronunceable and are easy to mis-type.

<b>Hungarian Notation</b>

Java programmers don't need type encoding. HN and other forms of type encoding are simply impediments. When using them it is very hard to change the name or type of a variable, function, or class. They make it harder to read the code. They can mislead the reader.

```java
PhoneNumber phoneString;
// name not changed when type changed!
```
<b>Member Prefixes</b>

There is no need to prefix member variables with <code>m_</code>. Classes and functions should be small enough that we don't need them. We should use editing environments that highlights members to make them distinct.

```java
public class Part {
   private String m_dsc; // The textual description
   void setName(String name) {
   m_dsc = name;
   }
}
```
<hr/>

```java
public class Part {
   String description;
   void setDescription(String description) {
   this.description = description;
   }
}
```

<b>Interfaces and Implementations</b>

Leave the interfaces unadorned. Not <code>IShapeFactory</code> but <code>ShapeFactory</code>.
If we must encode either the interface or the implementation, ecnoding the implementation would be better choice. E.g <code>ShapeFactoryImp</code>.

## Avoid Mental Mapping

Readers should not have to translate namings into other names they already know. This problem refers to naming variables with single-letter. For example <code>i, j, k</code> (never l!). Reader must mentally map these single-letters to the actual concept. 
Clarity is very important to be a professional programmer.

## Class Names

Classes and objects should have noun or noun phrase like <code>Customer</code>, <code>WikiPage</code>, <code>Account</code> and <code>AddressParse</code>. Avoid words like <code>Manager</code>, <code>Processor</code>, <code>Data</code>, <code>Info</code>. A class name should not be a verb.

## Method Names

Methods should have verb or verb phrase names like <code>postPayment</code>, <code>deletePage</code>. 
Accessors, mutators and predicates should be prefixed with <code>get</code>, <code>set</code>, <code>is</code> according to the javabean standard.

When constructors are overloaded, use static factory methods with names that describe the arguments.

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```
is generally better than

```java
Complex fulcrumPoint = new Complex(23.0);
```
Enforcing ther use by making the corresponding constructors private.

## Don't Be Cute

>Say what you mean. Mean what you say.

No need to make jokes on naming.

## Pick One Word per Concept

It is confusing to use <code>fetch</code>, <code>retrieve</code> and <code>get</code> as equivalent methods of different classes. 

The function names should be consistent and have to stand alone. Having a <code>controller</code>, <code>manager</code>, <code>driver</code> in the same code base is confusing. What is the essential difference between them? Name can lead programmers to think these methods expect or return different type of objects. Consistency on naming is important for programmers who must use our code.

## Don't Pun

Avoid using the same word for more than one purpose. Using the same term form other ideas is a pun. According to <code>one word per concept</code> rule we could end up many classes have an <code>add</code> method. As long as the parameter lists and return values of methods are sementically equivalent there is no problem. 

Let's say we have already had an <code>add</code> method which concantenates 2 parameters. If we are just writing a method to adding a simple parameter to a collection we should use <code>append</code> or <code>insert</code> instead of <code>add</code>. Because using <code>add</code> in this case would be a pun.

We want to make ourselves clear while writing a code that readers can easily understand and don't find themselves in an intense study.

## Use Solution Domain Names

It is encouraged to use CS terms, algorithm names, pattern names, mat terms etc. It might be a problem using problem domain in everywhere which could cause to make co-workers' tasks harder. <code>AccountVisitor</code>, <code>JobQueue</code> etc they are all technical names and usually the most appropriate course.

## Use Problem Domain Names

Seperating solution and problem domain concepts is a very important part of being a good programmer and designer. Problem domain concepts related names should be drawn from the problem domain.

## Add Meaningful Context

It is obvious that <code>firstName</code>, <code>lastName</code>, <code>street</code>, <code>houseNumber</code>, <code>city</code>, <code>state</code>, <code>zipCode</code> values form an address. But can we infer that <code>state </code> belongs to address when it is alone in the code? We can add <code>addr</code> prefix to these names to make a clear and meaningful context. Then readers will understand these variables belongs to a bigger concept. The better solution is to create a class named <code>Address</code>. 

<hr/>

Below code has 3 variables but context must be inferred. When we look at the method it is very big the meanings of the variables are opaque. 

```java
private void printGuessStatistics(char candidate, int count) {
   String number;
   String verb;
   String pluralModifier;
   if (count == 0) {
      number = "no";
      verb = "are";
      pluralModifier = "s";
   } else if (count == 1) {
      number = "1";
      verb = "is";
      pluralModifier = "";
   } else {
      number = Integer.toString(count);
      verb = "are";
      pluralModifier = "s";
   }
   String guessMessage = String.format(
   "There %s %s %s%s", verb, number, candidate, pluralModifier
   );
   print(guessMessage);
}
```
If we split the function into smaller pieces we would have a clear context for the three variables. They are definitively belongs to the <code>GuessStatisticsMessage</code> class. The improvement of context allows the algorithm more clean and clear by breaking it into many smaller functions.

```java
public class GuessStatisticsMessage {
   private String number;
   private String verb;
   private String pluralModifier;
   
   public String make(char candidate, int count) {
      createPluralDependentMessageParts(count);
      return String.format(
         "There %s %s %s%s",
         verb, number, candidate, pluralModifier );
   }

   private void createPluralDependentMessageParts(int count) {
      if (count == 0) {
         thereAreNoLetters();
      } else if (count == 1) {
         thereIsOneLetter();
      } else {
         thereAreManyLetters(count);
      }
   } 

   private void thereAreManyLetters(int count) {
      number = Integer.toString(count);
      verb = "are";
      pluralModifier = "s";
   }

   private void thereIsOneLetter() {
      number = "1";
      verb = "is";
      pluralModifier = "";
   }

   private void thereAreNoLetters() {
      number = "no";
      verb = "are";
      pluralModifier = "s";
   }
}
```

## Don't Add Gratuitous Context

Let's suppose there is an application called "Gas Station Deluxe", it is bad to prefix every class with <code>GSD</code>. Shorter names are generally better than longer ones as they are clear. There is no need to add more context to a name than is necessary. <code>Address</code> is fine for a class name and instances can be <code>accountAddress</code> and <code>customerAddress</code>.  


## Final Words
Choosing good names is a teaching issue rather than technical or business or management. It requires a shared cultural background. We don't need to be afraid when refactoring someone else's code as there are various editor tools to help us. These improvements will pay off in the short and long run. 


# <a name="functions">3. Functions</a>

Below function is too long. It has duplicated code, lots of odd strings and many strange- inobvious data types and APIS.  



```java
public static void testableHtml(
   PageData pageData,
   boolean includeSuiteSetup
) throws Exception {
   WikiPage wikiPage = pageData.getWikiPage();
   StringBuffer buffer = new StringBuffer();
   if (pageData.hasAttribute("Test")) {
       if (includeSuiteSetup) {
           WikiPage suiteSetup =
                   PageCrawlerImpl.getInheritedPage(
                           SuiteResponder.SUITE_SETUP_NAME, wikiPage
                   );
           if (suiteSetup != null) {
               WikiPagePath pagePath =
                       suiteSetup.getPageCrawler().getFullPath(suiteSetup);
               String pagePathName = PathParser.render(pagePath);
               buffer.append("!include -setup .")
                       .append(pagePathName)
                       .append("\n");
           }
       }
       WikiPage setup =
               PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
       if (setup != null) {
           WikiPagePath setupPath =
                   wikiPage.getPageCrawler().getFullPath(setup);
           String setupPathName = PathParser.render(setupPath);
           buffer.append("!include -setup .")
                   .append(setupPathName)
                   .append("\n");
       }
   }
   buffer.append(pageData.getContent());
   if (pageData.hasAttribute("Test")) {
       WikiPage teardown =
               PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
       if (teardown != null) {
           WikiPagePath tearDownPath =
                   wikiPage.getPageCrawler().getFullPath(teardown);
           String tearDownPathName = PathParser.render(tearDownPath);
           buffer.append("\n")
                   .append("!include -teardown .")
                   .append(tearDownPathName)
                   .append("\n");
       }
       if (includeSuiteSetup) {
           WikiPage suiteTeardown =
                   PageCrawlerImpl.getInheritedPage(
                           SuiteResponder.SUITE_TEARDOWN_NAME,
                           wikiPage
                   );
           if (suiteTeardown != null) {
               WikiPagePath pagePath =
                       suiteTeardown.getPageCrawler().getFullPath(suiteTeardown);
               String pagePathName = PathParser.render(pagePath);
               buffer.append("!include -teardown .")
                       .append(pagePathName)
                       .append("\n");
           }
       }
   }
   pageData.setContent(buffer.toString());
   return pageData.getHtml();
}
```

With just a few simple method extractions, some renaming and a little restructuring it is possible to capture the intent of the function.


```java
public static String renderPageWithSetupsAndTeardowns(
   PageData pageData, boolean isSuite
) throws Exception {
   boolean isTestPage = pageData.hasAttribute("Test");
   if (isTestPage) {
       WikiPage testPage = pageData.getWikiPage();
       StringBuffer newPageContent = new StringBuffer();
       includeSetupPages(testPage, newPageContent, isSuite);
       newPageContent.append(pageData.getContent());
       includeTeardownPages(testPage, newPageContent, isSuite);
       pageData.setContent(newPageContent.toString());
   }
   return pageData.getHtml();
}
```

What is it that makes a function like above? How can we make a function communicate its intent?

## Small!

Functions should be small. Functions should be very small. Functions should hardly ever be 20 lines long. 

Above code should still be shortened as below. 

```java
public static String renderPageWithSetupsAndTeardowns(
   PageData pageData, boolean isSuite) throws Exception {
   if (isTestPage(pageData))
      includeSetupAndTeardownPages(pageData, isSuite);
   return pageData.getHtml();
}
```

<b>Blocks and Indenting</b>

Blocks within if <code>if</code>, <code>else</code>, <code>while</code> and so on should be one line long. It adds documentary value in addition to keeping the enclosing function small because the function called can have a nicely descriptive name.

This also implies functions should not be large enough to hold nested structures. Therefore indent level of a function should not be greater than one or two. This makes the functions easier to read and understand.

## Do One Thing

First code does a lot of things. Creating buffers, fetching pages, rendering paths, generating HTML and so on. But last code is doing one simple thing. <b>Functions should do one thing. They should do it well. They should do it only.</b>

But there is a problem that actually the last code does "one thing". 

It is doing:

1. Determining whether the page is a test page.
2. If so, including setups and teardowns.
3. Rendering the page in HTML.

So is the function doing one thing or three things? Three steps of the function are one level of abstraction below the stated name of the function. 
We can describe it as a brief TO: 

<i>TO RenderPageWithSetupsAndTeardowns, we check to see whether the page is a test page
and if so, we include the setups and teardowns. In either case we render the page in
HTML.</i>

If the function does only steps that are one level below the stated name of the function, then it is doing one thing. We write functions to decompose a larger concept into a set of steps at the next level of abstraction.

We could extract the <code>if</code> statement to function <code>includeSetupsAndTeardownsIfTestPage</code>, but that restates the code without changing the level of abstraction.

Functions that do one thing cannot be reasonably divided into sections.

## One Level of Abstraction Per Function 

We need to make sure all statements within our function must be at the same level of abstraction. 

First code includes different level of abstractions. <code>.getHtml();</code> is high level abstraction, <code>String pagePathName = PathParser.render(pagePath);</code> is intermediate level abstraction and <code>.append("\n")</code> is low level abstraction. In this case readers may have some problems with essential concept or a detail.

 <b>Reading Code from top top Bottom: The Stepdown Rule </b>

 <i>We want the code to read like a top-down narrative.</i> Every function must be followed by those at the next level of abstraction so that we can read the program. In other words we want to be able to read the program as it were a set of TO paragraphs. Each of them should describe the current level of abstraction and refer to next level down. 

 ```
 To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns.

   To include the setups, we include the suite setup if this is a suite, then we includethe
   regular setup.

   To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page
   and add an include statement with the path of that page.

   To search the parent...
 ```
 </code>

This rule is key to keep functions short and making them to do "one thing." 

## Switch Statements

Switch statements generally don't do one thing. We can bury switch statements in a low level class with polymorphism to make them not repeat.

```java
public Money calculatePay(Employee e)
throws InvalidEmployeeType {
   switch (e.type) {
      case COMMISSIONED:
         return calculateCommissionedPay(e);
      case HOURLY:
         return calculateHourlyPay(e);
      case SALARIED:
         return calculateSalariedPay(e);
      default:
         throw new InvalidEmployeeType(e.type);
   }
}
```
Above function is large and it may grow if there are new types of employee. It violates SRP and OCP. 

The solution to this problem is creating an abstract factory and hide details of implementation. Factory will create derivatives of <code>Employee</code> based on their type.

```java
public abstract class Employee {
   public abstract boolean isPayday();
   public abstract Money calculatePay();
   public abstract void deliverPay(Money pay);
}
-----------------
public interface EmployeeFactory {
   public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}
-----------------
public class EmployeeFactoryImpl implements EmployeeFactory {
   public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
      switch (r.type) {
         case COMMISSIONED:
            return new CommissionedEmployee(r) ;
         case HOURLY:
            return new HourlyEmployee(r);
         case SALARIED:
            return new SalariedEmploye(r);
         default:
            throw new InvalidEmployeeType(r.type);
      }
   }
}
```

## Use Descriptive Names

One principle is choosing good names for small functions that do one thing.
The smaller and more focues a function is, the easier it is to choose a descriptive name.

A long descriptive name is better than a short enigmatic name. A long name is also better than a long descriptive comment. 

Use a naming convention that allows multiple words to be easily read and describe what function does.

Choosing descriptive names will clarify the design of the module in your mind and help you to improve it.

Consistency is important in names.

## Function Arguments

The ideal number of arguments for a function is zero, then one then two. More than three arguments requires very special justification. 

Arguments are also harder from a testing point of view. Writing all test cases to ensure various combinations of arguments is very difficult. 

Output arguments are harder to understand than input arguments.

<b>Common Monadic Forms</b>

There are two very common reasons to pass a single argument into a function. You may be
asking a question about that argument, as in <code>boolean fileExists(“MyFile”)</code>. Or you may be
operating on that argument, transforming it into something else and returning it. For
example, <code>InputStream fileOpen(“MyFile”)</code> transforms a file name String into an
InputStream return value. These two uses are what readers expect when they see a function. You should choose names that make the distinction clear, and always use the two
forms in a consistent context.

Try to avoid any monadic functions that don’t follow these forms, for example, <code>void
includeSetupPageInto(StringBuffer pageText)</code>. 

<b>Flag Arguments</b>

Using flag arguments is terrible practice. It complicates the signature of the method.  This function also does one more than one thing. It does one thing if the flag is true and another if the flag is false!

<code>render(boolean isSuite)</code> is bad practice. <code>renderForSuite()</code> and <code>renderForSingleTest()</code> is better. 

<b>Dyadic Functions</b>

A function with two arguments is harder to understand than a monadic function. For example, <code>writeField(name)</code> is easier to understand than <code>writeField(output-Stream, name)</code>. Though the meaning of both is clear, the first glides past the eye, easily depositing its
meaning. The second requires a short pause until we learn to ignore the first parameter.
And that, of course, eventually results in problems because we should never ignore any
part of code. The parts we ignore are where the bugs will hide.

Even obvious dyadic functions like <code>assertEquals(expected, actual)</code> are problematic.
How many times have you put the actual where the expected should be? The two arguments have no natural ordering. The expected, actual ordering is a convention that
requires practice to learn


<b>Triads</b>

Triads aare significantly harder to understand than dyads.

<b>Argument Objects</b>

When a function seems to need more than two or three arguments, it is likely that some of
those arguments ought to be wrapped into a class of their own. 

```java
Circle makeCircle(double x, double y, double radius);
--
Circle makeCircle(Point center, double radius);
```




<b>Argument Lists</b>

Below method is dyadic. 
```java
public String format(String format, Object... args)
```

Same rules apply for the lists. Not more than 3 arguments. 

<b>Verbs and Keywords</b>

<code>write(name)</code> is evocative <code>writeField(name)</code> is even better. 

<code>assertEquals</code> might be better written as <code>assertExpectedEqualsActual(expected, actual)</code>

This helps to remember the ordering of the arguments.

## Have No Side Effects

Function promises to do one thing but it does other hidden things.


<code>checkPassword</code> seems to do one thing but it also initializes the session. There is a side effect and this side effect creates temporal coupling. you want to be sure that is safe to initialize the session.
```java
public class UserValidator {
   private Cryptographer cryptographer;
   public boolean checkPassword(String userName, String password) {
      User user = UserGateway.findByName(userName);
      if (user != User.NULL) {
         String codedPhrase = user.getPhraseEncodedByPassword();
         String phrase = cryptographer.decrypt(codedPhrase, password);
         if ("Valid Password".equals(phrase)) {
            Session.initialize();
            return true;
         }
      }
      return false;
   }
}
```
If you must do temporal coupling change the name of the method as <code>checkPasswordAndInitializeSession</code>.


<b>Output Arguments</b>

<code>appendFooter(s);</code> 
Does this function append s as the footer to something? Or does it append some footer
to s? Is s an input or an output? It doesn’t take long to look at the function signature
and see:
<code>public void appendFooter(StringBuffer report)</code>

Better,
<code>report.appendFooter();</code>

In general output arguments should be avoided. If function must change the state of something, it can change its owning object's state.

## Command Query Separation

Functions either change the state of an object or return some informatio about that object. Not both at the same time.

> PREFER EXCEPTIONS TO RETURNING ERROR CODES


### Extract Try/Catch Blocks

```java
public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch (Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMessage());
}
```

### Error handling is One Thing
Error ahanding is a one thing, and functions should do one thing. Thus, a function handles errors should do nothing else. 


### The <b>Error.java</b> Dependency Magnet 

```java
public enum Error {
   OK,
   INVALID,
   NO_SUCH,
   LOCKED,
   OUT_OF_RESOURCES,
   WAITING_FOR_EVENT;
   }
```

Above class must be imported and used by other classes. Requires recompiling and redoploying. Instead use use exceptions. They can be extended so application of Open-Closed Principle. 

### DON'T REPEAT YOURSELF

Duplication is the evil of all evil in software. 

### STRUCTURED PROGRAMMING
Dijstra's rules of structured programming: One entry in to function and one exit from the function. No <code>break</code>, <code>countinue</code>  or <code>goto</code> statements.

If we keep functions small return break or continue statements won't be harmful.

### HOW DO YOU WRITE FUNCTIONS LIKE THIS?

First draft is disorganizied and clumsy. Then massage the code, refine, restructure, split functions, change names, eliminate duplications, shrink methods, shrink classes, write good unit tests meanwhile.

