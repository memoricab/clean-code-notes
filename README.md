#### My notes from R.C. Martin's Clean Code book 
# 

# Contents

   [Introduction](#introduction)
1. [Clean Code](#cleancode)

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

Dave Thomas (Programmer and author): Clean code ehanced by a developer other than its original author. It has unit, acceptance tests, meaningful names. <b> It provide one way rather than many ways of doing one thing </b>. Minimal dependencies which are explicitly defined and a clear minimal API.

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


