#### My notes from R.C. Martin's Clean Code book 
# 

# Contents

   [Introduction](#introduction)
1. [Clean Code](#cleancode)
2. [Meaningful Names](#meaningfulnames)

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

<b>Use intention-Revealing Names</b>

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
<b>Avoid Disinformation</b>

Avoid leaving false clues when naming like hp, aix, sco. They're the name of Unix plaforms or variants. 

If accountList is not actually a <code> List</code> don't name that as accountList. If it is a container but not a list <code>accountGroup</code>, <code>bunchOfAccounts</code> or <code> accounts</code> would be better. 

<i>Even container is a List better not to encode container type into the name.</i> 

Using names which vary in small ways is not good. It is hard to spot difference between <code>XYZControllerForEfficientHandlingOfStrings</code> and <code>XYZControllerForEfficientStorageOfStrings</code> 

Beware of using lower case <code>L</code> and upper-case <code>O</code>.

<hr/>

<b>Make Meaningful Distinctions</b>

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

<b>User Pronounceable Names</b>

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
class DtaRcrd102 {
   private Date generationTimeStamp;
   private Date modificationTimeStamp;
   private final String recordId = "102";
}
```
<i>There is a funny joke in the book at this part, check it out :D</i>











































